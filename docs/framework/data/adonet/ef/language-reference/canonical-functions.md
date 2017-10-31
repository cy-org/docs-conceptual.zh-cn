---
title: "规范函数 | Microsoft Docs"
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
ms.assetid: bbcc9928-36ea-4dff-9e31-96549ffed958
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 规范函数
本节讨论所有数据提供程序支持的并可由所有查询技术使用的规范函数。  规范函数不能由提供程序扩展。  
  
 这些规范函数将转换为提供程序的相应数据源功能。  这样，就可以用一种在不同数据源间通用的形式表示函数调用。  
  
 因为这些规范函数独立于数据源，所以会按概念模型中的类型来定义规范函数的参数和返回类型。  但某些数据源可能不支持概念模型中的所有类型。  
  
 当在 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查询中使用规范函数时，将在数据源中调用适当的函数。  
  
 所有规范函数都同时显式指定 null 输入行为和错误条件。  存储提供程序应遵循此行为，但 [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] 不强制执行此行为。  
  
 对于 LINQ 方案，对 [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] 所执行的查询涉及将 CLR 方法映射到基础数据源中的方法。  CLR 方法映射到规范函数，这样，无论数据源如何，特定的方法集都会正确映射。  
  
## 规范函数命名空间  
 规范函数的命名空间是 <xref:System.Data.Metadata.Edm>。  <xref:System.Data.Metadata.Edm> 命名空间自动包含在所有查询中。  但如果导入的另一个命名空间包含与规范函数（在 <xref:System.Data.Metadata.Edm> 命名空间中）同名的函数，则必须指定命名空间。  
  
## 本节内容  
 [聚合规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/aggregate-canonical-functions.md)  
 讨论 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 聚合规范函数。  
  
 [数学规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/math-canonical-functions.md)  
 讨论 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 数学规范函数。  
  
 [字符串规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/string-canonical-functions.md)  
 讨论 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 字符串规范函数。  
  
 [日期和时间规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/date-and-time-canonical-functions.md)  
 讨论 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 日期和时间规范函数。  
  
 [按位规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/bitwise-canonical-functions.md)  
 讨论 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 按位规范函数。  
  
 [空间函数](../../../../../../docs/framework/data/adonet/ef/language-reference/spatial-functions.md)  
 讨论空间 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 规范函数。  
  
 [其他规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/other-canonical-functions.md)  
 讨论未分类为按位、日期\/时间、字符串、数字或聚合函数的函数。  
  
## 请参阅  
 [Entity SQL 概述](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)   
 [Entity SQL 参考](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [概念模型规范函数到 SQL Server 函数映射](../../../../../../docs/framework/data/adonet/ef/conceptual-model-canonical-to-sql-server-functions-mapping.md)   
 [用户定义的函数](../../../../../../docs/framework/data/adonet/ef/language-reference/user-defined-functions-entity-sql.md)