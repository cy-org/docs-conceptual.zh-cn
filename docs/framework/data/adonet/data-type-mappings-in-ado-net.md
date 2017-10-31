---
title: "ADO.NET 中的数据类型映射 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d4afab94-ada6-4c77-a73c-41f17bae6b5a
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# ADO.NET 中的数据类型映射
.NET Framework 基于用于定义如何在运行时声明、使用和管理类型的通用类型系统。  它由值类型和引用类型组成，这两种类型均派生自 <xref:System.Object> 基类型。  使用数据源时，如果未显式指定数据类型，则从数据提供程序推断出它。  例如，<xref:System.Data.DataSet> 对象独立于任何特定的数据源。  `DataSet` 中的数据从数据源中进行检索，而更改则会使用 `DataAdapter` 持久保存回数据源。  这意味着当 `DataAdapter` 使用数据源中的值填充 `DataSet` 中的 <xref:System.Data.DataTable> 时，`DataTable` 中列的结果数据类型为 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 类型，而不是特定于用于连接数据源的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 数据提供程序的类型。  
  
 同样，当 `DataReader` 返回数据源中的值时，生成的值将存储在具有 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 类型的局部变量中。对于 `DataAdapter` 的 `Fill` 操作和 `DataReader` 的`Get` 方法，将从 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 数据提供程序中返回的值来推断 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 类型。  
  
 当所返回值的特定类型已知时，您可以使用 `DataReader` 的类型化访问器方法，而不是依靠推断出的数据类型。  类型化访问器方法以特定 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 类型的形式返回值，无需再进行其他类型转换，因此会提高性能。  
  
> [!NOTE]
>  [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 数据提供程序的数据类型的 null 值都用 `DBNull.Value` 表示。  
  
## 本节内容  
 [SQL Server 数据类型映射](../../../../docs/framework/data/adonet/sql-server-data-type-mappings.md)  
 列出针对 <xref:System.Data.SqlClient> 的推断数据类型映射和数据访问器方法。  
  
 [OLE DB 数据类型映射](../../../../docs/framework/data/adonet/ole-db-data-type-mappings.md)  
 列出针对 <xref:System.Data.OleDb> 的推断数据类型映射和数据访问器方法。  
  
 [ODBC 数据类型映射](../../../../docs/framework/data/adonet/odbc-data-type-mappings.md)  
 列出针对 <xref:System.Data.Odbc> 的推断数据类型映射和数据访问器方法。  
  
 [Oracle 数据类型映射](../../../../docs/framework/data/adonet/oracle-data-type-mappings.md)  
 列出针对 <xref:System.Data.OracleClient> 的推断数据类型映射和数据访问器方法。  
  
 [浮点数](../../../../docs/framework/data/adonet/floating-point-numbers.md)  
 描述开发人员在使用浮点数时经常遇到的问题。  
  
## 请参阅  
 [SQL Server 数据类型和 ADO.NET](../../../../docs/framework/data/adonet/sql/sql-server-data-types.md)   
 [配置参数和参数数据类型](../../../../docs/framework/data/adonet/configuring-parameters-and-parameter-data-types.md)   
 [检索数据库架构信息](../../../../docs/framework/data/adonet/retrieving-database-schema-information.md)   
 [常规类型系统](../../../../docs/standard/base-types/common-type-system.md)   
 [Converting Types](http://msdn.microsoft.com/zh-cn/6038316e-bdaf-4f55-8006-407f591ce156)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)