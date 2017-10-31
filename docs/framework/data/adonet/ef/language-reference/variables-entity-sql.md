---
title: "变量 (Entity SQL) | Microsoft Docs"
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
  - "ESQL"
ms.assetid: 3eed222a-f8f6-46b6-9cd5-220cc0e4e5d8
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 变量 (Entity SQL)
## 变量  
 变量表达式是对当前作用域中定义的命名表达式的引用。  变量引用必须是有效的 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 标识符，如[标识符](../../../../../../docs/framework/data/adonet/ef/language-reference/identifiers-entity-sql.md) 中的定义。  
  
 以下示例演示如何在表达式中使用变量。  FROM 子句中的 `c` 是变量定义。  在 SELECT 子句中使用的 `c` 表示变量引用。  
  
```  
select c   
from LOB.customers as c  
```  
  
## 请参阅  
 [标识符](../../../../../../docs/framework/data/adonet/ef/language-reference/identifiers-entity-sql.md)   
 [参数](../../../../../../docs/framework/data/adonet/ef/language-reference/parameters-entity-sql.md)   
 [Entity SQL 概述](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)