---
title: "基本数据类型 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eca2c472-9548-4800-bd31-5d8d9f11752b
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 基本数据类型
因为 LINQ to SQL 查询转换为 Transact\-SQL 后才在 Microsoft SQL Server 上执行。  LINQ to SQL 支持针对基本数据类型的许多和 SQL Server 一样的内置功能。  
  
## 强制转换  
 支持从源 CLR 类型到目标 CLR 类型的隐式或显式强制转换，前提是在 SQL Server 中存在类似的有效转换。  有关 CLR 强制转换的更多信息，请参见 [CType 函数](../Topic/CType%20Function%20\(Visual%20Basic\).md) \([!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)]\) 和 [as](../Topic/as%20\(C%23%20Reference\).md)。  转换后，强制转换会更改对 CLR 表达式执行的操作的行为，使之与自然映射到目标类型的其他 CLR 表达式的行为匹配。强制转换还可以在继承映射的上下文中进行。  可以将对象强制转换成更具体的实体子类型，以便可以访问其特定于子类型的数据。  
  
## 相等运算符  
 LINQ to SQL 支持以下 LINQ to SQL 查询内部的基本数据类型上的相等运算符：  
  
-   相等和不相等运算符：支持对数值 <xref:System.Boolean>、<xref:System.DateTime> 和 <xref:System.TimeSpan> 类型的相等和不相等运算符。  有关 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 运算符 `=` 和 `<>` 的更多信息，请参见[比较运算符](../Topic/Comparison%20Operators%20\(Visual%20Basic\).md)。有关 C\# 比较运算符 `==` 和 `!=` 的更多信息，请分别参见 [\=\= 运算符](../Topic/==%20Operator%20\(C%23%20Reference\).md)和 [\!\= 运算符](../Topic/!=%20Operator%20\(C%23%20Reference\).md)  
  
-   Is 运算符：在使用继承映射时，`IS` 运算符具有受支持的转换形式。  可以使用该运算符，而不用通过直接测试鉴别器列来确定对象是否属于特定实体类型，该运算符会转换为对鉴别器列的检查。  有关 Visual Basic 和 C\# Is 运算符的更多信息，请参见 [Is 运算符](../Topic/Is%20Operator%20\(Visual%20Basic\).md) 和 [is](../Topic/is%20\(C%23%20Reference\).md)。  
  
## 请参阅  
 [SQL\-CLR 类型映射](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)   
 [数据类型和函数](../../../../../../docs/framework/data/adonet/sql/linq/data-types-and-functions.md)