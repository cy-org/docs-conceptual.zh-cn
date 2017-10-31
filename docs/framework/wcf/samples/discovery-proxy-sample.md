---
title: "发现代理示例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1dfa02df-15b1-4e97-9c8e-f5f2772711b0
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 发现代理示例
此示例演示如何创建发现代理的实现以存储有关现有服务的信息，并演示客户端如何可以查询该代理以获取信息。此示例由三个项目组成：  
  
-   **服务**：一个简单的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 计算器服务，它向发现代理注册自身。  
  
-   **发现代理**：发现代理服务的实现。  
  
-   **客户端**：一个 WCF 客户端应用程序，它将调用发现代理以搜索服务。  
  
## 演示  
 发现代理实现  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Discovery\DiscoveryProxy`  
  
## DiscoveryProxy  
 在 Program.cs 文件的 `Main`方法中，该示例演示如何承载 <xref:System.ServiceModel.Discovery.DiscoveryProxy> 类型的服务。它公开两个终结点，一个终结点为 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint> 类型，另一个终结点为 <xref:System.ServiceModel.Discovery.AnnouncementEndpoint> 类型。两个终结点都将 TCP 用作传输。<xref:System.ServiceModel.Discovery.DiscoveryEndpoint> 正在侦听 `probeEndpointAddress` 参数指定的 URI，客户端可以在此处发送探测消息以向代理查询其数据。<xref:System.ServiceModel.Discovery.AnnouncementEndpoint> 正在侦听 `announcementEndpointAddress` 参数指定的 URI。代理将在这里侦听公告。接收到联机公告时，代理将服务添加到其缓存；当接收到脱机公告时，代理从其缓存移除服务。  
  
 DiscoveryProxy.cs 包含 <xref:System.ServiceModel.Discovery.DiscoveryProxy> 的实现。代理必须从 <xref:System.ServiceModel.Discovery.DiscoveryProxyBase> 类继承，并需要 <xref:System.Runtime.Remoting.Messaging.AsyncResult> 的实现。在进行实例化时，代理将创建一个新的 <xref:Systems.Collections.Generic.Dictionary%601>，用于存储它所知道的元素。  
  
 该文件分为两个区域：代理缓存方法区域和发现代理实现区域。代理缓存方法区域包含用于更新 <xref:Systems.Collections.Generic.Dictionary%601>、对 <xref:Systems.Collections.Generic.Dictionary%601> 执行查询和打印用户数据的方法。发现代理实现区域包含公告和探测功能所需的重写方法。这些方法定义在接收到联机公告、脱机公告或探测消息后代理执行的操作。  
  
## 服务  
 在服务项目中的 Program.cs 文件中，相同的 URI 将用于其公告终结点以作为发现代理。这是因为服务使用该终结点发送公告，而代理使用该终结点接收公告。服务使用 <xref:System.ServiceModel.Discovery.DiscoveryBehavior>，并向其添加一个公告终结点。  
  
## 客户端  
 客户端项目针对其探测终结点使用相同的 URI 作为代理。这是因为此方案中的探测还特别单播到代理上可用的终结点。客户端连接到此已知地址，然后查询该地址以获取服务。一旦发现服务，它就会连接到该服务。  
  
#### 使用此示例  
  
1.  在 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 中加载项目解决方案，然后生成项目。  
  
2.  首先运行 \[解决方案基目录\]\\DiscoveryProxy\\bin\\debug 中生成的发现代理应用程序。首先必须运行发现代理，因为 TCP 公告终结点必须做好让服务发送其公告的准备。  
  
3.  然后运行 \[解决方案基目录\]\\Service\\bin\\debug 中生成的服务应用程序。启动时，该服务将公告发送到发现代理的公告终结点，并在该代理的缓存中注册。  
  
4.  接下来运行 \[解决方案基目录\]\\Client\\bin\\debug 中生成的客户端应用程序。客户端查询该代理，获取服务地址，然后连接到该服务。  
  
5.  最后终止客户端、服务和代理。代理必须运行，以便它能接收服务的脱机公告。  
  
## 请参阅