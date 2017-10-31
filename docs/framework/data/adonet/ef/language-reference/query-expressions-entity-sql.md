---
title: "查询表达式 (Entity SQL) | Microsoft Docs"
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
ms.assetid: c36f327b-e230-48d4-bbd5-78dc6478c447
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 查询表达式 (Entity SQL)
查询表达式将许多不同的查询运算符组合成单个语法。  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 提供了不同类型的表达式，包括：[文本](../../../../../../docs/framework/data/adonet/ef/language-reference/literals-entity-sql.md)、[参数](../../../../../../docs/framework/data/adonet/ef/language-reference/parameters-entity-sql.md)、[变量](../../../../../../docs/framework/data/adonet/ef/language-reference/variables-entity-sql.md)、运算符、[函数](../../../../../../docs/framework/data/adonet/ef/language-reference/functions-entity-sql.md)、集运算符等等。  有关详细信息，请参阅[Entity SQL 参考](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)。  
  
## 子句  
 查询表达式由一系列子句组成，这些子句将连续的操作应用于一个对象集合。  它们基于可在标准 SQL 选择语句中找到的相同子句：[SELECT](../../../../../../docs/framework/data/adonet/ef/language-reference/select-entity-sql.md)、[FROM](../../../../../../docs/framework/data/adonet/ef/language-reference/from-entity-sql.md)、[WHERE](../../../../../../docs/framework/data/adonet/ef/language-reference/where-entity-sql.md)、[GROUP BY](../../../../../../docs/framework/data/adonet/ef/language-reference/group-by-entity-sql.md)、[HAVING](../../../../../../docs/framework/data/adonet/ef/language-reference/having-entity-sql.md) 和 [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md)。  
  
## 范围  
 在 FROM 子句中定义的名称以从左到右的出现顺序引入到 FROM 作用域。  在 JOIN 列表中，表达式可以引用以前在列表中定义的名称。  在 FROM 子句中标识的元素的公共属性不添加到 FROM 作用域：始终必须通过别名限定名称来引用这些属性。  通常，SELECT 表达式的所有部分都视作在 FROM 作用域内。  
  
## 请参阅  
 [Entity SQL 参考](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)