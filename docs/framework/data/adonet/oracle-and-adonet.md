---
title: "Oracle 和 ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8ee8e389-53cf-45cf-80bd-1df63ef34f2e
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Oracle 和 ADO.NET
> [!NOTE]
>  <xref:System.Data.OracleClient> 中的类型已过时。  当前版本的 .NET Framework 仍支持这些类型，但以后的版本会将这些类型删除。  Microsoft 建议您使用第三方 Oracle 提供程序。  
  
 本节说明特定于适用于 Oracle 的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 数据提供程序的功能和行为。  
  
 适用于 Oracle 的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 数据提供程序允许使用 Oracle 客户端软提供的 Oracle 调用接口 \(OCI\) 来访问 Oracle 数据库。  该数据提供程序设计的功能与用于 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]、OLE DB 和 ODBC 的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 数据提供程序的功能类似。  
  
 若要使用适用于 Oracle 的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 数据提供程序，应用程序必须引用 <xref:System.Data.OracleClient> 命名空间，如下所示：  
  
```vb  
Imports System.Data.OracleClient  
```  
  
```csharp  
using System.Data.OracleClient;  
```  
  
 在编译代码时还必须包括对该 DLL 的引用。  例如，如果编译的是 C\# 程序，命令行中应包括：  
  
```  
csc /r:System.Data.OracleClient.dll  
```  
  
## 本节内容  
 [系统要求](../../../../docs/framework/data/adonet/system-requirements-for-the-dotnet-data-provider-for-oracle.md)  
 说明使用适用于 Oracle 的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 数据提供程序时的要求，并说明使用时应注意的若干问题。  
  
 [Oracle BFILE](../../../../docs/framework/data/adonet/oracle-bfiles.md)  
 描述用于使用 Oracle BFILE 数据类型的 <xref:System.Data.OracleClient.OracleBFile> 类。  
  
 [Oracle LOB](../../../../docs/framework/data/adonet/oracle-lobs.md)  
 描述用于使用 Oracle LOB 数据类型的 <xref:System.Data.OracleClient.OracleLob> 类。  
  
 [Oracle REF CURSOR](../../../../docs/framework/data/adonet/oracle-ref-cursors.md)  
 描述对 Oracle REF CURSOR 数据类型的支持。  
  
 [OracleType](../../../../docs/framework/data/adonet/oracletypes.md)  
 描述可以用于使用 Oracle 数据类型的结构，包括 <xref:System.Data.OracleClient.OracleNumber> 和 <xref:System.Data.OracleClient.OracleString>。  
  
 [Oracle 序列](../../../../docs/framework/data/adonet/oracle-sequences.md)  
 说明对检索服务器生成的 Oracle 键序列值的支持。  
  
 [Oracle 数据类型映射](../../../../docs/framework/data/adonet/oracle-data-type-mappings.md)  
 列出 Oracle 数据类型及其与 <xref:System.Data.OracleClient.OracleDataReader> 的映射。  
  
 [Oracle 分布式事务](../../../../docs/framework/data/adonet/oracle-distributed-transactions.md)  
 描述 <xref:System.Data.OracleClient.OracleConnection> 对象如何自动在现有分布式事务中登记（如果确定某个事务是活动的）。  
  
## 相关章节  
 [保证 ADO.NET 应用程序的安全](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)  
 说明使用 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 时的安全编码做法。  
  
 [DataSet、DataTable 和 DataView](../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)  
 说明如何创建和使用 `DataSets`、类型化 `DataSets`、`DataTables` 和 `DataViews`。  
  
 [在 ADO.NET 中检索和修改数据](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)  
 说明如何使用 ADO.NET 中的数据。  
  
 [SQL Server 和 ADO.NET](../../../../docs/framework/data/adonet/sql/index.md)  
 说明如何使用特定于 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 的功能。  
  
 [DbProviderFactory](../../../../docs/framework/data/adonet/dbproviderfactories.md)  
 说明允许在 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 中编写独立于提供程序的代码的泛型类。  
  
## 请参阅  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)