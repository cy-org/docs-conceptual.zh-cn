---
title: "事务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 51212219-a39e-448e-bff3-10064ff5de64
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 事务
本节包含用于演示使用 [!INCLUDE[wf](../../../../includes/wf-md.md)] 中的工作流事务的方案的示例。  
  
## 本节内容  
 [在命令式 TransactionScope 中执行工作流](../../../../docs/framework/windows-workflow-foundation/samples/execute-a-workflow-in-an-imperative-transactionscope.md)  
 演示如何利用命令性 C\# 代码在 <xref:System.Transactions.Transaction> 下使用 <xref:System.Activities.WorkflowInvoker> 执行工作流。  
  
 [事务队列范围](../../../../docs/framework/windows-workflow-foundation/samples/transaction-convoy-scope.md)  
 演示如何结合 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 创建“并行队列”消息传递活动模式以建立一个协议模型，在此协议中，在同一个事务下可以按任意顺序执行大量操作。  
  
 [事务回滚](../../../../docs/framework/windows-workflow-foundation/samples/transaction-rollback.md)  
 演示如何创建一个自定义 <xref:System.Activities.NativeActivity>，该活动访问环境 <xref:System.Activities.RuntimeTransactionHandle> 以获取环境事务并显式回滚它。  
  
 [禁止显示事务范围](../../../../docs/framework/windows-workflow-foundation/samples/suppress-transaction-scope.md)  
 演示如何创作自定义 `SuppressTransactionScope` 活动以禁止环境运行时事务（如果存在的话）。  
  
 [事务处理队列](../../../../docs/framework/windows-workflow-foundation/samples/transacted-queues.md)  
 演示如何在 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 中集成队列和事务，以便创建可靠的、可伸缩的服务。