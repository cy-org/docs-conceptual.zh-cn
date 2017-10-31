---
title: "发送和处理错误 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 98e8e04d-2ac9-4a33-ae08-462f757a7a14
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 发送和处理错误
此示例演示如何使用 <xref:System.ServiceModel.Activities.SendReply> 和 <xref:System.ServiceModel.Activities.ReceiveReply> 消息传递活动来发送和接收预期的和意外的错误。在此方案中，第一个客户端请求导致已包含在其 <xref:System.ServiceModel.Activities.Send.KnownTypes%2A> 集合中的预期错误。在最终请求成功之前，接下来的几个客户端请求会导致接收意外错误。  
  
## 使用此示例  
  
1.  通过右击 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 图标并选择**“以管理员身份运行”**，使用提升的权限打开 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)]。  
  
2.  打开 Faults.sln 解决方案文件。  
  
3.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
4.  运行服务项目。  
  
    1.  在**“解决方案资源管理器”**中，右击 `FaultService` 项目，然后选择**“设为启动项目”**。  
  
    2.  按 Ctrl\+F5。  
  
5.  通过右击 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 图标并选择**“以管理员身份运行”**，用提升的权限打开 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 的另一个副本。  
  
6.  打开 Faults.sln 解决方案文件。  
  
7.  运行客户端项目。  
  
    1.  在**“解决方案资源管理器”**中，右击 `FaultClient` 项目，然后选择**“设为启动项目”**。  
  
    2.  按 Ctrl\+F5。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Services\Faults`  
  
## 请参阅