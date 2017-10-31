---
title: "类型系统 (Entity SQL) | Microsoft Docs"
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
ms.assetid: 818a505b-a196-41dd-aaac-2ccd5f7a2f1a
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 类型系统 (Entity SQL)
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 支持下面一些类型：  
  
-   基元（简单）类型，如 `Int32` 和 `String`。  
  
-   在架构中定义的名义类型，如 <xref:System.Data.Metadata.Edm.EntityType>、<xref:System.Data.Metadata.Edm.ComplexType> 和 <xref:System.Data.Metadata.Edm.RelationshipType>。  
  
-   架构中未显式定义的匿名类型：<xref:System.Data.Metadata.Edm.CollectionType>、<xref:System.Data.Metadata.Edm.RowType> 和 <xref:System.Data.Metadata.Edm.RefType>。  
  
 本节讨论在架构中未显式定义但受 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 支持的匿名类型。  有关基元类型和名义类型的信息，请参见 [Conceptual Model Types \(CSDL\)](http://msdn.microsoft.com/zh-cn/987b995f-e429-4569-9559-b4146744def4)。  
  
## 行  
 行的结构取决于该行所包含的类型化以命名成员的序列。  行类型没有标识，不能被继承。  如果同一行类型的实例的成员分别等效，则这些实例是等效的。  行不具有超出其结构等效项的行为，在公共语言运行库中没有等效项。  查询可产生包含行或行的集合的结构。  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 查询和主机语言之间的 API 绑定定义行在产生结果的查询中的实现方式。  有关如何构造行实例的信息，请参见[构造类型](../../../../../../docs/framework/data/adonet/ef/language-reference/constructing-types-entity-sql.md)。  
  
## 集合  
 集合类型表示其他对象的零个或零个以上的实例。  有关如何构造集合的信息，请参见[构造类型](../../../../../../docs/framework/data/adonet/ef/language-reference/constructing-types-entity-sql.md)。  
  
## 参考资料  
 引用是指向特定实体集中的特定实体的逻辑指针。  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 支持使用以下运算符对引用进行构造、解构和导航：  
  
-   [REF](../../../../../../docs/framework/data/adonet/ef/language-reference/ref-entity-sql.md)  
  
-   [CREATEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/createref-entity-sql.md)  
  
-   [KEY](../../../../../../docs/framework/data/adonet/ef/language-reference/key-entity-sql.md)  
  
-   [DEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/deref-entity-sql.md)  
  
 可以使用成员访问（点）运算符 \(`.`\) 对引用进行导航。  下面的代码段通过对 r（引用）属性进行导航提取 Order 的 Id 属性。  
  
```  
select o2.r.Id   
from (select ref(o) as r from LOB.Orders as o) as o2   
```  
  
 如果引用值为 null，或引用的目标不存在，则结果为 null。  
  
## 请参阅  
 [Entity SQL 概述](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)   
 [Entity SQL 参考](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [CAST](../../../../../../docs/framework/data/adonet/ef/language-reference/cast-entity-sql.md)   
 [CSDL、SSDL 和 MSL 规范](../../../../../../docs/framework/data/adonet/ef/language-reference/csdl-ssdl-and-msl-specifications.md)