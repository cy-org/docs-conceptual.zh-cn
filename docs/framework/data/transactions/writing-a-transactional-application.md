---
title: "编写事务应用程序  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a4d891f2-6fc8-4395-93c6-6819492406e0
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 编写事务应用程序 
作为事务应用程序程序员，您可以利用 <xref:System.Transactions> 命名空间所提供的两种编程模型来创建事务。可采用 <xref:System.Transactions.Transaction> 类来利用显式编程模型，也可采用 <xref:System.Transactions.TransactionScope> 类来利用隐式编程模型（其中的事务将由基础结构自动管理）。建议您使用隐式事务模型进行开发。在[使用事务范围实现隐式事务 ](../../../../docs/framework/data/transactions/implementing-an-implicit-transaction-using-transaction-scope.md)主题中可找到有关如何使用事务范围的更多信息。  
  
 这两种模型都支持在程序达到一致状态时提交事务。如果提交成功，就会永久提交事务。如果提交失败，事务就会中止。如果应用程序无法成功完成事务，则会尝试中止并撤消事务的效果。  
  
## 本节内容  
  
### 创建事务  
 <xref:System.Transactions> 命名空间提供了两种用于创建事务的模型。下列主题对这两种模型进行了介绍。  
  
 [使用事务范围实现隐式事务 ](../../../../docs/framework/data/transactions/implementing-an-implicit-transaction-using-transaction-scope.md)  
  
 描述 <xref:System.Transactions> 命名空间如何支持使用 <xref:System.Transactions.TransactionScope> 类创建隐式事务。  
  
 [使用 CommittableTransaction 执行显式事务 ](../../../../docs/framework/data/transactions/implementing-an-explicit-transaction-using-committabletransaction.md)  
  
 描述 <xref:System.Transactions> 命名空间如何支持使用 <xref:System.Transactions.CommittableTransaction> 类创建显式事务。  
  
### 升级事务管理  
 当事务需要访问其他应用程序域中的资源时，或者要登记到其他持久资源管理器时，事务会自动升级为由 MSDTC 管理。将在[事务管理升级 ](../../../../docs/framework/data/transactions/transaction-management-escalation.md)主题中介绍事务升级。  
  
### 并发  
 [使用 DependentTransaction 管理并发 ](../../../../docs/framework/data/transactions/managing-concurrency-with-dependenttransaction.md)主题演示如何使用 <xref:System.Transactions.DependentTransaction> 类在异步任务之间实现并发。  
  
### COM\+ 互操作  
 [与企业服务和 COM\+ 事务的互操作性 ](../../../../docs/framework/data/transactions/interoperability-with-enterprise-services-and-com-transactions.md)主题阐释如何使分布式事务与 COM\+ 事务交互。  
  
### 诊断  
 [诊断跟踪 ](../../../../docs/framework/data/transactions/diagnostic-traces.md)描述如何使用 <xref:System.Transactions> 基础结构所生成的跟踪代码排除应用程序中的错误。  
  
### 使用 ASP.NET  
 [在 ASP.NET 中使用 System.Transactions](../../../../docs/framework/data/transactions/using-system-transactions-in-aspnet.md) 主题描述如何才能在 ASP.NET 应用程序中成功使用 <xref:System.Transactions>。