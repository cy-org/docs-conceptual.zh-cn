---
title: "基于内容的相关 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8638b5d6-1d59-456d-8acd-179a5b39b260
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 基于内容的相关
此示例演示消息传递活动（<xref:System.ServiceModel.Activities.Send>、<xref:System.ServiceModel.Activities.Receive>、<xref:System.ServiceModel.Activities.SendReply> 和 <xref:System.ServiceModel.Activities.ReceiveReply>）如何用于多个基于内容的相关性和一个基于内容的相关性。在此方案中，首先基于订单 ID 初始化一个相关性，然后基于客户 ID 创建另一个相关性。这将演示 <xref:System.ServiceModel.Activities.Receive> 活动如何基于相同的传入消息，遵循现有相关性并初始化新的相关性。  
  
## 演示  
 消息传递活动和基于内容的相关性  
  
## 讨论  
 本示例演示如何使用多个基于内容的相关性。在此方案中，首先基于订单 ID 初始化一个相关性，然后基于客户 ID 创建另一个相关性。使用 <xref:System.ServiceModel.Activities.Receive> 活动级联这些相关性，该活动基于相同的传入消息遵循现有相关性 \(PurchaseOrderId\) 并初始化新的相关性 \(CustomerId\)。为实现此目的，<xref:System.ServiceModel.Activities.Receive> 活动使用 <xref:System.ServiceModel.Activities.Receive.CorrelatesOn%2A>、<xref:System.ServiceModel.Activities.Receive.CorrelatesWith%2A> 和 <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> 属性。  
  
## 使用此示例  
  
1.  通过右击 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 图标并选择**“以管理员身份运行”**，使用提升的权限打开 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)]。  
  
2.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 CascadingCorrelation.sln 解决方案文件。  
  
3.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
4.  若要运行服务器，请按 F5。  
  
5.  在服务准备就绪并开始侦听消息之后，在“解决方案资源管理器”中右击“Client”项目，并运行它。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Services\ContentBasedCorrelation`  
  
## 请参阅