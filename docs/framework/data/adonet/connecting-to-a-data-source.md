---
title: "连接到 ADO.NET 中的数据源 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9abc3f92-1be3-4e1a-b360-762dc689650e
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 连接到 ADO.NET 中的数据源
在 ADO.NET 中，通过在连接字符串中提供必要的身份验证信息，使用 **Connection** 对象连接到特定的数据源。  您使用的 **Connection** 对象取决于数据源的类型。  
  
 随 .NET Framework 提供的每个 .NET Framework 数据提供程序都具有一个 <xref:System.Data.Common.DbConnection> 对象：适用于 OLE DB 的 .NET Framework 数据提供程序包括一个 <xref:System.Data.OleDb.OleDbConnection> 对象，适用于 SQL Server 的 .NET Framework 数据提供程序包括一个 <xref:System.Data.SqlClient.SqlConnection> 对象，适用于 ODBC 的 .NET Framework 数据提供程序包括一个 <xref:System.Data.Odbc.OdbcConnection> 对象，适用于 Oracle 的 .NET Framework 数据提供程序包括一个 <xref:System.Data.OracleClient.OracleConnection> 对象。  
  
## 本节内容  
 [建立连接](../../../../docs/framework/data/adonet/establishing-the-connection.md)  
 说明如何使用 **Connection** 对象建立到数据源的连接。  
  
 [连接事件](../../../../docs/framework/data/adonet/connection-events.md)  
 说明如何使用 **InfoMessage** 事件从数据源中检索信息性消息。  
  
## 请参阅  
 [连接字符串](../../../../docs/framework/data/adonet/connection-strings.md)   
 [连接池](../../../../docs/framework/data/adonet/connection-pooling.md)   
 [命令和参数](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [DataAdapter 和 DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [事务和并发](../../../../docs/framework/data/adonet/transactions-and-concurrency.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)