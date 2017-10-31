---
title: "不支持的表达式 (Entity SQL) | Microsoft Docs"
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
ms.assetid: 5e79da7e-e78a-413c-8fb0-f3f9cd84f579
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 不支持的表达式 (Entity SQL)
本主题介绍 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 中不支持的 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)]。有关更多信息，请参见[Entity SQL 与 Transact\-SQL 的区别](../../../../../../docs/framework/data/adonet/ef/language-reference/how-entity-sql-differs-from-transact-sql.md)。  
  
## 限定谓词  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] 允许以下形式的构造：  
  
```  
sal > all (select salary from employees)  
sal > any (select salary from employees)  
```  
  
 但 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 不支持此这样的构造。  在 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 中的等效表达式可以写为如下形式：  
  
```  
not exists(select 0 from employees as e where sal > e.salary)  
exists(select 0 from employees as e where sal > e.salary)  
```  
  
## \* 运算符  
 [!INCLUDE[tsql](../../../../../../includes/tsql-md.md)] 支持在 SELECT 子句中使用 \* 运算符来表示应提取出所有列。  在 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 中不支持使用此运算符。  
  
## 请参阅  
 [Entity SQL 概述](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)   
 [Entity SQL 与 Transact\-SQL 的区别](../../../../../../docs/framework/data/adonet/ef/language-reference/how-entity-sql-differs-from-transact-sql.md)