---
title: "Application Domain Resource Monitoring | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "monitoring managed memory use by application domain"
  - "application domains, memory use"
  - "memory use, monitoring"
  - "application domains, resource monitoring"
ms.assetid: 318bedf8-7f35-4f00-b34a-2b7b8e3fa315
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Application Domain Resource Monitoring
应用程序域资源监控 \(ARM\) 使宿主可以监控应用程序域对 CPU 和内存的使用情况。  这对于在长期运行的进程中使用很多应用程序域的宿主（例如 ASP.NET）很有用。  宿主可以卸载对整个进程的性能有不利影响的应用程序的应用程序域，但前提是它可以标识有问题的应用程序。  ARM 提供可用于协助做出此类决定的信息。  
  
 例如，承载服务可能具有很多在 ASP.NET 服务器上运行的应用程序。  如果进程中的一个应用程序开始消耗太多的内存或太多的处理器时间，则承载服务可使用 ARM 标识引起问题的应用程序域。  
  
 ARM 是一个轻量服务，可以在实时应用程序中使用。  可以通过使用 Windows 事件跟踪 \(ETW\) 访问此信息，也可以通过托管 API 或本机 API 直接访问此信息。  
  
## 启用资源监控  
 可以通过以下四种方式启用 ARM：在启动公共语言运行时 \(CLR\) 时提供一个配置文件，使用非托管承载 API，使用托管代码或侦听 ARM ETW 事件。  
  
 一旦启用 ARM，它就会开始收集有关进程中的所有应用程序域的数据。  如果某个应用程序域是在启用 ARM 之前创建的，则累计数据将从启用 ARM 时（而不是创建该应用程序域时）开始。一旦启用 ARM，则无法将其禁用。  
  
-   通过向配置文件中添加[\<appDomainResourceMonitoring\>](../../../docs/framework/configure-apps/file-schema/runtime/appdomainresourcemonitoring-element.md)元素并将`enabled` 特性设置为`true`，可在 CLR 启动时启用 ARM。  `false` 值（默认值）只意味着在启动时没有启用 ARM；稍后可以通过使用其他激活机制之一来激活它。  
  
-   通过请求 [ICLRAppDomainResourceMonitor](../../../ocs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-interface.md) 承载接口，宿主可启用 ARM。  一旦成功获取此接口，即会启用 ARM。  
  
-   通过将静态（Visual Basic 中为 `Shared`）<xref:System.AppDomain.MonitoringIsEnabled%2A?displayProperty=fullName> 属性设置为 `true`，托管代码可以启用 ARM。  一旦设置该属性，即会启用 ARM。  
  
-   通过侦听 ETW 事件，可在启动后启用 ARM。  当通过使用 `AppDomainResourceManagementKeyword` 关键字来启用公共提供程序 `Microsoft-Windows-DotNETRuntime` 时，启用 ARM 并开始对所有应用程序域引发事件。  若要将数据与应用程序域和线程关联起来，还必须使用 `ThreadingKeyword` 关键字来启用 `Microsoft-Windows-DotNETRuntimeRundown` 提供程序。  
  
## 使用 ARM  
 ARM 可提供由应用程序域使用的总处理器时间和有关内存使用的三类信息。  
  
-   **应用程序域的总处理器时间（以秒为单位）**：这是通过将操作系统为所有线程报告的线程时间加起来计算得到的，这些线程在其生存期内均在应用程序域中执行了一定时间的操作。  被阻塞的线程或休眠线程不使用处理器时间。  当一个线程调入本机代码时，线程在本机代码中花费的时间将计入到执行调用的应用程序域的计数中。  
  
    -   托管 API：<xref:System.AppDomain.MonitoringTotalProcessorTime%2A?displayProperty=fullName> 属性。  
  
    -   承载 API：[ICLRAppDomainResourceMonitor::GetCurrentCpuTime](../Topic/ICLRAppDomainResourceMonitor::GetCurrentCpuTime%20Method.md) 方法。  
  
    -   ETW 事件：`ThreadCreated`、`ThreadAppDomainEnter` 和 `ThreadTerminated` 事件。  有关提供程序和关键字的信息，请参见 [CLR ETW 事件](../../../docs/framework/performance/clr-etw-events.md)中的“AppDomain 资源监控事件”。  
  
-   **在生存期中由应用程序域执行的总托管分配空间量（以字节为单位）**：总的分配空间量并不总是反映应用程序域的内存使用情况，这是因为分配的对象的生存期可能很短。  但是，如果应用程序分配并释放大量的对象，则分配的开销可能是有意义的。  
  
    -   托管 API：<xref:System.AppDomain.MonitoringTotalAllocatedMemorySize%2A?displayProperty=fullName> 属性。  
  
    -   承载 API：[ICLRAppDomainResourceMonitor::GetCurrentAllocated](../Topic/ICLRAppDomainResourceMonitor::GetCurrentAllocated%20Method.md) 方法。  
  
    -   ETW 事件：`AppDomainMemAllocated` 事件、`Allocated` 字段。  
  
-   **由应用程序域引用的并且未由最近的完整的阻塞式回收释放的托管内存（以字节为单位）**：此数字只有在完整的阻塞式回收之后才是准确的。（这与在后台执行的不阻塞应用程序的并发回收正好相反。）例如，<xref:System.GC.Collect?displayProperty=fullName> 方法重载将导致完整的阻塞式回收。  
  
    -   托管 API：<xref:System.AppDomain.MonitoringSurvivedMemorySize%2A?displayProperty=fullName> 属性。  
  
    -   承载 API：[ICLRAppDomainResourceMonitor::GetCurrentSurvived](../Topic/ICLRAppDomainResourceMonitor::GetCurrentSurvived%20Method.md) 方法，`pAppDomainBytesSurvived` 参数。  
  
    -   ETW 事件：`AppDomainMemSurvived` 事件、`Survived` 字段。  
  
-   **由进程引用的并且未由最近的完整的阻塞式回收释放的总托管内存（以字节为单位）**：各个应用程序域的未释放的内存与此数字一致。  
  
    -   托管 API：<xref:System.AppDomain.MonitoringSurvivedProcessMemorySize%2A?displayProperty=fullName> 属性。  
  
    -   承载 API：[ICLRAppDomainResourceMonitor::GetCurrentSurvived](../Topic/ICLRAppDomainResourceMonitor::GetCurrentSurvived%20Method.md) 方法、`pTotalBytesSurvived` 参数。  
  
    -   ETW 事件：`AppDomainMemSurvived` 事件、`ProcessSurvived` 字段。  
  
### 确定完整的阻塞式回收发生的时间  
 若要确定未释放的内存计数何时是准确的，需要知道何时执行了完整的阻塞式回收。  执行此操作的方法取决于用于检查 ARM 统计信息的 API。  
  
#### 托管 API  
 如果使用 <xref:System.AppDomain> 类的属性，则可以使用 <xref:System.GC.RegisterForFullGCNotification%2A?displayProperty=fullName> 方法来注册完整回收的通知。  使用的阈值并不重要，因为您等待的是回收的完成而不是回收的方法。  然后可以调用 <xref:System.GC.WaitForFullGCComplete%2A?displayProperty=fullName> 方法，该方法将进行阻塞，直至完成完整的回收。  可以创建一个线程，用于以循环方式调用方法并在方法返回时执行任何必需的分析。  
  
 或者，可以定期调用 <xref:System.GC.CollectionCount%2A?displayProperty=fullName> 方法以查看第 2 代回收的计数是否已增加。  根据轮询频率，此方法可能无法提供有关发生完整回收的准确指示。  
  
#### 承载 API  
 如果使用未托管的承载 API，则宿主必须为 CLR 传递 [IHostGCManager](../../../ocs/framework/unmanaged-api/hosting/ihostgcmanager-interface.md) 接口的实现。  当 CLR 继续执行在回收发生时已挂起的线程时，它将调用 [IHostGCManager::SuspensionEnding](../Topic/IHostGCManager::SuspensionEnding%20Method.md) 方法。  CLR 将传递已完成的回收的代数作为该方法的参数，因此，宿主可以确定回收是完整的或还是部分的。  您的 [IHostGCManager::SuspensionEnding](../Topic/IHostGCManager::SuspensionEnding%20Method.md) 方法实现可查询未释放的内存，以确保在更新计数后立即对其进行检索。  
  
## 请参阅  
 <xref:System.AppDomain.MonitoringIsEnabled%2A?displayProperty=fullName>   
 [ICLRAppDomainResourceMonitor 接口](../../../ocs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-interface.md)   
 [\<appDomainResourceMonitoring\>](../../../docs/framework/configure-apps/file-schema/runtime/appdomainresourcemonitoring-element.md)   
 [CLR ETW 事件](../../../docs/framework/performance/clr-etw-events.md)