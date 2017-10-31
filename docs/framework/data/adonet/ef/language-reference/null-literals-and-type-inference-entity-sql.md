---
title: "Null 文本和类型推理 (Entity SQL) | Microsoft Docs"
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
ms.assetid: edd56afb-af1b-4e7d-b210-cb8998143426
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Null 文本和类型推理 (Entity SQL)
Null 文本与 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 类型系统中的任何类型都兼容。  但是，为了正确进行 Null 文本类型推理，[!INCLUDE[esql](../../../../../../includes/esql-md.md)] 对何处可以使用 Null 文本实施某些约束。  
  
## 类型化 Null  
 类型化 Null 可以在任意位置使用。  类型化 Null 是已知的，因此不需要类型推理。  例如，使用下面的 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 构造可以构造 Int16 类型的 Null。  
  
 `(cast(null as Int16))`  
  
## 自由浮动 Null 文本  
 自由浮动 Null 文本的用法如下：  
  
-   用作 CAST 或 TREAT 表达式的参数。  建议用这种方式生成类型化 Null 表达式。  
  
-   用作方法或函数的参数。  标准重载规则适用。  
  
-   用作算术表达式（例如 \+、\- 或 \/）的一个参数。  其他参数不能为 Null 文本，否则不能进行类型推理。  
  
-   用作逻辑表达式（AND、OR 或 NOT）的任何参数。  所有参数都已知为类型 Boolean。  
  
-   用作 IS NULL 或 IS NOT NULL 表达式的参数。  
  
-   用作 LIKE 表达式的一个或多个参数。  所有参数都应为字符串。  
  
-   用作命名类型构造函数的一个或多个参数。  
  
-   用作多集构造函数的一个或多个参数。  多集构造函数至少有一个参数必须为非 Null 文本的表达式。  
  
-   用作 CASE 表达式中的一个或多个 THEN 或 ELSE 表达式。  CASE 表达式中至少有一个 THEN 或 ELSE 表达式必须为非 Null 文本的表达式。  
  
 其他情况下不能使用自由浮动 Null 文本。  例如，它们不能用作行构造函数的参数。  
  
## 请参阅  
 [Entity SQL 概述](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)