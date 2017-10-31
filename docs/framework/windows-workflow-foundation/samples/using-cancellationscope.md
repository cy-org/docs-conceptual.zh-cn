---
title: "使用 CancellationScope | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 39c5c338-b316-43d6-b7fe-a543281dd1ec
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 使用 CancellationScope
此示例演示如何使用 <xref:System.Activities.Statements.CancellationScope> 活动取消应用程序中的工作。  
  
 许多中间层组件和服务依靠已知的事务编程构造来处理针对它们的取消操作。  但在许多情况下，必须取消事务中无法执行的工作。  使用取消的难度大于使用事务的难度，这是因为必须先跟踪必须取消的工作。  [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] 通过提供 <xref:System.Activities.Statements.CancellationScope> 活动帮助您执行此操作。  
  
 可以从活动内或活动的父级触发取消。  按照父活动（如 <xref:System.Activities.Statements.Sequence>、<xref:System.Activities.Statements.Parallel>、<xref:System.Activities.Statements.Flowchart> 或自定义复合活动）来计划其子活动。  父活动可以出于任何原因取消子活动。  例如，只要带三个子分支的 <xref:System.Activities.Statements.Parallel> 活动完成一个分支且 <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> 表达式的计算结果为 `true`，该活动就会取消剩余子分支。  宿主应用程序可以调用 <xref:System.Activities.WorkflowApplication.Cancel%2A> 来外部取消工作流。  
  
 若要使用 <xref:System.Activities.Statements.CancellationScope> 活动，请将需要取消的工作置于 <xref:System.Activities.Statements.CancellationScope.Body%2A> 属性中，并将取消后执行的工作置于 <xref:System.Activities.Statements.CancellationScope.CancellationHandler%2A> 属性中。  
  
 此示例演示如何从活动自身内部取消活动。  
  
 此示例用来演示 <xref:System.Activities.Statements.CancellationScope> 活动的场景是：一个客户需要尽快购买到迈阿密的机票。  有两家旅行社希望承接此业务。  示例使用 <xref:System.Activities.Statements.CancellationScope> 活动中的两个 <xref:System.Activities.Statements.Parallel> 对此业务逻辑进行建模。  <xref:System.Activities.Statements.Parallel.CompletionCondition%2A> 活动的 <xref:System.Activities.Statements.Parallel> 设置为 `true`；由于在完成任何分支后将检查 <xref:System.Activities.Statements.Parallel.CompletionCondition%2A>，因此将导致剩余分支在第一个分支完成后被取消。  客户端应用程序会同时请求这两家旅行社购买机票，一旦第一家旅行社确认已购得机票，应用程序将取消对另一家旅行社所下的订单。  
  
## 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 CancelationScopeXAML.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 Ctrl\+F5。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Built-InActivities\CancellationScope`  
  
## 请参阅