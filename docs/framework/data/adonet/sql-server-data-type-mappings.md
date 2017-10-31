---
title: "SQL Server 数据类型映射 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fafdc31a-f435-4cd3-883f-1dfadd971277
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# SQL Server 数据类型映射
SQL Server 和 .NET Framework 基于不同的类型系统。  例如，.NET Framework <xref:System.Decimal> 结构的最大小数位数为 28，而 SQL Server 的 decimal 和 numeric 数据类型的最大小数位数为 38。  为了在读取和写入数据时维护数据的完整性，<xref:System.Data.SqlClient.SqlDataReader> 将公开用于返回 <xref:System.Data.SqlTypes> 的对象的 SQL Server 特定的类型化访问器方法以及用于返回 .NET Framework 类型的访问器方法。  SQL Server 类型和 .NET Framework 类型也可通过 <xref:System.Data.DbType> 和 <xref:System.Data.SqlDbType> 类中的枚举表示，当您指定 <xref:System.Data.SqlClient.SqlParameter> 数据类型时可以使用这些枚举。  
  
 下表显示推断的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 类型、<xref:System.Data.DbType> 和 <xref:System.Data.SqlDbType> 枚举以及 <xref:System.Data.SqlClient.SqlDataReader> 的访问器方法。  
  
|SQL Server 数据库引擎类型|.NET Framework 类型|SqlDbType 枚举|SqlDataReader SqlTypes 类型化访问器|DbType 枚举|SqlDataReader DbType 类型化访问器|  
|------------------------|-----------------------|------------------|-----------------------------------|---------------|---------------------------------|  
|bigint|Int64|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlInt64%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetInt64%2A>|  
|binary|Byte\[\]|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlBinary%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|bit|Boolean|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlBoolean%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetBoolean%2A>|  
|char|String<br /><br /> Char\[\]|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType>,<br /><br /> <xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:System.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|date<br /><br /> （SQL Server 2008 及更高版本）|DateTime|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlDateTime%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetDateTime%2A>|  
|datetime|DateTime|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlDateTime%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetDateTime%2A>|  
|datetime2<br /><br /> （SQL Server 2008 及更高版本）|DateTime|<xref:System.Data.SqlDbType>|无|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetDateTime%2A>|  
|datetimeoffset<br /><br /> （SQL Server 2008 及更高版本）|DateTimeOffset|<xref:System.Data.SqlDbType>|无|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|  
|decimal|Decimal|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlDecimal%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetDecimal%2A>|  
|FILESTREAM 特性 \(varbinary\(max\)\)|Byte\[\]|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlBytes%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|float|Double|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlDouble%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetDouble%2A>|  
|图像|Byte\[\]|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlBinary%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|int|Int32|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlInt32%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetInt32%2A>|  
|money|Decimal|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlMoney%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetDecimal%2A>|  
|nchar|String<br /><br /> Char\[\]|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:System.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|ntext|String<br /><br /> Char\[\]|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:System.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|数值|Decimal|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlDecimal%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetDecimal%2A>|  
|nvarchar|String<br /><br /> Char\[\]|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:System.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|实数|Single|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlSingle%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetFloat%2A>|  
|rowversion|Byte\[\]|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlBinary%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|smalldatetime|DateTime|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlDateTime%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetDateTime%2A>|  
|smallint|Int16|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlInt16%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetInt16%2A>|  
|smallmoney|Decimal|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlMoney%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetDecimal%2A>|  
|sql\_variant|Object\*|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlValue%2A> \*|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetValue%2A> \*|  
|文本|String<br /><br /> Char\[\]|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:System.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|时间<br /><br /> （SQL Server 2008 及更高版本）|TimeSpan|<xref:System.Data.SqlDbType>|无|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetDateTime%2A>|  
|时间戳|Byte\[\]|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlBinary%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|tinyint|Byte|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlByte%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetByte%2A>|  
|uniqueidentifier|Guid|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlGuid%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetGuid%2A>|  
|varbinary|Byte\[\]|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlBinary%2A>|<xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|varchar|String<br /><br /> Char\[\]|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType>, <xref:System.Data.DbType>|<xref:System.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:System.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|xml|Xml|<xref:System.Data.SqlDbType>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlXml%2A>|<xref:System.Data.DbType>|无|  
  
 \* 如果已知 `sql_variant` 的基础类型，则使用特定的类型化访问器。  
  
## [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 联机丛书参考  
 有关 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 数据类型的更多信息，请参见[数据类型（数据库引擎）](http://go.microsoft.com/fwlink/?LinkID=107468)（可能为英文网页）。  
  
## 请参阅  
 [SQL Server 数据类型和 ADO.NET](../../../../docs/framework/data/adonet/sql/sql-server-data-types.md)   
 [SQL Server 二进制和大值数据](../../../../docs/framework/data/adonet/sql/sql-server-binary-and-large-value-data.md)   
 [ADO.NET 中的数据类型映射](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md)   
 [配置参数和参数数据类型](../../../../docs/framework/data/adonet/configuring-parameters-and-parameter-data-types.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)