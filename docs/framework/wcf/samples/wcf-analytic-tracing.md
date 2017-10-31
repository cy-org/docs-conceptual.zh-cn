---
title: "WCF 分析跟踪 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6029c7c7-3515-4d36-9d43-13e8f4971790
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# WCF 分析跟踪
此示例演示如何将您自己的跟踪事件添加到分析跟踪流中，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 将把该分析跟踪流写入 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] 中的 ETW。跟踪分析是为了便于查看服务，而不会导致较高性能损失。此示例演示如何使用 <xref:System.Diagnostics.Eventing?displayProperty=fullName> API 来写入与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务集成的事件。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] <xref:System.Diagnostics.Eventing?displayProperty=fullName> API 的更多信息，请参见 <xref:System.Diagnostics.Eventing?displayProperty=fullName>。  
  
 若要了解有关 Windows 中事件跟踪的更多信息，请参见[使用 ETW 改善调试和性能优化](http://go.microsoft.com/fwlink/?LinkId=166488)（可能为英文网页）。  
  
## 释放 EventProvider  
 此示例使用 <xref:System.Diagnostics.Eventing.EventProvider?displayProperty=fullName> 类，该类实现 <xref:System.IDisposable?displayProperty=fullName>。在实现 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的跟踪时，可以针对服务的生存期使用 <xref:System.Diagnostics.Eventing.EventProvider> 的资源。因此，为了便于阅读，此示例永远不会释放已包装的 <xref:System.Diagnostics.Eventing.EventProvider>。如果出于某种原因服务具有不同的跟踪要求，并且必须释放此资源，则应根据释放非托管资源的最佳做法来修改此示例。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]释放非托管资源的更多信息，请参见 [Implementing a Dispose Method](http://go.microsoft.com/fwlink/?LinkId=166436)（实现 Dispose 方法）。  
  
## 自我承载与Web 承载  
 对于 Web 承载的服务，WCF 的分析跟踪提供了一个名为“HostReference”的字段，该字段用于标识发出这些跟踪的服务。可扩展的用户跟踪可以参与此模型，此示例演示执行该操作的最佳做法。当竖线字符“&#124;”实际显示在生成的字符串中时，Web 宿主引用的格式可以是下面任何一种：  
  
-   如果该应用程序不在根处。  
  
     \<SiteName\>\<ApplicationVirtualPath\>&#124;\<ServiceVirtualPath\>&#124;\<ServiceName\>  
  
-   如果该应用程序在根处。  
  
     \<SiteName\>&#124;\<ServiceVirtualPath\>&#124;\<ServiceName\>  
  
 对于自承载服务，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的分析跟踪不会填充“HostReference”字段。此示例中的 `WCFUserEventProvider` 类在由自承载服务使用时，其行为是一致的。  
  
## 自定义事件详细信息  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的 ETW 事件提供程序清单定义了三个事件，这些事件设计为由 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务作者在服务代码内发出。下表显示了这三个事件的分类。  
  
|事件|说明|事件 ID|  
|--------|--------|-----------|  
|UserDefinedInformationEventOccurred|服务中发生的说明内容不是一个问题时发出此事件。例如，可以在对数据库成功进行调用后发出一个事件。|301|  
|UserDefinedWarningOccurred|发生的问题可能导致将来出现错误时发出此事件。例如，如果调用数据库失败，但能够通过回退到冗余数据存储区进行恢复，则可以发出一个警告事件。|302|  
|UserDefinedErrorOccurred|服务的行为方式不符合预期时发出此事件。例如，如果调用数据库失败且无法从其他位置检索数据，则可能会发出一个事件。|303|  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 打开 WCFAnalyticTracingExtensibility.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 Ctrl\+F5。  
  
     在 Web 浏览器中，单击**“Calculator.svc”**。服务的 WSDL 文档的 URI 应出现在浏览器中。复制该 URI。  
  
4.  运行 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 测试客户端 \(WcfTestClient.exe\)。  
  
     [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 测试客户端 \(WcfTestClient.exe\) 位于 \<[!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 安装目录\>\\Common7\\IDE\\ WcfTestClient.exe 中（默认 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 安装目录为 C:\\Program Files\\Microsoft Visual Studio 10.0）。  
  
5.  在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 测试客户端中，通过选择**“文件”**、**“添加服务”**来添加服务。  
  
     在输入框中添加终结点地址。  
  
6.  单击**“确定”**关闭对话框。  
  
     ICalculator 服务将添加到**“我的服务项目”**下的左窗格中。  
  
7.  打开事件查看器应用程序。  
  
     在调用服务之前，请启动事件查看器并确保事件日志正在侦听从 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务发出的跟踪事件。  
  
8.  在**“开始”**菜单中，选择**“管理工具”**，然后选择**“事件查看器”**。启用**“分析”**和**“调试”**日志。  
  
9. 在事件查看器的树视图中，导航到**“事件查看器”**、**“应用程序和服务日志”**、**“Microsoft”**、**“Windows”**、**“应用程序服务器”\-\>“应用程序”**。右击**“应用程序服务器”\-\>“应用程序”**，并选择**“查看”**，然后选择**“显示分析和调试日志”**。  
  
     确保已选中**“显示分析和调试日志”**选项。启用**“分析”**日志。  
  
     在事件查看器的树视图中，导航到**“事件查看器”**、**“应用程序和服务日志”**、**“Microsoft”**、**“Windows”**、**“应用程序服务器”\-\>“应用程序”**、**“分析”**。右击**“分析”**，然后选择**“启用日志”**。  
  
10. 使用 WCF 测试客户端来测试服务。  
  
    1.  在 WCF 测试客户端中，双击 ICalculator 服务节点下的**“Add\(\)”**。  
  
         **“Add\(\)”**方法将显示在右窗格中（带有两个参数）。  
  
    2.  为第一个参数键入 2，为第二个参数键入 3。  
  
    3.  单击**“调用”**调用该方法。  
  
11. 转到已经打开的**“事件查看器”**窗口。导航到**“事件查看器”**、**“应用程序和服务日志”**、**“Microsoft”**、**“Windows”**、**“应用程序服务器”\-\>“应用程序”**。  
  
12. 右击**“分析”**节点并选择**“刷新”**。  
  
     事件将显示在右窗格中。  
  
13. 使用 ID 303 来查找事件，然后双击该事件将其打开，并检查其内容。  
  
     此事件是由 ICalculator 服务的 `Add()` 方法发出的，并且具有一个负载等于“2\+3\=5”的负载。  
  
#### 清理（可选）  
  
1.  打开**“事件查看器”**。  
  
2.  导航到**“事件查看器”**、**“应用程序和服务日志”**、**“Microsoft”**、**“Windows”**、**“应用程序服务器”\-\>“应用程序”**。右击**“分析”**并选择**“禁用日志”**。  
  
3.  导航到**“事件查看器”**、**“应用程序和服务日志”**、**“Microsoft”**、**“Windows”**、**“应用程序服务器”\-\>“应用程序”**、**“分析”**。右击**“分析”**并选择**“清除日志”**。  
  
4.  单击**“清除”**清除这些事件。  
  
## 已知问题  
 **“事件查看器”**中存在一个已知问题，可能无法解码 ETW 事件。您可能会看到一条错误消息：“无法找到源“Microsoft\-Windows\-应用程序服务器\-应用程序”中事件 ID \<id\> 的说明。本地计算机上未安装引发此事件的组件，或者安装已损坏。可以安装或修复本地计算机上的组件。”如果遇到此错误，请从**“操作”**菜单中选择**“刷新”**。然后，该事件应能正确解码。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Management\ETWTrace`  
  
## 请参阅  
 [AppFabric 监视示例](http://go.microsoft.com/fwlink/?LinkId=193959)