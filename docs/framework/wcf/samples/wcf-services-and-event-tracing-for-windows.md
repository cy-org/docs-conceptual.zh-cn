---
title: "针对 Windows 的 WCF 服务和事件跟踪 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eda4355d-0bd0-4dc9-80a2-d2c832152272
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 针对 Windows 的 WCF 服务和事件跟踪
此示例演示如何使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中的分析跟踪在 Windows 事件跟踪 \(ETW\) 中发出事件。  分析跟踪是在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 堆栈中的关键点处发出的事件，用于在生产环境中排除 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的故障。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务中的分析跟踪是可以在生产环境中以最小性能影响启用的跟踪。  这些跟踪都以事件的形式向 ETW 会话发出。  
  
 此示例包括一个基本 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务，事件从该服务向事件日志发出，使用事件查看器可以查看这些事件。  该示例还可以启动一个专用 ETW 会话，用于侦听来自 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的事件。  该示例包括一个用于创建专用 ETW 会话的脚本，该会话将事件存储在可以使用事件查看器读取的二进制文件中。  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 打开 EtwAnalyticTraceSample.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 Ctrl\+F5。  
  
     在 Web 浏览器中，单击**“Calculator.svc”**。  服务的 WSDL 文档的 URI 应出现在浏览器中。  复制该 URI。  
  
     默认情况下，服务开始在端口 1378 上侦听请求 \(http:\/\/localhost:1378\/Calculator.svc\)。  
  
4.  运行 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 测试客户端 \(WcfTestClient.exe\)。  
  
     [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 测试客户端 \(WcfTestClient.exe\) 位于 \<[!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 安装目录\>\\Common7\\IDE\\ WcfTestClient.exe 中（默认 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 安装目录为 C:\\Program Files\\Microsoft Visual Studio 10.0）。  
  
5.  在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 测试客户端中，通过选择**“文件”**，然后选择**“添加服务”**来添加服务。  
  
     在输入框中添加终结点地址。  默认值为 http:\/\/localhost:1378\/Calculator.svc。  
  
6.  打开事件查看器应用程序。  
  
     在调用服务之前，请启动事件查看器并确保事件日志正在侦听从 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务发出的跟踪事件。  
  
7.  在**“开始”**菜单中，选择**“管理工具”**，然后选择**“事件查看器”**。  启用**“分析”**和**“调试”**日志。  
  
8.  在事件查看器的树视图中，导航到**“事件查看器”**、**“应用程序和服务日志”**、**“Microsoft”**、**“Windows”**、**“应用程序服务器”\-\>“应用程序”**。  右击**“应用程序服务器”\-\>“应用程序”**，并选择**“查看”**，然后选择**“显示分析和调试日志”**。  
  
     确保已选中**“显示分析和调试日志”**选项。  
  
9. 启用**“分析”**日志。  
  
     在事件查看器的树视图中，导航到**“事件查看器”**、**“应用程序和服务日志”**、**“Microsoft”**、**“Windows”**、**“应用程序服务器”\-\>“应用程序”**。  右击**“分析”**，然后选择**“启用日志”**。  
  
#### 测试服务  
  
1.  切换回 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 测试客户端，然后双击 `Divide` 并保留默认值（指定分母为 0）。  
  
     如果分母为 0，则服务引发错误。  
  
2.  观察从服务发出的事件。  
  
     切换回事件查看器并导航到**“事件查看器”**、**“应用程序和服务日志”**、**“Microsoft”**、**“Windows”**、**“应用程序服务器”\-\>“应用程序”**。  右击**“分析”**，然后选择**“刷新”**。  
  
     WCF 分析跟踪事件显示在事件查看器中。  请注意，因为服务引发了错误，所以事件查看器中会显示错误跟踪事件。  
  
3.  重复步骤 1 和 2，但是使用有效的输入。  `N2` 参数的值可以为 0 之外的任何数。  
  
     刷新分析通道以查看 WCF 事件，可以看到不包含任何错误事件。  
  
 该示例演示从 WCF 服务发出的分析跟踪事件。  
  
#### 清理（可选）  
  
1.  打开事件查看器。  
  
2.  导航到**“事件查看器”**、**“应用程序和服务日志”**、**“Microsoft”**、**“Windows”**、**“应用程序服务器”\-\>“应用程序”**。  右击**“分析”**，然后选择**“禁用日志”**。  
  
3.  导航到**“事件查看器”**、**“应用程序和服务日志”**、**“Microsoft”**、**“Windows”**、**“应用程序服务器”\-\>“应用程序”**。  右击**“分析”**，然后选择**“清除日志”**。  
  
4.  选择**“清除”**选项以清除事件。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Management\ETWTracing`  
  
## 请参阅  
 [AppFabric 监视示例 （可能为英文网页）](http://go.microsoft.com/fwlink/?LinkId=193959)