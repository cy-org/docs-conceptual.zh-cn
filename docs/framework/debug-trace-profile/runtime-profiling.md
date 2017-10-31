---
title: "运行时分析"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- performance counters
- common language runtime, profiling
- Perfmon.exe
- System Monitor
- profiling
- runtime, profiling
- profiling applications
- Performance Console
ms.assetid: ccd68284-f3a8-47b8-bc3f-92e5fe3a1640
caps.latest.revision: 22
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 9589e838eacd758d43ac9ceb1442d217e6406a03
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="runtime-profiling"></a>运行时分析
分析是用于在任何开发或部署方案中收集性能数据的方法。 本节面向想要收集有关应用程序性能的信息的开发人员和系统管理员。  
  
## <a name="tracking-performance-using-the-performance-monitor-perfmonexe"></a>使用性能监视器 (Perfmon.exe) 跟踪性能  
 性能监视器是用于分析 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 应用程序的最易于使用的工具。 性能监视器以图形方式表示随公共语言运行时和 [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)]一起安装的.NET Framework 性能计数器中的数据。 这些计数器可用于监视从内存管理到实时 (JIT) 编译器性能的方方面面。 它们告诉你应用程序所使用的资源的情况，这是了解应用程序性能的间接方法。 使用这些计数器可了解应用程序在内部的工作方式。  
  
#### <a name="to-run-perfmonexe-on-windows-vista-and-later-versions"></a>在 Windows Vista 和更高版本上运行 Perfmon.exe  
  
1.  在命令提示符处，键入 **perfmon**。 将出现“性能监视器”  控制台。  
  
2.  在“监视工具”  文件夹中，单击“性能监视器” 。  
  
3.  在“性能监视器”工具栏上，如果有“添加”  图标（加号），请单击该图标。 如果没有，请在监视器窗口中单击右键，然后选择“添加计数器”  选项。  
  
     这将打开“添加计数器”  对话框。 “可用计数器”  列表框中显示可用的性能对象。 .NET Framework 应用程序有许多预定义的对象，包括用于内存管理、互操作性、异常处理以及多线程处理的计数器，它们分别是“.NET CLR Memory”**.**、“.NET CLR Interop”、“.NET CLR Exceptions”和“.NET CLR LocksAndThreads”。 每个性能对象均包含多个单一性能计数器。 在性能监视器中的可用性能计数器列表，请参阅 [Performance Counters](../../../docs/framework/debug-trace-profile/performance-counters.md)一起安装的.NET Framework 性能计数器中的数据。  
  
4.  选择性能对象的名称旁边的复选框，以查看它所支持的各个性能计数器的列表。  
  
5.  单击要查看的性能计数器。  
  
6.  在“选定对象的实例”列表框中，单击“\<所有实例>”，指定要在全局（也就是在整个系统范围内）监视公共语言运行时的性能计数器。  
  
     - 或 -  
  
     在“选定对象的实例”  列表框中，单击要监视该应用程序的性能计数器的应用程序的名称。  
  
     若要区分运行时的多个版本，或消除具有相同名称的多个应用程序的歧义，还必须修改注册表项。 有关详细信息，请参阅 [Performance Counters and In-Process Side-By-Side Applications](../../../docs/framework/debug-trace-profile/performance-counters-and-in-process-side-by-side-applications.md)。  
  
> [!NOTE]
>  如果在性能控制台正在运行时安装新的性能计数器，请在停止后再重启性能控制台，以便显示新的计数器。  
  
 要分析位于某一区域或远程共享中的程序集，请确保该远程程序集在运行性能计数器的计算机上完全受信任。 如果该程序集不具有足够的信任，则性能计数器将不工作。 有关向不同区域授予信任的信息，请参阅 [Caspol.exe（代码访问安全策略工具）](../../../docs/framework/tools/caspol-exe-code-access-security-policy-tool.md)。  
  
> [!NOTE]
>  在安装有 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 的系统上，对于使用 **开发的应用程序，性能监视器可能不会显示某些类别的性能计数器数据，如“.NET CLR Data”****和“.NET CLR Networking”**[!INCLUDE[net_v11_short](../../../includes/net-v11-short-md.md)]。 如果属于这种情况，可以配置性能监视器以显示此数据，方法是将 [\<forcePerformanceCounterUniqueSharedMemoryReads>](../../../docs/framework/configure-apps/file-schema/runtime/forceperformancecounteruniquesharedmemoryreads-element.md) 元素添加到应用程序的配置文件。  
  
## <a name="reading-and-creating-performance-counters-programmatically"></a>以编程方式读取和创建性能计数器  
 可以使用 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 提供的类以编程方式访问性能控制台中提供的相同性能信息。 另外，还可以使用这些类创建自定义性能计数器。 下表描述了 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]中提供的某些性能监视类。  
  
|类|说明|  
|-----------|-----------------|  
|<xref:System.Diagnostics.PerformanceCounter?displayProperty=nameWithType>|表示 Windows NT 性能计数器组件。 使用此类可读取现有预定义或自定义计数器，并向自定义计数器发布（写入）性能数据。|  
|<xref:System.Diagnostics.PerformanceCounterCategory?displayProperty=nameWithType>|提供与计数器交互的几种方法以及计算机上计数器的类别。|  
|<xref:System.Diagnostics.PerformanceCounterInstaller?displayProperty=nameWithType>|指定 `PerformanceCounter` 组件的安装程序。|  
|<xref:System.Diagnostics.PerformanceCounterType?displayProperty=nameWithType>|为 `NextValue` 指定用于计算 `PerformanceCounter`的方法。|  
  
## <a name="see-also"></a>另请参阅  
 [Performance Counters](../../../docs/framework/debug-trace-profile/performance-counters.md)

