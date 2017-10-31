---
title: "数学函数 | Microsoft Docs"
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
ms.assetid: b040c7cb-156d-40f2-9152-61065b18148c
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 数学函数
SQL Server .NET Framework 数据提供程序 \(SqlClient\) 提供了各种数学函数，这些函数针对作为参数提供的输入值执行计算并返回数值结果。  这些函数位于 SqlServer 命名空间中，该命名空间在您使用 SqlClient 时可用。  提供程序的命名空间属性使实体框架可以确定此提供程序对特定构造（如类型和函数）使用哪个前缀。下表描述 SqlClient 数学函数。  
  
|函数|描述|  
|--------|--------|  
|`ABS(` `expression` `)`|执行绝对值函数。<br /><br /> **参数**<br /><br /> `expression`：`Int32`、 `Int64`、`Double` 或 `Decimal`。<br /><br /> **返回值**<br /><br /> 指定表达式的绝对值。<br /><br /> **示例**<br /><br /> `SqlServer.ABS(-2)`|  
|`ACOS(` `expression` `)`|返回指定表达式的反余弦值。<br /><br /> **参数**<br /><br /> `expression`：`Double`。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> `SqlServer.ACOS(.9)`|  
|`ASIN(` `expression` `)`|返回指定表达式的反正弦值。<br /><br /> **参数**<br /><br /> `expression`：`Double`。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> `SqlServer.ASIN(.9)`|  
|`ATAN(` `expression` `)`|返回指定数值表达式的反正切值。<br /><br /> **参数**<br /><br /> `expression`：`Double`。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> `SqlServer.ATAN(9)`|  
|`ATN2(` `expression`, `expression``)`|返回以弧度表示的角度，其正切介于两个指定的数值表达式之间。<br /><br /> **参数**<br /><br /> `expression`：`Double`。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> `SqlServer.ATN2(9, 8)`|  
|`CEILING(` `expression` `)`|将指定表达式转换为大于或等于该表达式的最小整数。<br /><br /> **参数**<br /><br /> `expression`：`Int32`、 `Int64`、`Double` 或 `Decimal`。<br /><br /> **返回值**<br /><br /> `Int32`、`Int64`、`Double` 或 `Decimal`。<br /><br /> **示例**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_CEILING](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_ceiling)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_CEILING](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_ceiling)]|  
|`COS(` `expression` `)`|计算以弧度表示的指定角度的三角余弦。<br /><br /> **参数**<br /><br /> `expression`：`Double`。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> `SqlServer.COS(45)`|  
|`COT(` `expression` `)`|计算以弧度表示的指定角度的三角余切。<br /><br /> **参数**<br /><br /> `expression`：`Double`。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> `SqlServer.COT(60)`|  
|`DEGREES(` `radians` `)`|返回以度为单位的对应角度。<br /><br /> **参数**<br /><br /> `expression`：`Int32`、 `Int64`、`Double` 或 `Decimal`。<br /><br /> **返回值**<br /><br /> `Int32`、`Int64`、`Double` 或 `Decimal`。<br /><br /> **示例**<br /><br /> `SqlServer.DEGREES(3.1)`|  
|`EXP(` `expression` `)`|计算指定数值表达式的指数值。<br /><br /> **参数**<br /><br /> `expression`：`Double`。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> `SqlServer.EXP(1)`|  
|`FLOOR(` `expression` `)`|将指定表达式转换为小于或等于该表达式的最大整数。<br /><br /> **参数**<br /><br /> `expression`：`Double`。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> [!code-csharp[DP EntityServices Concepts#SQLSERVER_FLOOR](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/entitysql.cs#sqlserver_floor)]
 [!code-sql[DP EntityServices Concepts#SQLSERVER_FLOOR](../../../../../samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_floor)]|  
|`LOG(` `expression` `)`|计算指定 `float` 表达式的自然对数。<br /><br /> **参数**<br /><br /> `expression`：`Double`。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> `SqlServer.LOG(100)`|  
|`LOG10(` `expression` `)`|返回指定 `Double` 表达式的以 10 为底的对数。<br /><br /> **参数**<br /><br /> `expression`：`Double`。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> `SqlServer.LOG10(100)`|  
|`PI()`|以 `Double` 格式返回 pi 的常量值。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> `SqlServer.PI()`|  
|`POWER(` `numeric_expression, power_expression` `)`|计算指定表达式的指定幂的值。<br /><br /> **参数**<br /><br /> `numeric_expression`： `Int32`、 `Int64`、`Double` 或 `Decimal`。<br /><br /> `power_expression`：`Double`，表示对 `numeric_expression` 进行幂运算的幂值。<br /><br /> **返回值**<br /><br /> 指定 `numeric_expression` 的指定 `power_expression` 次幂的值。<br /><br /> **示例**<br /><br /> `SqlServer.POWER(2,7)`|  
|`RADIANS(` `expression` `)`|将度数转换成弧度。<br /><br /> **参数**<br /><br /> `expression`：`Int32`、 `Int64`、`Double` 或 `Decimal`。<br /><br /> **返回值**<br /><br /> `Int32`、 `Int64`、<br /><br /> `Double` 或<br /><br /> `Decimal`.<br /><br /> **示例**<br /><br /> `SqlServer.RADIANS(360.0)`|  
|`RAND(`\[seed\]`)`|返回介于 0 和 1 之间的随机值。<br /><br /> **参数**<br /><br /> 以 `Int32` 形式返回种子值。  如果未指定种子，则 SQL Server 数据库引擎将随机分配种子值。  对于指定的种子值，返回的结果始终相同。<br /><br /> **返回值**<br /><br /> 介于 0 和 1 之间的随机 `Double` 值。<br /><br /> **示例**<br /><br /> `SqlServer.RAND()`|  
|`ROUND(` `numeric_expression, length` \[ ,`function` \]`)`|返回一个舍入到指定长度或精度的数值表达式。<br /><br /> **参数**<br /><br /> `numeric_expression`： `Int32`、 `Int64`、`Double` 或 `Decimal`。<br /><br /> `length`：表示 `numeric_expression` 要舍入到的精度的 `Int32`。  如果 `length` 为正数，则将 `numeric_expression` 舍入到 `length` 指定的小数位数。  如果 `length` 为负数，则将 `numeric_expression` 向小数点左边舍入 `length` 指定的长度。<br /><br /> `function`： `` （可选）表示要执行的操作类型的 `Int32`。  如果省略 function 或其值为 0（默认值），则将舍入 `numeric_expression`。  如果指定了 0 以外的值，则将截断 `numeric_expression` 。<br /><br /> **返回值**<br /><br /> 指定 `numeric_expression` 的指定 `power_expression` 次幂的值。<br /><br /> **示例**<br /><br /> `SqlServer.ROUND(748.58, -3)`|  
|`SIGN(` `expression` `)`|返回指定表达式的正号 \(\+1\)、零 \(0\) 或负号 \(\-1\)。<br /><br /> **参数**<br /><br /> `expression`：`Int32`、`Int64`、`Double` 或 `Decimal`<br /><br /> **返回值**<br /><br /> `Int32`、`Int64`、`Double` 或 `Decimal`。<br /><br /> **示例**<br /><br /> `SqlServer.SIGN(-10)`|  
|`SIN(` `expression` `)`|计算以弧度表示的指定角度的三角正弦并返回 `Double` 表达式。<br /><br /> **参数**<br /><br /> `expression`：`Double`。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> `SqlServer.SIN(20)`|  
|`SQRT(` `expression` `)`|返回指定表达式的平方根。<br /><br /> **参数**<br /><br /> `expression`：`Double`。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> `SqlServer.SQRT(3600)`|  
|`SQUARE(` `expression` `)`|返回指定表达式的平方。<br /><br /> **参数**<br /><br /> `expression`：`Double`。<br /><br /> **返回值**<br /><br /> `Double`。<br /><br /> **示例**<br /><br /> `SqlServer.SQUARE(25)`|  
|`TAN(` `expression` `)`|计算指定表达式的正切。<br /><br /> **参数**<br /><br /> `expression`: `Double`<br /><br /> **返回值**<br /><br /> `Double`<br /><br /> **示例**<br /><br /> `SqlServer.TAN(45.0)`|  
  
 有关 SqlClient 支持的数学函数的更多信息，请参见 SqlClient 提供程序清单中所指定的 SQL Server 版本的相应文档：  
  
|SQL Server 2000|SQL Server 2005|SQL Server 2008|  
|---------------------|---------------------|---------------------|  
|[数学函数 \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=115913)（可能为英文网页）|[数学函数 \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=115911)（可能为英文网页）|[数学函数 \(Transact\-SQL\)](http://go.microsoft.com/fwlink/?LinkId=115912)（可能为英文网页）|  
  
## 请参阅  
 [用于实体框架函数的 SqlClient](../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md)