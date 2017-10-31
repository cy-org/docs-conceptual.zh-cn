---
title: "日期和时间函数 | Microsoft Docs"
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
ms.assetid: 971762d0-663b-4b64-8c61-352a8e6d3949
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 日期和时间函数
SQL Server .NET Framework 数据提供程序 \(SqlClient\) 提供了日期和时间函数，这些函数针对 `System.DateTime` 输入值执行运算并返回 `string`、数值或 `System.DateTime` 值结果。  这些函数位于 SqlServer 命名空间中，该命名空间在您使用 SqlClient 时可用。  提供程序的命名空间属性使实体框架可以确定此提供程序对特定构造（如类型和函数）使用哪个前缀。下表显示 SqlClient 日期和时间函数。  
  
|函数|描述|  
|--------|--------|  
|`DATEADD(` `datepart`, `number`, `date``)`|返回给指定日期加上一个间隔后的新 `DateTime` 值。<br /><br /> **参数**<br /><br /> `datepart`：一个 `String`，表示用于返回新值的日期部分。<br /><br /> `number`：用于增加 `datepart` 的 `Int32`、`Int64`、`Decimal` 或 `Double` 值。<br /><br /> `date`：一个表达式，返回精度为 0 到 7 的 `DateTime`、`DateTimeOffset` 或 `Time` 或日期格式的字符串。<br /><br /> **返回值**<br /><br /> 精度为 0 到 7 的新 `DateTime`、`DateTimeOffset` 或 `Time` 值。<br /><br /> **示例**<br /><br /> `SqlServer.DATEADD('day', 22, cast('6/9/2006' as DateTime))`|  
|`DATEDIFF(` `datepart`, `startdate`, `enddate``)`|返回两个指定日期之间所跨的日期和时间边界的数目。<br /><br /> **参数**<br /><br /> `datepart`：一个 `String`，表示用于计算差异的日期部分。<br /><br /> `startdate`：计算的开始日期为一个表达式，该表达式返回精度为 0 到 7 的 `DateTime`、`DateTimeOffset` 或 `Time` 值或日期格式的字符串。<br /><br /> `enddate`：计算的结束日期为一个表达式，该表达式返回精度为 0 到 7 的 `DateTime`、`DateTimeOffset` 或 `Time` 值或日期格式的字符串。<br /><br /> **返回值**<br /><br /> `Int32`。<br /><br /> **示例**<br /><br /> `SqlServer.DATEDIFF('day', cast('6/9/2006' as DateTime),`<br /><br /> `cast('6/20/2006' as DateTime))`|  
|`DATENAME(` `datepart`, `date``)`|返回表示指定日期的指定日期部分的字符串。<br /><br /> **参数**<br /><br /> `datepart`：一个 `String`，表示用于返回新值的日期部分。<br /><br /> `date`：一个表达式，返回精度为 0 到 7 的 `DateTime`、`DateTimeOffset` 或 `Time` 值或日期格式的字符串。<br /><br /> **返回值**<br /><br /> 表示指定日期的指定日期部分的字符串。<br /><br /> **示例**<br /><br /> `SqlServer.DATENAME('year', cast('6/9/2006' as DateTime))`|  
|`DATEPART(` `datepart`, `date``)`|返回表示指定日期的指定日期部分的整数。<br /><br /> **参数**<br /><br /> `datepart`：一个 `String`，表示用于返回新值的日期部分。<br /><br /> `date`：一个表达式，返回精度为 0 到 7 的 `DateTime`、`DateTimeOffset` 或 `Time` 值或日期格式的字符串。<br /><br /> **返回值**<br /><br /> 指定日期的指定日期部分（以 `Int32` 表示）。<br /><br /> **示例**<br /><br /> `SqlServer.DATEPART('year', cast('6/9/2006' as DateTime))`|  
|`DAY(` `date` `)`|以整数形式返回指定日期的“日”。<br /><br /> **参数**<br /><br /> `date`：类型为 `DateTime` 或 `DateTimeOffset`、精度为 0 到 7 的表达式。<br /><br /> **返回值**<br /><br /> 指定日期的“日”（以 `Int32` 表示）。<br /><br /> **示例**<br /><br /> `SqlServer.DAY(cast('6/9/2006' as DateTime))`|  
|`GETDATE()`|为 datetime 值生成以 SQL Server 内部格式表示的当前日期和时间。<br /><br /> **返回值**<br /><br /> `DateTime` 类型的当前系统日期和时间（精度为 3）。<br /><br /> **示例**<br /><br /> `SqlServer.GETDATE()`|  
|`GETUTCDATE()`|以 UTC（协调世界时或格林威治标准时间）格式生成 datetime 值。<br /><br /> **返回值**<br /><br /> UTC 格式的 `DateTime` 值（精度为 3）。<br /><br /> **示例**<br /><br /> `SqlServer.GETUTCDATE()`|  
|`MONTH(` `date` `)`|以整数形式返回指定日期的月份。<br /><br /> **参数**<br /><br /> `date`：类型为 `DateTime` 或 `DateTimeOffset`、精度为 0 到 7 的表达式。<br /><br /> **返回值**<br /><br /> 指定日期的月份（以 `Int32` 表示）。<br /><br /> **示例**<br /><br /> `SqlServer.MONTH(cast('6/9/2006' as DateTime))`|  
|`YEAR(` `date` `)`|以整数形式返回指定日期的年度。<br /><br /> **参数**<br /><br /> `date`：类型为 `DateTime` 或 `DateTimeOffset`、精度为 0 到 7 的表达式。<br /><br /> **返回值**<br /><br /> 指定日期的年度（以 `Int32` 表示）。<br /><br /> **示例**<br /><br /> `SqlServer.YEAR(cast('6/9/2006' as DateTime))`|  
|`SYSDATETIME()`|返回精度为 7 的 `DateTime` 值。<br /><br /> **返回值**<br /><br /> 精度为 7 的 `DateTime` 值。<br /><br /> **示例**<br /><br /> `SqlServer.SYSDATETIME()`|  
|`SYSUTCDATE()`|以 UTC（协调世界时或格林威治标准时间）格式生成 datetime 值。<br /><br /> **返回值**<br /><br /> UTC 格式的 `DateTime` 值（精度为 7）。<br /><br /> **示例**<br /><br /> `SqlServer.SYSUTCDATE()`|  
|`SYSDATETIMEOFFSET()`|返回精度为 7 的 `DateTimeOffset` 值。<br /><br /> **返回值**<br /><br /> UTC 格式的 `DateTimeOffset` 值（精度为 7）。<br /><br /> **示例**<br /><br /> `SqlServer.SYSDATETIMEOFFSET()`|  
  
 有关 SqlClient 支持的日期和时间函数的更多信息，请参见 SqlClient 提供程序清单中所指定的 SQL Server 版本的相应文档：  
  
|SQL Server 2000|SQL Server 2005|SQL Server 2008|  
|---------------------|---------------------|---------------------|  
|[日期和时间函数 \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=115908)（可能为英文网页）|[日期和时间函数 \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=115909)（可能为英文网页）|[日期和时间函数 \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=98360)（可能为英文网页）|  
  
## 请参阅  
 [用于实体框架函数的 SqlClient](../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md)