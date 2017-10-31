---
title: "服务内的 TransactionScope 嵌套 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e7e1ba64-1384-4eba-add8-415636e2d6d0
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 服务内的 TransactionScope 嵌套
此示例包含两个演示如何在一个服务中处理 <xref:System.Activities.Statements.TransactionScope> 活动实例的方案。首先使用 <xref:System.Activities.Statements.TransactionScope> 活动发起事务，以在客户端上创建一个新的事务和要接收的 <xref:System.ServiceModel.Activities.TransactedReceiveScope>，并确定事务在服务器上的生存期范围。该服务内的第一个方案运行一个辅助 <xref:System.Activities.Statements.TransactionScope> 活动，以演示服务中的 <xref:System.Activities.Statements.TransactionScope> 活动的嵌套。第二个方案演示如何在嵌套的 <xref:System.Activities.Statements.TransactionScope> 活动中遵循超时限制。  
  
## 客户端应用程序  
 客户端应用程序运行一个工作流，该工作流启动一个 <xref:System.Activities.Statements.TransactionScope> 活动，输出分布式事务 ID，向服务器发送消息，流动事务，接收回复，再次输出分布式事务 ID 并完成操作。它对每个服务方案执行一次这样的操作。  
  
## 服务器应用程序  
 服务器项目承载于 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 中，后者可创建用于侦听来自客户端的消息的终结点。工作流位于 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 的中心，后者从客户端接收流动的事务，输出分布式事务 ID，然后再次执行 <xref:System.Activities.Statements.TransactionScope> 活动。在第一个方案中，事务成功完成。在第二个方案中，<xref:System.Activities.Statements.TransactionScope> 活动的主体是 5 秒延迟，事务的超时设置为 2 秒。当事务超时时，事务将会中止。  
  
#### 运行示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开 TransactionServiceExample.sln 解决方案。  
  
2.  若要生成该解决方案，请按 CTRL\+SHIFT\+B 或从**“生成”**菜单中选择**“生成解决方案”**。  
  
3.  在成功生成之后，右击该解决方案，然后选择**“设置启动项目”**。从对话框中选择**“多启动项目”**，并确保两个项目的操作都设置为**“启动”**。  
  
4.  按 F5，或从**“调试”**菜单中选择**“开始调试”**。或者，可以按 Ctrl\+F5 或从**“调试”**菜单中选择**“开始执行\(不调试\)”**，以便在不调试情况下运行。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Transactions\TRSCompostability`