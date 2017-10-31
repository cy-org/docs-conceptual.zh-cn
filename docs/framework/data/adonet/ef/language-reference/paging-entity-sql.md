---
title: "分页 (Entity SQL) | Microsoft Docs"
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
ms.assetid: ba4f334d-03e5-4a7b-9d42-628f4639b9a2
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 分页 (Entity SQL)
可以通过在 [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md) 子句中使用 [SKIP](../../../../../../docs/framework/data/adonet/ef/language-reference/skip-entity-sql.md) 和 [LIMIT](../../../../../../docs/framework/data/adonet/ef/language-reference/limit-entity-sql.md) 子子句执行物理分页。  若要以确定的方式执行物理分页，应使用 SKIP 和 LIMIT。  如果您只是希望以非确定的方式限制结果中的行数，则应使用 [TOP](../../../../../../docs/framework/data/adonet/ef/language-reference/top-entity-sql.md)。  TOP 和 SKIP\/LIMIT 是互斥的。  
  
## TOP 概述  
 SELECT 子句可以在可选的 ALL\/DISTINCT 修饰符之后具有可选的 TOP 子子句。  TOP 子子句指定查询结果中将只返回第一组行。  有关更多信息，请参见 [TOP](../../../../../../docs/framework/data/adonet/ef/language-reference/top-entity-sql.md)。  
  
## SKIP 和 LIMIT 概述  
 SKIP 和 LIMIT 是 ORDER BY 子句的组成部分。  如果 ORDER BY 子句中存在 SKIP 表达式子子句，则将根据排序规范对结果排序，结果集将包含从紧接着 SKIP 表达式之后的下一行开始的行。  例如，SKIP 5 将跳过前五行，并返回第六行以及后续行。  如果 ORDER BY 子句中存在 LIMIT 表达式子子句，则将根据排序规范对查询排序，并且结果行数将受到 LIMIT 表达式限制。  例如，LIMIT 5 将结果集限制为五个实例或行。  SKIP 和 LIMIT 不必一起使用，可以只将 SKIP 或 LIMIT 用于 ORDER BY 子句。  有关详细信息，请参阅下列主题：  
  
-   [SKIP](../../../../../../docs/framework/data/adonet/ef/language-reference/skip-entity-sql.md)  
  
-   [LIMIT](../../../../../../docs/framework/data/adonet/ef/language-reference/limit-entity-sql.md)  
  
-   [ORDER BY](../../../../../../docs/framework/data/adonet/ef/language-reference/order-by-entity-sql.md)  
  
## 请参阅  
 [Entity SQL 参考](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [Entity SQL 概述](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)   
 [How to: Page Through Query Results](http://msdn.microsoft.com/zh-cn/ffc0f920-e7de-42e0-9b12-ef356421d030)