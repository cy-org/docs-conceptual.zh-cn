---
title: "查询计划缓存 (Entity SQL) | Microsoft Docs"
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
ms.assetid: 90b0c685-5ef2-461b-98b4-c3c0a2b253c7
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 查询计划缓存 (Entity SQL)
每当试图执行查询时，查询管道都会查找它的查询计划缓存，以便了解该查询是否已经编译且可用。  如果答案是肯定的，它将重用缓存的计划而不是生成新的计划。  如果未在查询计划缓存中找到匹配的计划，则会编译和缓存该查询。  查询由其 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 文本和参数集合（名称和类型）标识。  所有文本比较都区分大小写。  
  
## 配置  
 可以通过 <xref:System.Data.EntityClient.EntityCommand> 配置查询计划缓存。  
  
 若要通过 <xref:System.Data.EntityClient.EntityCommand.EnablePlanCaching%2A?displayProperty=fullName> 启用或禁用查询计划缓存，请将此属性设置为 `true` 或 `false`。  为单个不太可能使用一次以上的动态查询禁用计划缓存可以改进性能。  
  
 可以通过 <xref:System.Data.Objects.ObjectQuery.EnablePlanCaching%2A> 启用查询计划缓存。  
  
## 推荐的做法  
 一般来说，应该避免使用动态查询。  下面的动态查询示例容易受到 SQL 注入式攻击，因为该示例在不进行任何验证的情况下直接获取用户输入。  
  
 `"SELECT sp.SalesYTD FROM AdventureWorksEntities.SalesPerson as sp WHERE sp.EmployeeID = " + employeeTextBox.Text;`  
  
 如果您确实要使用动态生成的查询，请考虑禁用查询计划缓存，从而避免不必要地将内存用于不太可能重复使用的缓存项。  
  
 静态查询和参数化查询的查询计划缓存可以提供性能方面的好处。  下面是一个静态查询示例：  
  
```  
"SELECT sp.SalesYTD FROM AdventureWorksEntities.SalesPerson as sp";  
```  
  
 为了通过查询计划缓存正确匹配查询，查询应该遵守以下要求：  
  
-   查询文本应该具有常量模式，最好是常量字符串或资源。  
  
-   每当必须传递用户提供的值时，都应该使用 <xref:System.Data.EntityClient.EntityParameter> 或 <xref:System.Data.Objects.ObjectParameter>。  
  
 应该避免以下查询模式，这种模式不必要地消耗查询计划缓存中的存储槽：  
  
-   对文本中字母大小写的更改。  
  
-   对空格的更改。  
  
-   对字面值的更改。  
  
-   对注释内部文本的更改。  
  
## 请参阅  
 [Entity SQL 概述](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)