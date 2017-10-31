---
title: "桥接和错误处理 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4ae87d1a-b615-4014-a494-a53f63ff0137
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# 桥接和错误处理
此示例演示 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 路由服务如何用于在使用不同绑定的客户端和服务之间桥接通信。此示例还演示如何将备份服务用于故障转移方案。路由服务是一个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 组件，使用该组件可方便地在您的应用程序中包含基于内容的路由器。此示例采用标准的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 计算器示例，用于使用路由服务进行通信。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\RoutingServices\ErrorHandlingAndBridging`  
  
## 示例详细信息  
 在此示例中，计算器客户端配置为将消息发送到由路由器公开的一个终结点。路由服务配置为接受发送给它的所有消息，然后将这些消息转发至与计算器服务对应的终结点。下面几点介绍了主要计算器服务、备份计算器服务和计算器客户端的配置，以及客户端和服务之间如何使用路由服务进行通信：  
  
-   计算器客户端配置为使用 BasicHttpBinding，而计算器服务配置为使用 NetTcpBinding。将消息发送到计算器服务之前，路由服务将根据需要自动转换这些消息，同时还会转换响应，以便计算器客户端可对它们进行访问。  
  
-   路由服务知道两种计算器服务：主要计算器服务和备份计算器服务。路由服务首先尝试与主要计算器服务终结点通信。如果此尝试因该终结点关闭而失败，则路由服务尝试与备份计算器服务终结点通信。  
  
 因此，从客户端发送的消息将由路由器接收，并重新路由到实际的计算器服务。如果计算器服务终结点关闭，则路由服务将消息路由到备份计算器服务终结点。来自备份计算器服务的消息将发送回服务路由器，后者将这些消息传递回计算器客户端。  
  
> [!NOTE]
>  一个备份列表中可具有多个定义的终结点。在此情况下，如果备份服务终结点关闭，则路由服务尝试连接到列表中的下一个备份终结点，直到成功进行连接。  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 打开 RouterBridgingAndErrorHandling.sln。  
  
2.  在 Visual Studio 中按 F5 或 Ctrl\+Shift\+B  
  
    1.  如果要在按 F5 时自动启动所需的项目，请右击该解决方案，选择**“属性”**，然后在**“通用属性”**下的**“启动项目”**节点中选择**“多启动项目”**，并将所有项目设置为**“启动”**。  
  
    2.  如果使用 Ctrl\+Shift\+B 生成项目，则必须启动以下应用程序：  
  
        1.  计算器客户端 \(.\/CalculatorClient\/bin\/client.exe\)  
  
        2.  计算器服务 \(.\/CalculatorService\/bin\/service.exe\)  
  
        3.  路由服务 \(.\/RoutingService\/bin\/RoutingService.exe\)  
  
3.  在计算器客户端中，按 Enter 启动客户端。  
  
     您应看到以下输出：  
  
    ```Output  
    Add(100,15.99) = 115.99  
    Subtract(145,76.54) = 68.46  
    Multiply(9,81.25) = 731.25  
    Divide(22,7) = 3.14285714285714  
  
    ```  
  
## 可通过代码或 App.config 进行配置  
 所提供的示例配置为使用 App.config 文件来定义路由器行为。也可将 App.config 文件的名称更改为无法识别的其他名称，并将对 `ConfigureRouterViaCode()` 的方法调用取消注释。以上任一方法都可产生相同的路由器行为。  
  
### 方案  
 此示例演示作为协议桥和错误处理程序的服务路由器。在此方案中，没有发生基于内容的路由；路由服务充当一个透明的代理节点，该节点配置为将消息直接传递到目标终结点的预配置集。该路由服务还执行一些附加步骤，以透明方式处理在其尝试发送到已配置为与之通信的终结点时发生的错误。通过充当协议桥，路由服务使用户能够为外部通信定义一个协议，并为内部通信定义另一个协议。  
  
### 实际方案  
 Contoso 希望在内部优化性能的同时，向外界提供一个可互操作的服务终结点。因此，它通过一个使用 BasicHttpBinding 的终结点向外界公开其服务，而在内部使用路由服务将该连接桥接到使用 NetTcpBinding（由其服务使用）的终结点。而且，Contoso 还希望其提供的服务能够容许他们的任何一个生产服务发生暂时中断，从而通过使用错误处理功能来虚拟化路由器服务后面的多个终结点，以便在必要时自动故障转移到备份终结点。  
  
## 请参阅  
 [AppFabric 承载和持久性示例](http://go.microsoft.com/fwlink/?LinkId=193961)