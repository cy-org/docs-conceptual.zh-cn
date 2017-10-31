---
title: "数据类型和函数 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 683413c5-0312-4e60-8619-9a97bdc6e62a
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 数据类型和函数
下表列出的主题介绍了对公共语言运行库 \(CLR\) 的成员、构造和强制转换的 LINQ to SQL 支持。  受支持的成员和构造可以在 LINQ to SQL 查询中使用。  
  
 表中不受支持的项表示 LINQ to SQL 无法转换 CLR 成员、构造或强制转换以供在 SQL Server 上执行。  您可能仍可以在您的代码中使用这些项，但是在查询转换为 Transact\-SQL 之前或结果已经从数据库中检索后必须对其进行计算。  
  
|主题|描述|  
|--------|--------|  
|[SQL\-CLR 类型映射](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)|提供 CLR 类型和 SQL Server 类型之间的详细映射矩阵。|  
|[基本数据类型](../../../../../../docs/framework/data/adonet/sql/linq/basic-data-types.md)|总结与 [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] 之间的行为差异。|  
|[Boolean 数据类型](../../../../../../docs/framework/data/adonet/sql/linq/boolean-data-types.md)|总结与 [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] 之间的行为差异。|  
|[Null 语义](../../../../../../docs/framework/data/adonet/sql/linq/null-semantics.md)|提供指向讨论 null 和可以为 null 问题的 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 主题的链接。|  
|[数值运算符和比较运算符](../../../../../../docs/framework/data/adonet/sql/linq/numeric-and-comparison-operators.md)|总结与 [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] 之间的行为差异。|  
|[顺序运算符](../../../../../../docs/framework/data/adonet/sql/linq/sequence-operators.md)|总结与 [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] 之间的行为差异。|  
|[System.Convert 方法](../../../../../../docs/framework/data/adonet/sql/linq/system-convert-methods.md)|总结与 [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] 之间的行为差异。|  
|[System.DateTime 方法](../../../../../../docs/framework/data/adonet/sql/linq/system-datetime-methods.md)|介绍对 <xref:System.DateTime?displayProperty=fullName> 结构的成员的 LINQ to SQL 支持。|  
|[System.DateTimeOffset 方法](../../../../../../docs/framework/data/adonet/sql/linq/system-datetimeoffset-methods.md)|介绍对 <xref:System.DateTimeOffset?displayProperty=fullName> 结构的成员的 LINQ to SQL 支持。|  
|[System.Math 方法](../../../../../../docs/framework/data/adonet/sql/linq/system-math-methods.md)|总结与 [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] 之间的行为差异。|  
|[System.Object 方法](../../../../../../docs/framework/data/adonet/sql/linq/system-object-methods.md)|总结与 [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] 之间的行为差异。|  
|[System.String 方法](../../../../../../docs/framework/data/adonet/sql/linq/system-string-methods.md)|总结与 [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] 之间的行为差异。|  
|[System.TimeSpan 方法](../../../../../../docs/framework/data/adonet/sql/linq/system-timespan-methods.md)|介绍对 <xref:System.TimeSpan?displayProperty=fullName> 结构的成员的 LINQ to SQL 支持。|  
|[不支持的功能](../../../../../../docs/framework/data/adonet/sql/linq/unsupported-functionality.md)|介绍 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 不支持的功能。|  
  
## 请参阅  
 [SQL\-CLR 类型不匹配](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mismatches.md)   
 [参考](../../../../../../docs/framework/data/adonet/sql/linq/reference.md)   
 [.NET Framework Class Library in Visual Studio](http://msdn.microsoft.com/zh-cn/a03e374c-3d5c-4169-937b-49857ab273ae)