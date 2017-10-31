---
title: "Oracle 数据类型映射 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ec34ae21-bbbb-4adb-b672-83865e2a8451
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Oracle 数据类型映射
下表列出 Oracle 数据类型及其与 <xref:System.Data.OracleClient.OracleDataReader> 的映射。  
  
|Oracle 数据类型|由 OracleDataReader.GetValue 返回的 .NET Framework 数据类型|由 OracleDataReader.GetOracleValue 返回的 OracleClient 数据类型|备注|  
|-----------------|---------------------------------------------------------|-------------------------------------------------------------|--------|  
|**BFILE**|**Byte\[\]**|<xref:System.Data.OracleClient.OracleBFile>||  
|**BLOB**|**Byte\[\]**|<xref:System.Data.OracleClient.OracleLob>||  
|**CHAR**|**String**|<xref:System.Data.OracleClient.OracleString>||  
|**CLOB**|**String**|<xref:System.Data.OracleClient.OracleLob>||  
|**DATE**|**DateTime**|<xref:System.Data.OracleClient.OracleDateTime>||  
|**FLOAT**|**Decimal**|<xref:System.Data.OracleClient.OracleNumber>|此数据类型是 **NUMBER** 数据类型的别名，其设计目的是使 <xref:System.Data.OracleClient.OracleDataReader> 返回 **System.Decimal** 或 <xref:System.Data.OracleClient.OracleNumber>，而不是浮点值。  使用该 .NET Framework 数据类型可能导致溢出。|  
|**INTEGER**|**Decimal**|<xref:System.Data.OracleClient.OracleNumber>|此数据类型是 **NUMBER\(38\)** 数据类型的别名，其设计目的是使 <xref:System.Data.OracleClient.OracleDataReader> 返回 **System.Decimal** 或 <xref:System.Data.OracleClient.OracleNumber>，而不是整数值。  使用该 .NET Framework 数据类型可能导致溢出。|  
|**INTERVAL YEAR TO MONTH**|**Int32**|<xref:System.Data.OracleClient.OracleMonthSpan>||  
|**INTERVAL DAY TO SECOND**|**TimeSpan**|<xref:System.Data.OracleClient.OracleTimeSpan>||  
|**LONG**|**String**|<xref:System.Data.OracleClient.OracleString>||  
|**LONG RAW**|**Byte\[\]**|<xref:System.Data.OracleClient.OracleBinary>||  
|**NCHAR**|**String**|<xref:System.Data.OracleClient.OracleString>||  
|**NCLOB**|**String**|<xref:System.Data.OracleClient.OracleLob>||  
|**NUMBER**|**Decimal**|<xref:System.Data.OracleClient.OracleNumber>|使用该 .NET Framework 数据类型可能导致溢出。|  
|**NVARCHAR2**|**String**|<xref:System.Data.OracleClient.OracleString>||  
|**RAW**|**Byte\[\]**|<xref:System.Data.OracleClient.OracleBinary>||  
|**REF CURSOR**|||<xref:System.Data.OracleClient.OracleDataReader> 对象不支持 Oracle **REF CURSOR** 数据类型。|  
|**ROWID**|**String**|<xref:System.Data.OracleClient.OracleString>||  
|**TIMESTAMP**|**DateTime**|<xref:System.Data.OracleClient.OracleDateTime>||  
|**TIMESTAMP WITH LOCAL TIME ZONE**|**DateTime**|<xref:System.Data.OracleClient.OracleDateTime>||  
|**TIMESTAMP WITH TIME ZONE**|**DateTime**|<xref:System.Data.OracleClient.OracleDateTime>||  
|**UNSIGNED INTEGER**|**数字**|<xref:System.Data.OracleClient.OracleNumber>|此数据类型是 **NUMBER\(38\)** 数据类型的别名，其设计目的是使 <xref:System.Data.OracleClient.OracleDataReader> 返回 **System.Decimal** 或 <xref:System.Data.OracleClient.OracleNumber>，而不是无符号整数值。  使用该 .NET Framework 数据类型可能导致溢出。|  
|**VARCHAR2**|**String**|<xref:System.Data.OracleClient.OracleString>||  
  
 下表列出了在将数据类型作为参数绑定时使用的 Oracle 数据类型和 .NET Framework 数据类型（**System.Data.DbType** 和 <xref:System.Data.OracleClient.OracleType>）。  
  
|Oracle 数据类型|要绑定为参数的 DbType 枚举|要绑定为参数的 OracleType 枚举|备注|  
|-----------------|-----------------------|---------------------------|--------|  
|**BFILE**||**BFile**|Oracle 只允许将 **BFILE** 绑定为 **BFILE** 参数。  如果您尝试绑定一个非 **BFILE** 值（如 **byte\[\]** 或 <xref:System.Data.OracleClient.OracleBinary>），适用于 Oracle 的 .NET 数据提供程序并不会自动为您构造这样的值。|  
|**BLOB**||**Blob**|Oracle 只允许将 **BLOB** 绑定为 **BLOB** 参数。  如果您尝试绑定一个非 **BLOB** 值（如 **byte\[\]** 或 <xref:System.Data.OracleClient.OracleBinary>），适用于 Oracle 的 .NET 数据提供程序并不会自动为您构造这样的值。|  
|**CHAR**|**AnsiStringFixedLength**|**Char**||  
|**CLOB**||**Clob**|Oracle 只允许将 **CLOB** 绑定为 **CLOB** 参数。  如果您尝试绑定一个非 **CLOB** 值（如 **System.String** 或 <xref:System.Data.OracleClient.OracleString>），适用于 Oracle 的 .NET 数据提供程序并不会自动为您构造这样的值。|  
|**DATE**|**DateTime**|**DateTime**||  
|**FLOAT**|**Single、Double、Decimal**|**Float、Double、Number**|<xref:System.Data.OracleClient.OracleParameter.Size%2A> 确定 **System.Data.DBType** 和 <xref:System.Data.OracleClient.OracleType>。|  
|**INTEGER**|**SByte、Int16、Int32、Int64、Decimal**|**SByte、Int16、Int32、Number**|<xref:System.Data.OracleClient.OracleParameter.Size%2A> 确定 **System.Data.DBType** 和 <xref:System.Data.OracleClient.OracleType>。|  
|**INTERVAL YEAR TO MONTH**|**Int32**|**IntervalYearToMonth**|只有在同时使用 Oracle 9i 客户端和服务器软件时，<xref:System.Data.OracleClient.OracleType> 才可用。|  
|**INTERVAL DAY TO SECOND**|**对象**|**IntervalDayToSecond**|只有在同时使用 Oracle 9i 客户端和服务器软件时，<xref:System.Data.OracleClient.OracleType> 才可用。|  
|**LONG**|**AnsiString**|**LongVarChar**||  
|**LONG RAW**|**二进制**|**LongRaw**||  
|**NCHAR**|**StringFixedLength**|**NChar**||  
|**NCLOB**||**NClob**|Oracle 只允许将 **NCLOB** 绑定为 **NCLOB** 参数。  如果您尝试绑定一个非 **NCLOB** 值（如**System.String** 或 <xref:System.Data.OracleClient.OracleString>），适用于 Oracle 的 NET 数据提供程序并不会自动为您构造这样的值。|  
|**NUMBER**|**VarNumeric**|**数字**||  
|**NVARCHAR2**|**String**|**NVarChar**||  
|**RAW**|**二进制**|**Raw**||  
|**REF CURSOR**||**Cursor**|有关详细信息，请参阅[Oracle REF CURSOR](../../../../docs/framework/data/adonet/oracle-ref-cursors.md)。|  
|**ROWID**|**AnsiString**|**Rowid**||  
|**TIMESTAMP**|**DateTime**|**时间戳**|只有在同时使用 Oracle 9i 客户端和服务器软件时，<xref:System.Data.OracleClient.OracleType> 才可用。|  
|**TIMESTAMP WITH LOCAL TIME ZONE**|**DateTime**|**TimestampLocal**|只有在同时使用 Oracle 9i 客户端和服务器软件时，<xref:System.Data.OracleClient.OracleType> 才可用。|  
|**TIMESTAMP WITH TIME ZONE**|**DateTime**|**TimestampWithTz**|只有在同时使用 Oracle 9i 客户端和服务器软件时，<xref:System.Data.OracleClient.OracleType> 才可用。|  
|**UNSIGNED INTEGER**|**Byte、UInt16、UInt32、UInt64、Decimal**|**Byte、UInt16、Uint32、Number**|<xref:System.Data.OracleClient.OracleParameter.Size%2A> 确定 **System.Data.DBType** 和 <xref:System.Data.OracleClient.OracleType>。|  
|**VARCHAR2**|**AnsiString**|**VarChar**||  
  
 由 <xref:System.Data.OracleClient.OracleParameter> 对象的 <xref:System.Data.OracleClient.OracleParameter.Value%2A> 属性使用的 **InputOutput**、**Output** 和 **ReturnValue** **ParameterDirection** 值为 .NET Framework 数据类型，除非输入值是 Oracle 数据类型（例如 <xref:System.Data.OracleClient.OracleNumber> 或 <xref:System.Data.OracleClient.OracleString>）。  这并不适用于 **REF CURSOR**、**BFILE** 或 **LOB** 数据类型。  
  
## 请参阅  
 [Oracle 和 ADO.NET](../../../../docs/framework/data/adonet/oracle-and-adonet.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)