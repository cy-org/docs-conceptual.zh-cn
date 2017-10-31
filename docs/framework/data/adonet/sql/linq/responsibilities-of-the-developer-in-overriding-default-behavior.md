---
title: "开发人员在重写默认行为方面的责任 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c6909ddd-e053-46a8-980c-0e12a9797be1
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 开发人员在重写默认行为方面的责任
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 不强制满足以下要求，但如果这些要求未得到满足，就会导致行为不明确。  
  
-   重写方法不能调用<xref:System.Data.Linq.DataContext.SubmitChanges%2A> 或 <xref:System.Data.Linq.Table%601.Attach%2A>。  如果在重写方法中调用这些方法，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 会引发异常。  
  
-   重写方法不能用来启动、提交或停止事务。  <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 操作以事务的形式执行。  内嵌的事务可能会干扰外层事务。  加载重写方法只能在它们确定 <xref:System.Transactions.Transaction> 中未在执行相应操作后启动事务。  
  
-   重写方法应遵循适用的开放式并发映射。  发生开放式并发冲突时，重写方法应引发 <xref:System.Data.Linq.ChangeConflictException>。  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 会捕获此异常，以便您可以正确处理 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 时提供的 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 选项。  
  
-   Create \(`Insert`\) 和 `Update` 重写方法在相应操作成功完成后应使数据库生成的列的值流回对应的对象成员。  
  
     例如，如果 `Order.OrderID` 映射到标识列（autoincrement 主键），则 `InsertOrder()` 重写方法必须检索数据库生成的 ID 并将 `Order.OrderID` 成员设置为该 ID。  同样，时间戳成员必须更新为数据库生成的时间戳值，以确保更新后的对象一致。  如果未能传播数据库生成的值，则会造成数据库与 <xref:System.Data.Linq.DataContext> 跟踪的对象之间不一致。  
  
-   调用正确的动态 API 是用户的责任。  例如，在更新重写方法中，只能调用 <xref:System.Data.Linq.DataContext.ExecuteDynamicUpdate%2A>。  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 不检测或验证调用的动态方法是否与适用的操作相匹配。  如果调用了不适用的方法（例如，为要更新的对象调用了 <xref:System.Data.Linq.DataContext.ExecuteDynamicDelete%2A>），则结果是不明确的。  
  
-   最后，重写方法应执行明确的操作。  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 操作（如预先加载、延迟加载和 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>））的语义要求重写提供明确的服务。例如，只返回空集合而不检查数据库内容的加载重写有可能会造成数据不一致。  
  
## 请参阅  
 [自定义插入、更新和删除操作](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md)