---
title: "由 System.Transactions 提供的功能  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e458cef9-63b5-4401-b448-1536dcd9d9e5
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 由 System.Transactions 提供的功能 
本节描述如何使用 <xref:System.Transactions> 命名空间所提供的功能编写您自己的事务应用程序和资源管理器。具体来说，本节介绍如何创建事务（本地或分布式事务）并与一个或多个参与者一起参与该事务。  
  
## System.Transactions 概述  
 <xref:System.Transactions> 命名空间中的类所提供的基础结构通过支持在 SQL Server、ADO.NET、消息队列 \(MSMQ\) 和 Microsoft 分布式事务协调器 \(MSDTC\) 中启动的事务，使事务编程变得简单和高效。<xref:System.Transactions> 命名空间提供基于 <xref:System.Transactions.Transaction> 类的显式编程模型和使用 <xref:System.Transactions.TransactionScope> 类的隐式编程模型，在后一种模型中，事务由该基础结构自动管理。有关如何使用这两种模型创建事务应用程序的更多信息，请参见[编写事务应用程序 ](../../../../docs/framework/data/transactions/writing-a-transactional-application.md)。  
  
 此外，<xref:System.Transactions> 命名空间还提供了用于实现资源管理器的类型。资源管理器管理事务中使用的持久或可变数据，并与事务管理器协调工作，共同为应用程序提供了原子性和隔离性的保证。由 <xref:System.Transactions> 基础结构提供的事务管理器支持的事务可涉及到多个可变资源或单个持久资源。有关实现资源管理器的更多信息，请参见[实现资源管理器 ](../../../../docs/framework/data/transactions/implementing-a-resource-manager.md)。  
  
 此外，事务管理器还通过与基于磁盘的事务管理器（如 DTC）进行协调，透明地将本地事务升级为分布式事务，此时另一个持久资源管理器会将自身登记到事务中。<xref:System.Transactions> 基础结构提供增强性能的关键方式有两种。  
  
-   动态升级，它可确保事务跨多个分布式资源时 <xref:System.Transactions> 基础结构仅使用 MSDTC。有关动态升级的更多信息。请参见 [事务管理升级 ](../../../../docs/framework/data/transactions/transaction-management-escalation.md) 主题。  
  
-   可提升的登记，如果某个资源是参与事务的唯一实体，则允许该资源（如数据库）取得事务的所有权。以后在需要时，<xref:System.Transactions> 基础结构仍然可以将事务管理升级到 MSDTC。这样进一步减少了使用 MSDTC 的机会。[使用单阶段提交和可提升的单阶段通知进行优化 ](../../../../docs/framework/data/transactions/optimization-spc-and-promotable-spn.md)主题详细介绍了可提升的登记。  
  
 <xref:System.Transactions> 命名空间定义了三种限制访问它所公开的资源类型的信任级别：AllowPartiallyTrustedCallers \(APTCA\)、DistributedTransactionPermission\(DTP\) 和完全信任。有关各信任级别的更多信息，请参见[访问资源时的安全信任级别 ](../../../../docs/framework/data/transactions/security-trust-levels-in-accessing-resources.md)。  
  
## 本节内容  
  
### 编写事务应用程序  
 <xref:System.Transactions> 命名空间提供了两种用于创建事务应用程序的模型。[使用事务范围实现隐式事务 ](../../../../docs/framework/data/transactions/implementing-an-implicit-transaction-using-transaction-scope.md) 描述 <xref:System.Transactions> 命名空间如何支持使用 <xref:System.Transactions.TransactionScope> 类创建隐式事务。  
  
 [使用 CommittableTransaction 执行显式事务 ](../../../../docs/framework/data/transactions/implementing-an-explicit-transaction-using-committabletransaction.md)描述 <xref:System.Transactions> 命名空间如何支持使用 <xref:System.Transactions.CommittableTransaction> 类创建显式事务。  
  
 有关介绍事务应用程序编写的其他主题，请参见[编写事务应用程序 ](../../../../docs/framework/data/transactions/writing-a-transactional-application.md)。  
  
### 实现资源管理器  
 若要实现可参与事务的资源管理器，请参见[实现资源管理器 ](../../../../docs/framework/data/transactions/implementing-a-resource-manager.md)。该节将介绍资源登记、事务提交、故障后恢复以及最佳优化实践。