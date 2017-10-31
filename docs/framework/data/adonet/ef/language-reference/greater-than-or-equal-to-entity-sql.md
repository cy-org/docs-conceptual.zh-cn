---
title: "&gt;=（大于或等于）(Entity SQL) | Microsoft Docs"
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
ms.assetid: 70780ac4-0123-4da8-b731-8af856daffe3
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# &gt;=（大于或等于）(Entity SQL)
比较两个表达式以确定左侧表达式的值是否大于或等于右侧表达式的值。  
  
## 语法  
  
```  
  
expression  
>=  
expression  
  
```  
  
## 参数  
 `expression`  
 任何有效表达式。 两个表达式都必须具有可隐式转换的数据类型。  
  
## 结果类型  
 如果左侧表达式的值大于或等于右侧表达式的值，则为 `true`；否则为 `false`。  
  
## 示例  
 下面的 Entity SQL 查询使用 \>\= 比较运算符比较两个表达式，以确定左侧表达式的值是否大于或等于右侧表达式的值。 此查询基于 AdventureWorks 销售模型。 若要编译并运行此查询，请执行下列步骤：  
  
1.  执行 [如何：执行返回 StructuralType 结果的查询](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md) 中的过程。  
  
2.  将以下查询作为参数传递给 `ExecuteStructuralTypeQuery` 方法：  
  
 [!code-csharp[DP EntityServices Concepts 2#GREATER_OR_EQUALS](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#greater_or_equals)]  
  
## 请参阅  
 [Entity SQL 参考](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)