---
title: "编写嵌套 Entity SQL 查询 | Microsoft Docs"
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
ms.assetid: 685d4cd3-2c1f-419f-bb46-c9d97a351eeb
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 编写嵌套 Entity SQL 查询
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 是一种功能丰富的语言。  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 的构造块是一个表达式。  与传统的 SQL 不同，[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 并不仅限于表格结果集：[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 支持编写可以包含文本、参数或嵌套表达式的复杂表达式。  表达式中的值可以参数化，或者也可以由其他表达式构成。  
  
## 嵌套表达式  
 嵌套表达式可以放置在任何可接受其返回类型值的位置。  例如：  
  
```  
-- Returns a hierarchical collection of three elements at top-level.   
-- x must be passed in the parameter collection.  
ROW(@x, {@x}, {@x, 4, 5}, {@x, 7, 8, 9})  
  
-- Returns a hierarchical collection of one element at top-level.  
-- x must be passed in the parameter collection.  
{{{@x}}};  
```  
  
 嵌套查询可以放在投影子句中。  例如：  
  
```  
-- Returns a collection of rows where each row contains an Address entity.  
-- and a collection of references to its corresponding SalesOrderHeader entities.  
SELECT address, (SELECT DEREF(soh)   
                    FROM NAVIGATE(address, AdventureWorksModel.FK_SalesOrderHeader_Address_BillToAddressID) AS soh)   
                    AS salesOrderHeader FROM AdventureWorksEntities.Address AS address  
```  
  
 在 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 中，嵌套查询必须括在括号中：  
  
```  
-- Pseudo-Entity SQL  
( SELECT …  
FROM … )  
UNION ALL  
( SELECT …  
FROM … );  
```  
  
 下面的示例演示如何在 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 中正确嵌套表达式：[How to: Order the Union of Two Queries](http://msdn.microsoft.com/zh-cn/853c583a-eaba-4400-830d-be974e735313)。  
  
## 投影中的嵌套查询  
 投影子句中的嵌套查询可在服务器上转换为笛卡尔积查询。  在某些后端服务器（包括 SLQ Server）中，这会导致 TempDB 表变得过大，对服务器性能产生负面影响。  
  
 以下是这种查询的一个示例：  
  
```  
SELECT c, (SELECT c, (SELECT c FROM AdventureWorksModel.Vendor AS c  ) As Inner2 FROM AdventureWorksModel.JobCandidate AS c  ) As Inner1 FROM AdventureWorksModel.EmployeeDepartmentHistory AS c  
```  
  
## 嵌套查询排序  
 在实体框架中，嵌套表达式可置于查询中的任何位置。  Entity SQL 为编写查询提供了非常大的灵活性，可以在编写的查询中包含对嵌套查询的排序。  但是，将不保留嵌套查询的顺序。  
  
```  
-- The following query will order the results by last name.  
SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorksModel.Contact as C1  
        ORDER BY C1.LastName  
```  
  
```  
-- In the following query, ordering of the nested query is ignored.  
SELECT C2.FirstName, C2.LastName  
    FROM (SELECT C1.FirstName, C1.LastName  
        FROM AdventureWorksModel.Contact as C1  
        ORDER BY C1.LastName) as C2  
```  
  
## 请参阅  
 [Entity SQL 概述](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)