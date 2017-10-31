---
title: "检索数据库架构信息 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 79038d52-f122-4fd4-9bfb-aaa22d6a114b
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 检索数据库架构信息
从数据库获取架构信息通过架构发现过程来完成。  通过架构发现，应用程序可以请求托管提供程序查找并返回有关给定数据库的数据库架构（也称为*元数据*）名称的信息。  不同的数据库架构元素（例如表、列和存储过程）通过架构集合进行公开。  每个架构集合包含所使用的提供程序特定的各种架构信息。  
  
 每个 .NET Framework 托管提供程序实现 **Connection** 类中的 **GetSchema** 方法，从 **GetSchema** 方法返回的架构信息采用 <xref:System.Data.DataTable> 的形式。  **GetSchema** 方法属于重载方法，提供可选的参数来指定要返回的架构集合以及限制返回的信息量。  
  
 适用于 OLE DB、ODBC、Oracle 和 SqlClient 的 .NET Framework 数据提供程序提供了一种返回描述 **DataReader** 的列元数据的 **GetSchemaTable** 方法。  
  
 适用于 OLE DB 的 .NET Framework 数据提供程序还使用 <xref:System.Data.OleDb.OleDbConnection> 对象的 <xref:System.Data.OleDb.OleDbConnection.GetOleDbSchemaTable%2A> 方法来公开架构信息。  **GetOleDbSchemaTable** 将 <xref:System.Data.OleDb.OleDbSchemaGuid>（标识要返回的架构信息）和对返回列的限制数组用作参数。  **GetOleDbSchemaTable** 返回已填充所请求架构信息的 <xref:System.Data.DataTable>。  
  
## 本节内容  
 [GetSchema 和架构集合](../../../../docs/framework/data/adonet/getschema-and-schema-collections.md)  
 描述 **GetSchema** 方法以及如何使用该方法从数据库检索和限制架构信息。  
  
 架构限制  
 描述可用于 **GetSchema** 的架构限制。  
  
 [通用架构集合](../../../../docs/framework/data/adonet/common-schema-collections.md)  
 描述所有 .NET Framework 托管提供程序均支持的所有通用架构集合。  
  
 [SQL Server 架构集合](../../../../docs/framework/data/adonet/sql-server-schema-collections.md)  
 描述适用于 SQL Server 的 .NET Framework 提供程序支持的架构集合。  
  
 [Oracle 架构集合](../../../../docs/framework/data/adonet/oracle-schema-collections.md)  
 描述适用于 Oracle 的 SQL Server .NET Framework 提供程序支持的架构集合。  
  
 [ODBC 架构集合](../../../../docs/framework/data/adonet/odbc-schema-collections.md)  
 描述 ODBC 驱动程序的架构集合。  
  
 [OLE DB 架构集合](../../../../docs/framework/data/adonet/ole-db-schema-collections.md)  
 描述 OLE DB 提供程序的架构集合。  
  
## 参考  
 <xref:System.Data.Common.DbConnection.GetSchema%2A>  
 描述 <xref:System.Data.Common.DbConnection> 类的 **GetSchema** 方法。  
  
 <xref:System.Data.Odbc.OdbcConnection.GetSchema%2A>  
 描述 <xref:System.Data.Odbc.OdbcConnection> 类的 **GetSchema** 方法。  
  
 <xref:System.Data.OleDb.OleDbConnection.GetSchema%2A>  
 描述 <xref:System.Data.OleDb.OleDbConnection> 类的 **GetSchema** 方法。  
  
 <xref:System.Data.OracleClient.OracleConnection.GetSchema%2A>  
 描述 <xref:System.Data.OracleClient.OracleConnection> 类的 **GetSchema** 方法。  
  
 <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A>  
 描述 <xref:System.Data.SqlClient.SqlConnection> 类的 **GetSchema** 方法。  
  
 <xref:System.Data.Common.DbDataReader.GetSchemaTable%2A>  
 描述 <xref:System.Data.Common.DbDataReader> 类的 **GetSchemaTable** 方法。  
  
 <xref:System.Data.Odbc.OdbcDataReader.GetSchemaTable%2A>  
 描述 <xref:System.Data.Odbc.OdbcDataReader> 类的 **GetSchemaTable** 方法。  
  
 <xref:System.Data.OleDb.OleDbDataReader.GetSchemaTable%2A>  
 描述 <xref:System.Data.OleDb.OleDbDataReader> 类的 **GetSchemaTable** 方法。  
  
 <xref:System.Data.OracleClient.OracleDataReader.GetSchemaTable%2A>  
 描述 <xref:System.Data.OracleClient.OracleDataReader> 类的 **GetSchemaTable** 方法。  
  
 <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>  
 描述 <xref:System.Data.SqlClient.SqlDataReader> 类的 **GetSchemaTable** 方法。  
  
## 请参阅  
 [在 ADO.NET 中检索和修改数据](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)