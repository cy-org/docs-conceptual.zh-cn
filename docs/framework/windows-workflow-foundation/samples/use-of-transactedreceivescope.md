---
title: "使用 TransactedReceiveScope | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d455f1dc-bfc5-43d6-8ae9-bc3b3a3ea08a
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 使用 TransactedReceiveScope
此示例演示如何使用 <xref:System.Activities.Statements.TransactionScope> 将事务从客户端流动到服务器，以在客户端上创建一个新的事务和一个 <xref:System.ServiceModel.Activities.TransactedReceiveScope>，从而接收具有流动的事务的消息，并确定事务在服务器上的生存期范围。此示例由充当客户端和服务器角色的两个项目组成。  
  
## 客户端应用程序  
 客户端应用程序运行一个工作流，该工作流输出分布式事务 ID，向服务器发送消息，流动事务，接收回复，再次输出分布式事务 ID 并完成操作。最初输出分布式事务 ID 时，它是一个空 GUID，因为事务仍然仅为本地事务。  
  
## 服务器应用程序  
 服务器项目与客户端项目相似，不过，工作流承载于 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 中，因为它必须在一个终结点上侦听来自客户端的消息。工作流位于 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 的中心，后者从客户端接收流动的事务，输出已发送的消息，输出分布式事务 ID 并向客户端发送回复。分布式事务 ID 现在为非空 GUID，如果已在 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 的主体中添加了一个识别事务的活动，则它将在流动的事务下执行。  
  
#### 运行示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开 TransactedReceiveScope.sln 解决方案。  
  
2.  若要生成该解决方案，请按 CTRL\+SHIFT\+B 或从**“生成”**菜单中选择**“生成解决方案”**。  
  
3.  在成功生成之后，右击该解决方案，然后选择**“设置启动项目”**。从对话框中选择**“多启动项目”**，并确保两个项目的操作都设置为**“启动”**。  
  
4.  按 F5，或从**“调试”**菜单中选择**“开始调试”**。或者，可以按 Ctrl\+F5 或从**“调试”**菜单中选择**“开始执行\(不调试\)”**，以便在不调试情况下运行。  
  
    > [!NOTE]
    >  在启动客户端之前，服务器必须正在运行。承载服务的控制台窗口的输出将指示它启动的时间。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Transactions\TransactedReceiveScope`  
  
## 请参阅