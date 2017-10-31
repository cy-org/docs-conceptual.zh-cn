---
title: "事务队列范围 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 37141708-a29f-4b6a-81fe-f8a11f825061
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 事务队列范围
此示例演示如何创建“并行保护”消息传递活动模式与 <xref:System.ServiceModel.Activities.TransactedReceiveScope>，以便构建一个协议，允许很多操作在同一事务下按任意顺序执行。此示例还演示 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 如何在某个事务无法流向服务器时自动创建新的事务，以便客户端不使用任何事务。  
  
 该示例由两个表示客户端和服务器的工作流项目组成。客户端项目运行一个工作流，此工作流在开始时会发送一条消息来启动服务器工作流，服务器工作流将初始化一个关联并为其余的消息传递活动启动一个事务范围。客户端 <xref:System.Activities.Statements.Sequence> 活动包含一个初始 <xref:System.ServiceModel.Activities.Send> 和 <xref:System.ServiceModel.Activities.ReceiveReply> 对，之后是一个带三个分支的 <xref:System.Activities.Statements.Parallel> 活动。每个分支都向服务器发送单向消息。<xref:System.Activities.Statements.Parallel> 活动的 <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> 属性设置为 `false`，以便完成所有三个分支。  
  
 服务器工作流与客户端工作流类似，只不过消息传递活动面向的是通信的服务器端且包含在 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 活动中，以便在同一个事务下执行所有工作。当服务器上收到第一条消息时，将创建一个事务，然后使该事务成为 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 正文范围的环境事务，以便此范围中的任何活动都可以访问该事务。之后，将并行执行所有接收。所有接收必须刚好执行一次，如并行活动的完成条件所述。<xref:System.ServiceModel.Activities.TransactedReceiveScope> 正文的末尾有一个隐式持久性点，并且还将在同一事务下执行持久性操作。  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 ParallelConvoySample.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  确保两个项目都设置为启动。  
  
    1.  在**“解决方案资源管理器”**中右击解决方案，并选择**“设置启动项目”**。  
  
    2.  选择**“多启动项目”**，并确保两个项目的操作都设置为**“启动”**。  
  
4.  若要运行解决方案，请按 Ctrl\+F5。  
  
     服务器将输出 `Server is running`，它指示服务器已准备就绪。  
  
     在客户端控制台窗口中按任意键以启动示例。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Scenario\Transactions\TransactedConvoyScope`  
  
## 请参阅