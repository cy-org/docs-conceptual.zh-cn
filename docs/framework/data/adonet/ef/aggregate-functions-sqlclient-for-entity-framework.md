---
title: "聚合函数（用于实体框架的 SqlClient） | Microsoft Docs"
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
ms.assetid: 03303f01-b591-4efc-9875-f9c608edff0b
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 聚合函数（用于实体框架的 SqlClient）
SQL Server .NET Framework 数据提供程序 \(SqlClient\) 提供聚合函数。  聚合函数对一组输入值执行计算并返回一个值。  这些函数位于 SqlServer 命名空间中，该命名空间在您使用 SqlClient 时可用。  提供程序的命名空间属性使实体框架可以确定此提供程序对特定构造（如类型和函数）使用哪个前缀。  
  
 下表显示 SqlClient 聚合函数。  
  
|函数|描述|  
|--------|--------|  
|`AVG(` `expression` `)`|返回集合中各值的平均值。<br /><br /> 空值将被忽略。<br /><br /> **参数**<br /><br /> `Int32`、 `Int64`、`Double` 和 `Decimal`。<br /><br /> **返回值**<br /><br /> `expression` 的类型。<br /><br /> **示例**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_AVG](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_avg)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_AVG](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_avg)]|  
|`CHECKSUM_AGG(` `collection` `)`|返回集合中各值的校验和。<br /><br /> 空值将被忽略。<br /><br /> **参数**<br /><br /> 集合 \(`Int32`\)。<br /><br /> **返回值**<br /><br /> `Int32`。<br /><br /> **示例**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_CHECKSUM](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_checksum)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_CHECKSUM](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_checksum)]|  
|`COUNT(` `expression` `)`|以 `Int32` 形式返回集合中的项数。<br /><br /> **参数**<br /><br /> 集合 \(T\)，其中 T 为以下类型之一：<br /><br /> `Guid`（在 SQL Server 2000 中不返回）、<br /><br /> `Boolean`、`Double`、`DateTime`、`DateTimeOffset`、`Time`、`String` 或 `Binary`。<br /><br /> **返回值**<br /><br /> `Int32`。<br /><br /> **示例**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_COUNT](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_count)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_COUNT](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_count)]|  
|`COUNT_BIG(` `expression` `)`|以 `bigint` 形式返回集合中的项数。<br /><br /> **参数**<br /><br /> 集合 \(T\)，其中 T 为以下类型之一：<br /><br /> `Guid`（在 SQL Server 2000 中不返回）、`Boolean`、`Double`、`DateTime`、`DateTimeOffset`、`Time`、`String` 或 `Binary`。<br /><br /> **返回值**<br /><br /> `Int64`。<br /><br /> **示例**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_COUNTBIG](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_countbig)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_COUNTBIG](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_countbig)]|  
|`MAX(` `expression` `)`|返回集合中的最大值。<br /><br /> **参数**<br /><br /> 集合 \(T\)，其中 T 为以下类型之一：`Byte`、`Int16`、`Int32`、`Int64`、`Byte`、`Single`、`Double`、`Decimal`、`DateTime`、`DateTimeOffset`、`Time`、`String` 和 `Binary`。<br /><br /> **返回值**<br /><br /> `expression` 的类型。<br /><br /> **示例**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_MAX](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_max)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_MAX](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_max)]|  
|`MIN(` `expression` `)`|返回集合中的最小值。<br /><br /> **参数**<br /><br /> 集合 \(T\)，其中 T 为以下类型之一：`Byte`、`Int16`、`Int32`、`Int64`、`Byte`、`Single`、`Double`、`Decimal`、`DateTime`、`DateTimeOffset`、`Time`、`String`、<br /><br /> `Binary`.<br /><br /> **返回值**<br /><br /> `expression` 的类型。<br /><br /> **示例**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_MIN](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_min)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_MIN](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_min)]|  
|`STDEV(` `expression` `)`|返回指定表达式中所有值的统计标准偏差。<br /><br /> **参数**<br /><br /> 集合 \(`Double`\)。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_STDEV](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_stdev)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_STDEV](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_stdev)]|  
|`STDEVP(` `expression` `)`|返回指定表达式中所有值的总体标准偏差。<br /><br /> **参数**<br /><br /> 集合 \(`Double`\)。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_STDEVP](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_stdevp)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_STDEVP](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_stdevp)]|  
|`SUM(` `expression` `)`|返回集合中所有值的总和。<br /><br /> **参数**<br /><br /> 集合 \(T\)，其中 T 为以下类型之一：`Int32`、`Int64`、`Double` 和 `Decimal`。<br /><br /> **返回值**<br /><br /> `expression` 的类型。<br /><br /> **示例**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_SUM](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_sum)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_SUM](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_sum)]|  
|`VAR(` `expression` `)`|返回指定表达式中所有值的方差。<br /><br /> **参数**<br /><br /> 集合 \(`Double`\)。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_VAR](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_var)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_VAR](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_var)]|  
|`VARP(` `expression` `)`|返回指定表达式中所有值的总体方差。<br /><br /> **参数**<br /><br /> 集合 \(`Double`\)。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_VARP](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_varp)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_VARP](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_varp)]|  
  
 有关 SqlClient 支持的聚合函数的更多信息，请参见 SqlClient 提供程序清单中所指定的 SQL Server 版本的相应文档：  
  
|SQL Server 2000|SQL Server 2005|SQL Server 2008|  
|---------------------|---------------------|---------------------|  
|[聚合函数 \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=115906)（可能为英文网页）|[聚合函数 \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkID=115903)（可能为英文网页）|[聚合函数 \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=115907)（可能为英文网页）|  
  
## 请参阅  
 [Entity SQL 语言](../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-language.md)   
 [聚合规范函数](../../../../../docs/framework/data/adonet/ef/language-reference/aggregate-canonical-functions.md)