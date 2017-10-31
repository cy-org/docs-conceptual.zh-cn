---
title: "ADO.NET 概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ee3bc1d8-11db-4be4-89eb-c708cf04117d
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# ADO.NET 概述
ADO.NET 提供对诸如 SQL Server 和 XML 这样的数据源以及通过 OLE DB 和 ODBC 公开的数据源的一致访问。  共享数据的使用方应用程序可以使用 ADO.NET 连接到这些数据源，并可以检索、处理和更新其中包含的数据。  
  
 ADO.NET 通过数据处理将数据访问分解为多个可以单独使用或一前一后使用的不连续组件。  ADO.NET 包含用于连接到数据库、执行命令和检索结果的 .NET Framework 数据提供程序。  这些结果或者被直接处理，放在 ADO.NET <xref:System.Data.DataSet> 对象中以便以特别的方式向用户公开，并与来自多个源的数据组合；或者在层之间传递。  `DataSet` 对象也可以独立于 .NET Framework 数据提供程序，用于管理应用程序本地的数据或源自 XML 的数据。  
  
 ADO.NET 类位于 System.Data.dll 中，并与 System.Xml.dll 中的 XML 类集成。  有关连接到数据库，从数据库检索数据，然后在控制台窗口中显示该数据的示例代码，请参见 [ADO.NET 代码示例](../../../../docs/framework/data/adonet/ado-net-code-examples.md)。  
  
 ADO.NET 向编写托管代码的开发人员提供类似于 ActiveX 数据对象 \(ADO\) 向本机组件对象模型 \(COM\) 开发人员提供的功能。  建议您在 .NET 应用程序中使用 ADO.NET 而不使用 ADO 来访问数据。  
  
 ADO.NET 在 .NET Framework 中提供最直接的数据访问方法。  有关允许应用程序针对概念模型而不是基础存储模型运行的更高级别抽象，请参见 [ADO.NET 实体框架](../../../../docs/framework/data/adonet/ef/index.md)。  
  
 **隐私声明**：System.Data.dll、System.Data.Design.dll、System.Data.OracleClient.dll、System.Data.SqlXml.dll、System.Data.Linq.dll、System.Data.SqlServerCe.dll 和 System.Data.DataSetExtensions.dll 程序集不区分用户的隐私数据和非隐私数据。  这些程序集不收集、存储或传输任何用户隐私数据。  不过，第三方应用程序可能会使用这些程序集收集、存储或传输用户的隐私数据。  
  
## 本节内容  
 [ADO.NET 结构](../../../../docs/framework/data/adonet/ado-net-architecture.md)  
 提供 ADO.NET 结构和组件的概述。  
  
 [ADO.NET 技术选项和指南](../../../../docs/framework/data/adonet/ado-net-technology-options-and-guidelines.md)  
 描述实体数据平台附带的产品和技术。  
  
 [LINQ 和 ADO.NET](../../../../docs/framework/data/adonet/linq-and-ado-net.md)  
 描述如何在 ADO.NET 中实现语言集成查询 \(LINQ\) 并提供指向相关主题的链接。  
  
 [.NET Framework 数据提供程序](../../../../docs/framework/data/adonet/data-providers.md)  
 提供有关 .NET Framework 数据提供程序的设计的概述以及有关随 ADO.NET 提供的 .NET Framework 数据提供程序的概述。  
  
 [ADO.NET DataSet](../../../../docs/framework/data/adonet/ado-net-datasets.md)  
 提供有关 `DataSet` 设计和组件的概述。  
  
 [在 ADO.NET 中并行执行](../../../../docs/framework/data/adonet/side-by-side-execution.md)  
 讨论 ADO.NET 各个版本之间的区别及其对并行执行和应用程序兼容性的影响。  
  
 [ADO.NET 代码示例](../../../../docs/framework/data/adonet/ado-net-code-examples.md)  
 提供使用 ADO.NET 数据提供程序检索数据的代码示例。  
  
## 相关章节  
 [ADO.NET 中的新增功能](../../../../docs/framework/data/adonet/whats-new.md)  
 介绍 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 中的新功能。  
  
 [保证 ADO.NET 应用程序的安全](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)  
 描述使用 ADO.NET 时的安全编码做法。  
  
 [ADO.NET 中的数据类型映射](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md)  
 描述 .NET Framework 数据类型与 .NET Framework 数据提供程序之间的数据类型映射。  
  
 [在 ADO.NET 中检索和修改数据](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)  
 说明如何连接到数据源、检索数据和修改数据。  这包括 `DataReaders` 和 `DataAdapters`。  
  
## 请参阅  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)   
 [在 Visual Studio 中访问数据](../Topic/Accessing%20data%20in%20Visual%20Studio.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)