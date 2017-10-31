---
title: "事务回滚 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7f377147-7529-4689-a588-608cee87fdf8
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 事务回滚
此示例演示如何创建一个自定义 <xref:System.Activities.NativeActivity>，用于访问环境 <xref:System.Activities.RuntimeTransactionHandle> 以获取环境事务并显式回滚它。  
  
## 示例详细信息  
 在工作流中，当最外面的 <xref:System.Activities.Statements.TransactionScope> 或 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 完成时，将会自动完成一个事务。当未经处理的异常跨过范围边界传播时，将会隐式回滚一个事务。但是，您有时可能有必要显式回滚一个事务，而不必引发异常。在这种情况下，您可以使用此示例中的类似的自定义回滚活动，显式中止环境事务并提供一个可选的异常原因。  
  
 `RollbackActivity` 是一个 <xref:System.Activities.NativeActivity>， 因为它需要访问执行属性以获取环境 <xref:System.Activities.RuntimeTransactionHandle>。在 `Execute` 方法中，它包含 <xref:System.Activities.RuntimeTransactionHandle> 并检查它是否为 `null`，null 表示没有通过环境运行时事务来使用该活动。然后，它获取该事务，并再次检查是否存在 `null`。即使没有初始化运行时事务，也可能会有一个环境 <xref:System.Activities.RuntimeTransactionHandle>。最后，它通过调用 <xref:System.Transactions.Transaction.Rollback%2A> 并指定用户提供的异常或表明活动已回滚事务的一般异常，中止事务。  
  
 演示工作流包含一个 <xref:System.Activities.Statements.TransactionScope>，它的主体在 `RollbackActivity` 执行前后输出事务状态。请注意，即使已回滚事务，<xref:System.Activities.Statements.TransactionScope> 也会完成执行操作，并且在主体完成之前不会中止工作流。工作流中止的原因是 <xref:System.Activities.Statements.TransactionScope.AbortInstanceOnTransactionFailure%2A> 属性默认设置为 `true`。  
  
#### 使用此示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中加载 TransactionRollback.sln 解决方案。  
  
2.  按 Ctrl\+Shift\+B 生成解决方案。  
  
3.  按 Ctrl\+F5 运行应用程序。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Scenario\Transactions\TransactionRollback`  
  
## 请参阅  
 [事务](../../../../docs/framework/windows-workflow-foundation//workflow-transactions.md)