---
title: "示例提供程序中的 SQL 生成 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e70f553d-4622-4627-928e-1aa2ee605d8e
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 示例提供程序中的 SQL 生成
[实体框架示例提供程序](http://go.microsoft.com/fwlink/?LinkId=180616)（可能为英文网页）演示支持 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] 的 ADO.NET 数据提供程序的新组件。  它使用 SQL Server 2005 数据库，并实现为 System.Data.SqlClient ADO.NET 2.0 数据提供程序的一个包装。  
  
 该示例提供程序的 SQL 生成模块（位于 SQL Generation 文件夹下，不包括 DmlSqlGenerator.cs 文件）采用一个输入 DbQueryCommandTree，并且生成单个 SQL SELECT 语句。  
  
## 本节内容  
 本节包括下列主题：  
  
 [体系结构和设计](../../../../../docs/framework/data/adonet/ef/architecture-and-design.md)  
  
 [演练：SQL 生成](../../../../../docs/framework/data/adonet/ef/walkthrough-sql-generation.md)  
  
## 请参阅  
 [SQL 生成](../../../../../docs/framework/data/adonet/ef/sql-generation.md)