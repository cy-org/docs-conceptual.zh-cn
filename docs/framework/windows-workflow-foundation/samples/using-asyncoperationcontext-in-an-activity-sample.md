---
title: "在活动示例中使用 AsyncOperationContext | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0888a0bd-d227-4c00-ad6a-b654a01740e8
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 在活动示例中使用 AsyncOperationContext
此示例演示如何开发一个自定义 <xref:System.Activities.CodeActivity>，它使用 <xref:System.Activities.AsyncOperationContext> 在工作流外部异步执行工作。  
  
## 示例详细信息  
 该示例活动使用 <xref:System.IO.FileStream> 类上的 <xref:System.IO.FileStream.BeginWrite> 和 <xref:System.IO.FileStream.EndWrite> 方法以异步方式将数据写入文件。此处介绍的模式适合于与其他异步方法一起使用。在执行异步操作时，可以执行工作流中的其他活动，但无法持久化工作流。  
  
#### 设置、生成和运行示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开 Async.sln 示例解决方案。  
  
2.  生成和运行解决方案。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\CustomActivities\Code-Bodied\Async`  
  
## 请参阅