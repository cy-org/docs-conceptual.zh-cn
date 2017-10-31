---
title: "NAVIGATE (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: f107f29d-005f-4e39-a898-17f163abb1d0
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# NAVIGATE (Entity SQL)
导航实体之间建立的关系。  
  
## 语法  
  
```  
  
navigate(instance-expresssion, [relationship-type], [to-end [, from-end] ])  
```  
  
## 参数  
 `instance-expresssion`  
 一个实体的实例。  
  
 `relationship-type`  
 关系的类型名称，取自概念架构定义语言 \(CSDL\) 文件。`relationship-type` 限定为 \<命名空间\>.\<关系类型名称\>。  
  
 `to`  
 关系的结束端。  
  
 `from`  
 关系的起始端。  
  
## 返回值  
 如果结束端的基数为 1，返回值将为 `Ref<T>`。 如果结束端的基数为 n，返回值将为 `Collection<Ref<T>>`。  
  
## 备注  
 关系是 [!INCLUDE[adonet_edm](../../../../../../includes/adonet-edm-md.md)] \(EDM\) 中的一类构造。 可以在两个或更多实体类型之间建立关系，用户可以通过关系从一端（实体）导航到另一端。 当关系中的名称解析没有歧义时，`from` 和 `to` 为有条件可选。  
  
 NAVIGATE 在 O 和 C 空间中有效。  
  
 导航构造的常规形式如下：  
  
 navigate\(`instance-expresssion`, `relationship-type`, \[ `to-end` \[, `from-end` \] \] \)  
  
 例如：  
  
```  
Select o.Id, navigate(o, OrderCustomer, Customer, Order)  
From LOB.Orders as o  
```  
  
 其中 OrderCustomer 为 `relationship`，Customer 和 Order 为关系的 `to-end`（客户）和 `from-end`（订单）。 如果 OrderCustomer 为 n:1 关系，那么导航表达式的结果类型为 Ref\<Customer\>。  
  
 此表达式的简单形式如下：  
  
```  
Select o.Id, navigate(o, OrderCustomer)  
From LOB.Orders as o  
```  
  
 同样，在以下形式的查询中，导航表达式将生成 Collection\<Ref\<Order\>\>。  
  
```  
Select c.Id, navigate(c, OrderCustomer, Order, Customer)  
From LOB.Customers as c  
```  
  
 实例表达式必须为 entity\/ref 类型。  
  
## 示例  
 下面的 Entity SQL 查询使用 NAVIGATE 运算符来导航建立在 Address 和 SalesOrderHeader 实体类型之间的关系。 此查询基于 AdventureWorks 销售模型。 若要编译并运行此查询，请执行下列步骤：  
  
1.  执行 [如何：执行返回 StructuralType 结果的查询](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md) 中的过程。  
  
2.  将以下查询作为参数传递给 `ExecuteStructuralTypeQuery` 方法：  
  
 [!code-csharp[DP EntityServices Concepts 2#NAVIGATE](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#navigate)]  
  
## 请参阅  
 [Entity SQL 参考](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [How to: Navigate Relationships with Navigate Operator](../../../../../../docs/framework/data/adonet/ef/language-reference/navigate-entity-sql.md)