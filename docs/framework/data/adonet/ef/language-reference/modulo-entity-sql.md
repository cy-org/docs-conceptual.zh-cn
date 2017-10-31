---
title: "（取模）（实体 SQL） | Microsoft Docs"
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
ms.assetid: 243ddc4f-3c4e-41e1-a3ef-4ed39e36248b
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# （取模）（实体 SQL）
返回两个表达式相除后的余数。  
  
## 语法  
  
```  
  
dividend  
%  
divisor  
  
```  
  
## 参数  
 `dividend`  
 被除数的数值表达式。`dividend` 为任何一种数值数据类型的任何有效表达式。  
  
 `divisor`  
 除数的数值表达式。`divisor` 为任何一种数值数据类型的任何有效表达式。  
  
## 结果类型  
 Edm.Int32  
  
## 示例  
 以下 Entity SQL 查询使用 % 算数运算符以返回两个表达式相除后的余数。 此查询基于 AdventureWorks 销售模型。 若要编译并运行此查询，请执行下列步骤：  
  
1.  执行 [如何：执行返回 StructuralType 结果的查询](../../../../../../docs/framework/data/adonet/ef/how-to-execute-a-query-that-returns-structuraltype-results.md) 中的过程。  
  
2.  将以下查询作为参数传递给 `ExecuteStructuralTypeQuery` 方法：  
  
 [!code-csharp[DP EntityServices Concepts 2#MODULO](../../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts 2/cs/entitysql.cs#modulo)]  
  
## 请参阅  
 [Entity SQL 参考](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)