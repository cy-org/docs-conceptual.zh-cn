---
title: "事务处理队列 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b1b011dd-5e0b-482c-9bb0-9d8727038f14
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 事务处理队列
此示例演示如何在 [!INCLUDE[wf](../../../../includes/wf-md.md)] 中集成队列和事务，以创建可靠的且可伸缩的服务。在客户端工作流中使用 <xref:System.Activities.TransactionScope>，在一个使用 <xref:System.ServiceModel.NetMsmqBinding> 的事务中将消息传递给队列。在服务器上使用 <xref:System.ServiceModel.Activities.TransactedReceiveScope>，在同一个事务中从队列接受消息并更新工作流的状态。  
  
## 演示  
 <xref:System.Activities.Statements.TransactionScope>、<xref:System.ServiceModel.Activities.TransactedReceiveScope>、<xref:System.ServiceModel.NetMsmqBinding>、<xref:System.ServiceModel.Activities.Receive> 和基于内容的相关性。  
  
## 讨论  
 为了演示此示例中涉及的功能，将创建一个 `RewardsPoints` 工作流服务，该服务跟踪为给定帐户赚取和使用的点数。客户端使用 <xref:System.Activities.WorkflowInvoker> 来模拟向队列发送各种请求。若要在一个事务中将消息发送到队列中，可以将 <xref:System.ServiceModel.Activities.Send> 活动放在 <xref:System.Activities.Statements.TransactionScope> 的 <xref:System.Activities.Statements.TransactionScope.Body%2A> 的内部。在此示例中，首先运行客户端，然后运行服务器，演示队列消息如何分离客户和服务器应用程序。  
  
 在客户端完成之后，将配置并承载服务。一旦服务打开，它便会开始处理已放置在队列中的消息。在同一个服务器事务中接收和处理每条消息。在此示例中，接收的第一条消息是一个 `CreateAccount` 请求，该请求根据作为请求消息的一部分传递的帐户名，创建实例并初始化内容相关性。为了模拟现实世界中可能需要的服务类型，在 `while` 循环内的平行分支中放置两个 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 活动（分别用于处理 `AddPoints` 和 `UsePoints` 消息），以便这两个活动可以按任意顺序重复处理这些消息。  
  
 <xref:System.Activities.Statements.TransactionScope> 和 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 在其范围的结尾都有一个隐式的持久性点。因此，通过在 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 中将这些活动与队列组合使用，可以将工作流从一个一致状态可靠地移动到下一个一致状态，同时确保消息绝不丢失。  
  
#### 设置、生成和运行示例  
  
1.  安装和配置 MSMQ。有关详细信息，请参见[安装消息队列](http://go.microsoft.com/fwlink/?LinkId=178526)（可能为英文网页）。  
  
2.  通过在命令行上执行以下命令来确保 MSDTC 正在运行。`net start msdtc`  
  
3.  编译项目并打开可执行文件，或在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开项目并从“调试”菜单中选择一个启动选项。首先，创建队列，然后运行客户端并将消息发送到队列，最后启动服务并处理消息。按 Enter 退出程序。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Scenario\Transactions\TransactedQueues`