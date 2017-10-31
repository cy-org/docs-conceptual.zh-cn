---
title: "在 ADO.NET 中检索和修改数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 722e7f87-3691-46c6-87e8-7d159722d675
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# 在 ADO.NET 中检索和修改数据
任何数据库应用程序的一项主要功能是连接数据源并检索数据源中包含的数据。  ADO.NET 的 .NET Framework 数据提供程序充当应用程序和数据源之间的桥梁，使您可以执行命令以及使用 **DataReader** 或 **DataAdapter** 检索数据。  任何数据库应用程序的一项关键功能是更新数据库中存储的数据的能力。  在 ADO.NET 中，更新数据时会使用 **DataAdapter**、<xref:System.Data.DataSet> 和 **Command** 对象；此外，还可能会使用事务。  
  
## 本节内容  
 [连接到数据源](../../../../docs/framework/data/adonet/connecting-to-a-data-source.md)  
 说明如何建立到数据源的连接及如何使用连接事件。  
  
 [连接字符串](../../../../docs/framework/data/adonet/connection-strings.md)  
 包含说明使用连接字符串（包括连接字符串关键字、安全信息以及存储和检索连接字符串）的各个方面的主题。  
  
 [连接池](../../../../docs/framework/data/adonet/connection-pooling.md)  
 描述 .NET Framework 数据提供程序的连接池。  
  
 [命令和参数](../../../../docs/framework/data/adonet/commands-and-parameters.md)  
 包含说明如何创建命令和命令生成器、配置参数以及如何执行命令来检索和修改数据的主题。  
  
 [DataAdapter 和 DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)  
 包含说明 DataReader、DataAdapter、参数、处理 DataAdapter 事件和执行批操作的主题。  
  
 [事务和并发](../../../../docs/framework/data/adonet/transactions-and-concurrency.md)  
 包含说明如何执行本地事务、分布式事务及使用开放式并发的主题。  
  
 [检索“标识”或“自动编号”值](../../../../docs/framework/data/adonet/retrieving-identity-or-autonumber-values.md)  
 提供一个示例，该示例将为 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 表中的 **identity** 列或 Microsoft Access 表中的 **Autonumber** 字段生成的值映射到表中插入行的某一列。  讨论在 `DataTable` 中合并标识值。  
  
 [检索二进制数据](../../../../docs/framework/data/adonet/retrieving-binary-data.md)  
 介绍如何通过使用 `CommandBehavior`.`SequentialAccess` 修改 `DataReader` 的默认行为来检索二进制数据或大数据结构。  
  
 [使用存储过程修改数据](../../../../docs/framework/data/adonet/modifying-data-with-stored-procedures.md)  
 说明如何使用存储过程的输入参数和输出参数在数据库中插入行，同时返回新标识值。  
  
 [检索数据库架构信息](../../../../docs/framework/data/adonet/retrieving-database-schema-information.md)  
 说明如何获取可用数据库或编录、数据库中的表和视图、表存在的约束以及数据源中的其他架构信息。  
  
 [DbProviderFactory](../../../../docs/framework/data/adonet/dbproviderfactories.md)  
 描述提供程序工厂模型及说明如何在 `System.Data.Common` 命名空间中使用基类。  
  
 [ADO.NET 中的数据跟踪](../../../../docs/framework/data/adonet/data-tracing.md)  
 说明 ADO.NET 如何提供内置的数据跟踪功能。  
  
 [性能计数器](../../../../docs/framework/data/adonet/performance-counters.md)  
 说明 `SqlClient` 和 `OracleClient` 可用的性能计数器。  
  
 [异步编程](../../../../docs/framework/data/adonet/asynchronous-programming.md)  
 介绍了 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 对异步编程的支持。  
  
 [SqlClient 流支持](../../../../docs/framework/data/adonet/sqlclient-streaming-support.md)  
 讨论如何编写在不将其完全加载到内存的情况下从 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 流式读取数据的应用程序。  
  
## 请参阅  
 [ADO.NET 中的数据类型映射](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md)   
 [DataSet、DataTable 和 DataView](../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [保证 ADO.NET 应用程序的安全](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [SQL Server 和 ADO.NET](../../../../docs/framework/data/adonet/sql/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)