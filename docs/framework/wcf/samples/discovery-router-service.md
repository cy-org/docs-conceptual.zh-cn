---
title: "发现路由器服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3d30af47-b24f-40e5-833a-24d77125c9e6
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 发现路由器服务
此示例演示如何将发现消息转发到另一个终结点。  
  
## 演示  
 发现路由  
  
## 讨论  
 路由发现在以下方案中非常有用：客户端正在使用代理来查找服务，该代理不知道这种服务，但知道另一个代理。此代理可以将发现数据包从此客户端转发到第二个代理。第二个代理可以查找该服务，然后将响应返回到原始客户端。  
  
 在此示例中，客户端将一条消息发送到发现路由组件。此消息将发送到发现路由器上的一个特定终结点。然后，该路由器将此消息转发到一个 UDP 多播终结点。探测消息将到达该多播终结点，侦听 UDP 多播地址的服务将对该发现路由器做出响应。发现路由器收集这些响应，然后将它们发送回客户端。  
  
#### 设置、生成和运行示例  
  
1.  生成示例。  
  
2.  运行 DiscoveryRouter 可执行文件。  
  
3.  从生成目录运行服务可执行文件。  
  
4.  运行客户端可执行文件。请注意，客户端将查找服务。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Discovery\DiscoveryRouter`