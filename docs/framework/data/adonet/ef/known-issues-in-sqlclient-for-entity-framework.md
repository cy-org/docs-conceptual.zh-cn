---
title: "用于实体框架的 SqlClient 的已知问题 | Microsoft Docs"
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
ms.assetid: 48fe4912-4d0f-46b6-be96-3a42c54780f6
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 用于实体框架的 SqlClient 的已知问题
本节介绍与 SQL Server .NET Framework 数据提供程序 \(SqlClient\) 有关的已知问题。  
  
## 字符串函数中的尾随空格  
 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 忽略字符串值中的尾随空格。  因此，传递字符串中的尾随空格可能导致意外的结果，甚至会导致失败。  
  
 如果字符串中必须包含尾随空格，应考虑在末尾追加一个空白字符，这样 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 就不会修整该字符串。  如果尾随空格不是必需的，应在传递给查询管道之前进行修整。  
  
## RIGHT 函数  
 如果将非 `null` 值和 0 分别作为第一个参数和第二个参数传递给 `RIGHT(nvarchar(max)`, 0`)` 或 `RIGHT(varchar(max)`, 0`)`，将返回 `NULL` 值，而不是 `empty` 字符串。  
  
## CROSS 和 OUTER APPLY 运算符  
 [!INCLUDE[ssVersion2005](../../../../../includes/ssversion2005-md.md)] 引入了 CROSS 和 OUTER APPLY 运算符。  在某些情况下，查询管道可能生成包含 CROSS APPLY 和\/或 OUTER APPLY 运算符的 Transact\-SQL 语句。  因为某些后端提供程序（包括 [!INCLUDE[ssVersion2005](../../../../../includes/ssversion2005-md.md)] 之前的 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 版本）不支持这些运算符，所以不能对这些后端提供程序执行此类查询。  
  
 下面是一些可能导致输出查询中出现 CROSS APPLY 和\/或 OUTER APPLY 运算符的典型情况：  
  
-   带分页的相关子查询。  
  
-   相关子查询或导航所生成的集合上的 `AnyElement`。  
  
-   使用接受元素选择器的分组方法的 LINQ 查询。  
  
-   显式指定了 CROSS APPLY 或 OUTER APPLY 的查询  
  
-   在 REF 构造上具有 DEREF 构造的查询。  
  
## SKIP 运算符  
 如果使用的是 [!INCLUDE[ssVersion2000](../../../../../includes/ssversion2000-md.md)]，则对非键列同时使用 SKIP 和 ORDER BY 可能会返回不正确的结果。  如果非键列中有重复数据，那么跳过的行数可能多于指定的行数。  这是由于 [!INCLUDE[ssVersion2000](../../../../../includes/ssversion2000-md.md)] 对 SKIP 的解释方式造成的。  例如，在下面的查询中，如果 `E.NonKeyColumn` 有重复值，则跳过的行可能超过 5 行：  
  
```  
SELECT [E] FROM Container.EntitySet AS [E] ORDER BY [E].[NonKeyColumn] DESC SKIP 5L  
```  
  
## 以正确的 SQL Server 版本为目标  
 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]以基于 SQL Server 版本（在存储模型 \(.ssdl\) 文件中 Schema 元素的 `ProviderManifestToken` 特性中指定）的 [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] 查询为目标。  您实际连接到的 SQL Server 的版本可能不是这一版本。  例如，如果您使用的是 SQL Server 2005，但 `ProviderManifestToken` 特性设置为 2008，则可能无法在服务器上执行生成的 [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] 查询。例如，在 SQL Server 的早期版本上，无法执行使用了 SQL Server 2008 所引入的新日期时间类型的查询。  如果您使用的是 SQL Server 2005，但 `ProviderManifestToken` 属性设置为 2000，则生成的 [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] 查询可能不是最佳的，您也可能收到指出该查询不受支持的异常消息。  有关更多信息，请参见本主题前面的“CROSS 和 OUTER APPLY 运算符”部分。  
  
 某些数据库行为取决于为数据库设置的兼容级别。  如果 `ProviderManifestToken` 属性设置为 2005 并且 SQL Server 版本为 2005，但数据库的兼容级别设置为“80”\(SQL Server 2000\)，则生成的 [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] 将以 SQL Server 2005 为目标，但可能会因兼容级别设置而无法正常执行。  例如，如果 ORDER BY 列表中的列名与选择器中的列名相同，则可能会丢失排序信息。  
  
## 投影中的嵌套查询  
 投影子句中的嵌套查询可在服务器上转换为笛卡尔积查询。  在某些后端服务器（包括 SLQ Server）上，这会导致 TempDB 表变得相当大。  这样会降低服务器性能。  
  
 下面是投影子句中嵌套查询的示例：  
  
```  
SELECT c, (SELECT c, (SELECT c FROM AdventureWorksModel.Vendor AS c  ) As Inner2 FROM AdventureWorksModel.JobCandidate AS c  ) As Inner1 FROM AdventureWorksModel.EmployeeDepartmentHistory AS c  
```  
  
## 服务器生成的 GUID 标识值  
 [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]支持服务器生成的 GUID 类型标识值，但提供程序必须支持在插入行后返回服务器生成的标识值。  从 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 2005 开始，可以通过 [OUTPUT 子句](http://go.microsoft.com/fwlink/?LinkId=169400)（可能为英文网页）在 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 数据库中返回服务器生成的 GUID 类型。  
  
## 请参阅  
 [用于实体框架的 SqlClient](../../../../../docs/framework/data/adonet/ef/sqlclient-for-the-entity-framework.md)   
 [LINQ to Entities 的已知问题和注意事项](../../../../../docs/framework/data/adonet/ef/language-reference/known-issues-and-considerations-in-linq-to-entities.md)