---
title: "ADO.NET 技术选项和指南 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c8577281-38e6-4ce5-b036-572039a4c3d8
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# ADO.NET 技术选项和指南
ADO.NET 数据平台是一种多版本策略，通过使开发人员能够针对概念性实体数据模型进行编程，减少其所需的编码和维护工作量。  此平台包括 ADO.NET 实体框架和相关技术。  
  
## Entity Framework  
 ADO.NET 实体框架专门用于让开发人员能够通过针对概念应用程序模型进行编程（而不是直接针对关系存储架构进行编程）来创建数据访问应用程序。  这样做的目的是减少面向数据的应用程序所需的编码和维护工作。  有关详细信息，请参阅[ADO.NET 实体框架](../../../../docs/framework/data/adonet/ef/index.md)。  
  
### 实体数据模型 \(EDM\)  
 实体数据模型 \(EDM\) 是一种将应用程序数据定义为多组实体和关系的设计规范。  此模型中的数据支持跨应用程序边界的数据关系映射和数据可编程性。  
  
### Object Services — 对象服务  
 对象服务允许程序员通过一组公共语言运行库 \(CLR\) 类与概念模型进行交互。  这些类既可以从概念模型自动生成，也可以单独开发以反映概念模型的结构。  对象服务还为实体框架提供基础结构支持，包括状态管理、更改跟踪、标识解析、加载和导航关系、将对象更改传播到数据库修改和实体 SQL 查询生成支持等服务。  有关详细信息，请参阅[Object Services Overview \(Entity Framework\)](http://msdn.microsoft.com/zh-cn/43014cf9-c9cb-4538-bfbb-197820b60038)。  
  
### LINQ to Entities  
 LINQ to Entities 是一种语言集成查询 \(LINQ\) 实现，它允许开发人员通过使用 LINQ 表达式和 LINQ 标准查询运算符，根据实体框架对象上下文创建强类型查询。  LINQ to Entities 使开发人员能够针对一个概念模型开展工作，在此模型中，可在 Microsoft SQL Server 和第三方数据库之间非常灵活地进行对象关系映射。  有关详细信息，请参阅[LINQ to Entities](../../../../docs/framework/data/adonet/ef/language-reference/linq-to-entities.md)。  
  
### Entity SQL  
 实体 SQL 是一种基于文本的查询语言，专门用于与实体数据模型进行交互。  实体 SQL 是一种 SQL 变体，其中包含针对更高级别的建模概念的查询构造，例如继承、复杂类型和显式关系。  开发人员也可以直接将实体 SQL 与对象服务一起使用。  有关详细信息，请参阅[Entity SQL 语言](../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-language.md)。  
  
### EntityClient  
 EntityClient 是一种用于与实体数据模型交互的新的 .NET Framework 数据提供程序。  EntityClient 遵循 .NET Framework 数据提供程序模式，公开可返回 <xref:System.Data.EntityClient.EntityDataReader> 的 <xref:System.Data.EntityClient.EntityConnection> 对象和 <xref:System.Data.EntityClient.EntityCommand> 对象。  EntityClient 与实体 SQL 语言一起使用，可提供与特定于存储的数据提供程序的灵活映射。  有关详细信息，请参阅[EntityClient and Entity SQL](http://msdn.microsoft.com/zh-cn/49202ab9-ac98-4b4b-a05c-140e422bf527)。  
  
### 实体数据模型工具  
 实体框架提供了命令行工具、向导和设计器来帮助生成 EDM 应用程序。  EntityDataSource 控件支持基于 EDM 的数据绑定方案。  EntityDataSource 控件的编程接口与 Visual Studio 中的其他数据源控件类似。  有关详细信息，请参阅[ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/zh-cn/91076853-0881-421b-837a-f582f36be527)。  
  
## LINQ to SQL  
 LINQ to SQL 是一种对象关系映射 \(OR\/M\) 实现，它使您能够使用 .NET Framework 类为 SQL Server 数据建模。  LINQ to SQL 允许您使用 LINQ 来查询数据库，以及在数据库中更新、插入和删除数据。  LINQ to SQL 支持事务、视图和存储过程，因此可以方便地将数据验证和业务逻辑规则集成到数据模型中。  您可以使用对象关系设计器（O\/R 设计器），为基于数据库中对象的实体类和关联建模。  有关详细信息，请参阅[LINQ to SQL 工具在 Visual Studio 中](../Topic/LINQ%20to%20SQL%20Tools%20in%20Visual%20Studio2.md)。  
  
## WCF 数据服务  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 可在 Web 或 Intranet 上部署数据服务。  这些数据将按照实体数据模型的规范组织成不同的实体和关系。  在此模型上部署的数据可通过标准的 HTTP 协议进行寻址。  有关详细信息，请参阅[WCF 数据服务 4.5](../../../../docs/framework/data/wcf/index.md)。  
  
## 请参阅  
 [ADO.NET 概述](../../../../docs/framework/data/adonet/ado-net-overview.md)   
 [ADO.NET 中的新增功能](../../../../docs/framework/data/adonet/whats-new.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)