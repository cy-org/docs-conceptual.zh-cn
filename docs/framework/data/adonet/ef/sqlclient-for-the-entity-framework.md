---
title: "用于实体框架的 SqlClient | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 9a5d6d39-d955-43a5-a5c2-931c239398f1
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 用于实体框架的 SqlClient
本节介绍用于 SQL Server \(SqlClient\) 的 .NET Framework 数据提供程序，该提供程序使实体框架能够在 Microsoft SQL Server 上工作。  
  
## Provider 架构属性  
 `Provider` 是以存储架构定义语言 \(SSDL\) 表示的 `Schema` 元素的一个特性。  
  
 若要使用 SqlClient，请将字符串“System.Data.SqlClient”分配给 `Schema` 元素的 `Provider` 属性。  
  
## ProviderManifestToken 架构属性  
 `ProviderManifestToken` 是以 SSDL 表示的 `Schema` 元素的一个必需特性。  此标记用于为脱机方案加载提供程序清单。  有关 `ProviderManifestToken` 属性的更多信息，请参见 [Schema Element \(SSDL\)](http://msdn.microsoft.com/zh-cn/fec75ae4-7f16-4421-9265-9dac61509222)。  
  
 SqlClient 可以用作不同版本 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 的数据提供程序。  这些版本具有不同的功能。  例如，[!INCLUDE[ssVersion2000](../../../../../includes/ssversion2000-md.md)] 不支持在 [!INCLUDE[ssVersion2005](../../../../../includes/ssversion2005-md.md)] 中引入的 `varchar(max)` 和 `nvarchar(max)` 类型。  
  
 针对不同版本的 SQL Server，SqlClient 生成和接受以下提供程序清单标记。  
  
||||  
|-|-|-|  
|SQL Server 2000|SQL Server 2005|SQL Server 2008|  
|2000|2005|2008|  
  
> [!NOTE]
>  从 [!INCLUDE[vsprvs](../../../../../includes/vsprvs-md.md)] 2010 开始，[ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/zh-cn/91076853-0881-421b-837a-f582f36be527) 不支持 SQL Server 2000。  
  
## 提供程序命名空间名称  
 所有提供程序都必须指定一个命名空间。  实体框架通过此属性获知提供程序为特定构造（如类型和函数）使用哪个前缀。  SqlClient 提供程序清单的命名空间为 `SqlServer`。  有关命名空间的更多信息，请参见[命名空间](../../../../../docs/framework/data/adonet/ef/language-reference/namespaces-entity-sql.md)。  
  
## 类型  
 实体框架的 SqlClient 提供程序提供概念模型类型与 SQL Server 类型之间的映射信息。  有关详细信息，请参阅[用于实体框架的 SqlClient 类型](../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-types.md)。  
  
## 函数  
 实体框架的 SqlClient 提供程序定义提供程序支持的函数列表。  有关支持的函数的列表，请参见 [用于实体框架函数的 SqlClient](../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md)。  
  
## 本节内容  
 [用于实体框架函数的 SqlClient](../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md)  
  
 [用于实体框架的 SqlClient 类型](../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-types.md)  
  
 [用于实体框架的 SqlClient 的已知问题](../../../../../docs/framework/data/adonet/ef/known-issues-in-sqlclient-for-entity-framework.md)  
  
## 请参阅  
 [Entity SQL 语言](../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-language.md)   
 [语言参考](../../../../../docs/framework/data/adonet/ef/language-reference/index.md)   
 [Known Issues in SqlClient Provider for Entity Framework](../../../../../docs/framework/data/adonet/ef/sqlclient-for-the-entity-framework.md)