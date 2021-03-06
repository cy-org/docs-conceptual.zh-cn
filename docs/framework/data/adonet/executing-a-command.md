---
title: "执行命令 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 40494916-c25a-4cb8-8f7c-fcb8d378464e
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 执行命令
包含在 .NET Framework 中的每个 .NET Framework 数据提供程序都拥有自己的继承自 <xref:System.Data.Common.DbCommand> 的命令对象。  适用于 OLE DB 的 .NET Framework 数据提供程序包括一个 <xref:System.Data.OleDb.OleDbCommand> 对象，适用于 SQL Server 的 .NET Framework 数据提供程序包括一个 <xref:System.Data.SqlClient.SqlCommand> 对象，适用于 ODBC 的 .NET Framework 数据提供程序包括一个 <xref:System.Data.Odbc.OdbcCommand> 对象，适用于 Oracle 的 .NET Framework 数据提供程序包括一个 <xref:System.Data.OracleClient.OracleCommand> 对象。  其中每个对象都根据命令的类型和所需的返回值公开用于执行命令的方法，如下表所述。  
  
|命令|返回值|  
|--------|---------|  
|`ExecuteReader`|返回一个 `DataReader` 对象。|  
|`ExecuteScalar`|返回一个标量值。|  
|`ExecuteNonQuery`|执行不返回任何行的命令。|  
|`ExecuteXMLReader`|返回 <xref:System.Xml.XmlReader>。  只用于 `SqlCommand` 对象。|  
  
 每个强类型命令对象还支持指定如何解释命令字符串的 <xref:System.Data.CommandType> 枚举，如下表所述。  
  
|CommandType|描述|  
|-----------------|--------|  
|`Text`|定义要在数据源处执行的语句的 SQL 命令。|  
|`StoredProcedure`|存储过程的名称。  您可以使用某一命令的 `Parameters` 属性访问输入和输出参数，并返回值（无论调用哪种 `Execute` 方法）。  当使用 `ExecuteReader` 时，在关闭 `DataReader` 后才能访问返回值和输出参数。|  
|`TableDirect`|表的名称。|  
  
## 示例  
 下面的代码示例演示如何创建 <xref:System.Data.SqlClient.SqlCommand> 对象以通过设置其属性执行存储过程。  <xref:System.Data.SqlClient.SqlParameter> 对象用于指定存储过程的输入参数。  使用 <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> 方法执行此命令，并在控制台窗口中显示 <xref:System.Data.SqlClient.SqlDataReader> 的输出。  
  
 [!code-csharp[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/VB/source.vb#1)]  
  
### 命令疑难解答  
 用于 SQL Server 的 .NET Framework 数据提供程序添加了性能计数器，使您能够检测与失败的命令执行相关的间歇性问题。  有关详细信息，请参阅 [性能计数器](../../../../docs/framework/data/adonet/performance-counters.md)。  
  
## 请参阅  
 [命令和参数](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [DataAdapter 和 DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [Working with DataReaders](http://msdn.microsoft.com/zh-cn/126a966a-d08d-4d22-a19f-f432908b2b54)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)