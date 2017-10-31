---
title: "System.TimeSpan 方法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9333fee8-1454-4374-855b-8c14c002f48f
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# System.TimeSpan 方法
对 <xref:System.TimeSpan?displayProperty=fullName> 的成员支持在很大程度上取决于您正在使用的 .NET Framework 和 Microsoft SQL Server 的版本。  
  
 当某个方法、运算符或属性不受支持时；这意味着 LINQ to SQL 将无法转换成员以在 SQL Server 上执行。  您可能仍可以在代码中使用这些成员。  不过，在将查询转换为 Transact\-SQL 之前或在已经从数据库中检索结果之后，必须对这些成员进行计算。  
  
## 以前的限制  
 将 LINQ to SQL 与 .NET Framework 3.5 SP1 之前的 .NET Framework 版本一起使用时，您无法将 SQL Server 数据库字段映射到 <xref:System.TimeSpan?displayProperty=fullName>。  但是，支持对 <xref:System.TimeSpan> 的操作，原因是可以通过 <xref:System.DateTime> 减法运算返回 <xref:System.TimeSpan> 值或将这些值作为文本或绑定变量引入表达式。  
  
## 支持的 System.TimeSpan 方法支持  
 以下受 LINQ to SQL 支持的方法、运算符和属性可供您在 LINQ to SQL 查询中使用。  在对象模型或外部映射文件中进行映射后，LINQ to SQL 允许您从 LINQ to SQL 查询内调用许多 <xref:System.TimeSpan?displayProperty=fullName> 成员。  
  
|支持的 <xref:System.TimeSpan> 方法|支持的 <xref:System.TimeSpan> 运算符|支持的 <xref:System.TimeSpan> 属性|  
|-------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.TimeSpan.Compare%2A>|<xref:System.TimeSpan.op_Equality%2A>|<xref:System.TimeSpan.Days%2A>|  
|<xref:System.TimeSpan.CompareTo%28System.TimeSpan%29>|<xref:System.TimeSpan.op_GreaterThan%2A>|<xref:System.TimeSpan.Hours%2A>|  
|<xref:System.TimeSpan.Duration%2A>|<xref:System.TimeSpan.op_GreaterThanOrEqual%2A>|<xref:System.TimeSpan.MaxValue>|  
|<xref:System.TimeSpan.Equals%28System.TimeSpan%2CSystem.TimeSpan%29>|<xref:System.TimeSpan.op_Inequality%2A>|<xref:System.TimeSpan.Milliseconds%2A>|  
|<xref:System.TimeSpan.Equals%28System.TimeSpan%29>|<xref:System.TimeSpan.op_LessThan%2A>|<xref:System.TimeSpan.Minutes%2A>|  
||<xref:System.TimeSpan.op_LessThanOrEqual%2A>|<xref:System.TimeSpan.MinValue%2A>|  
  
> [!NOTE]
>  需要安装 .NET Framework 3.5 SP1 和更高版本，才能使用 LINQ to SQL 将 <xref:System.TimeSpan?displayProperty=fullName> 映射到 SQL `TIME` 列。  SQL `TIME` 数据类型仅在 Microsoft SQL Server 2008 和更高版本中提供。  
  
### 加法和减法  
 尽管 CLR <xref:System.TimeSpan?displayProperty=fullName> 类型支持加减运算，但 SQL `TIME` 类型不支持。  因此，将 LINQ to SQL 查询映射到 SQL `TIME` 类型后，如果这些查询尝试执行加减运算，则将生成错误。  您可以在 [SQL\-CLR 类型映射](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md) 中找到有关使用 SQL 日期和时间类型的其他注意事项。  
  
## 请参阅  
 [查询概念](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)   
 [创建对象模型](../../../../../../docs/framework/data/adonet/sql/linq/creating-the-object-model.md)   
 [SQL\-CLR 类型映射](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)   
 [数据类型和函数](../../../../../../docs/framework/data/adonet/sql/linq/data-types-and-functions.md)