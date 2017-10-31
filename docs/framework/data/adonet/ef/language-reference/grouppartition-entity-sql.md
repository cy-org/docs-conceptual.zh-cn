---
title: "GROUPPARTITION (Entity SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d0482e9b-086c-451c-9dfa-ccb024a9efb6
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# GROUPPARTITION (Entity SQL)
返回从聚合与之相关的当前组分区提取的参数值集合。`GroupPartition` 聚合是基于组的聚合，没有基于集合的形式。  
  
## 语法  
  
```  
  
GROUPPARTITION( [ALL|DISTINCT] expression )  
```  
  
## 参数  
 `expression`  
 任何 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 表达式。  
  
## 备注  
 以下查询生成产品列表以及每个产品的订单行数量的集合。  
  
```  
select p, GroupPartition(ol.Quantity) from LOB.OrderLines as ol  
  group by ol.Product as p  
```  
  
 以下两个查询在语义上是相同的：  
  
```  
select p, Sum(GroupPartition(ol.Quantity)) from LOB.OrderLines as ol  
  group by ol.Product as p  
select p, Sum(ol.Quantity) from LOB.OrderLines as ol  
  group by ol.Product as p  
```  
  
 `GROUPPARTITION` 运算符可以与用户定义的聚合函数结合使用。  
  
 `GROUPPARTITION` 是一个特殊的聚合运算符，它保留对于分组的输入集的引用。 此引用可以用在 GROUP BY 处于作用域内的查询中的任何位置。 例如，  
  
```  
select p, GroupPartition(ol.Quantity) from LOB.OrderLines as ol group by ol.Product as p  
```  
  
 使用正则 GROUP BY，分组的结果处于隐藏状态。 您只能在聚合函数中使用结果。 为了能够看到分组的结果，必须使用子查询使分组的结果与输入集相关。 下面两个查询是等效的：  
  
```  
select p, (select q from GroupPartition(ol.Quantity) as q) from LOB.OrderLines as ol group by ol.Product as p  
select p, (select ol.Quantity as q from LOB.OrderLines as ol2 where ol2.Product = p) from LOB.OrderLines as ol group by ol.Product as p  
```  
  
 如示例中所示，通过 GROUPPARTITION 聚合运算符，可以在分组后更轻松地获得对输入集的引用。  
  
 当您使用 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 参数时，GROUPPARTITION 运算符可以在运算符输入中指定任何 `expression` 表达式。  
  
 例如，下面针对组分区的所有输入表达式都是有效的：  
  
```  
select groupkey, GroupPartition(b) from {1,2,3} as a inner join {4,5,6} as b on true group by a as groupkey  
select groupkey, GroupPartition(1) from {1,2,3} as a inner join {4,5,6} as b on true group by a as groupkey  
select groupkey, GroupPartition(a + b) from {1,2,3} as a inner join {4,5,6} as b on true group by a as groupkey  
select groupkey, GroupPartition({a + b}) from {1,2,3} as a inner join {4,5,6} as b on true group by a as groupkey  
select groupkey, GroupPartition({42}) from {1,2,3} as a inner join {4,5,6} as b on true group by a as groupkey  
select groupkey, GroupPartition(b > a) from {1,2,3} as a inner join {4,5,6} as b on true group by a as groupkey  
```  
  
## 示例  
 下面的示例演示如何将 GROUPPARTITION 子句与 GROUP BY 子句一起使用。 GROUP BY 子句按照 `SalesOrderHeader` 实体的 `Contact` 对这些实体进行分组。 然后，GROUPPARTITION 子句投影每个组的 `TotalDue` 属性，而生成一个十进制值集合。  
  
 [!code-csharp[DP EntityServices Concepts 2#Collection_GroupPartition](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#collection_grouppartition)]