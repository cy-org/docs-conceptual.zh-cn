---
title: "在 .NET Framework 中分析其他字符串 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Char 数据类型，分析字符串"
  - "枚举 [.NET Framework]，分析字符串"
  - "基类型，分析字符串"
  - "分析字符串，其他字符串"
  - "Boolean 数据类型，分析字符串"
ms.assetid: d139bc00-3c4e-4d78-ac9a-5c951b258d28
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# 在 .NET Framework 中分析其他字符串
除了数值字符串和 <xref:System.DateTime> 字符串外，还可以分析将 <xref:System.Char>、<xref:System.Boolean> 和 <xref:System.Enum> 类型表示为数据类型的字符串。  
  
## Char  
 如果要将包含单个字符的字符串转换为其 Unicode 值，与 **Char** 数据类型相关的静态分析方法十分有用。  下面的代码示例将字符串分析为 Unicode 字符。  
  
 [!code-cpp[Conceptual.String.Parse#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.parse/cpp/parse.cpp#2)]
 [!code-csharp[Conceptual.String.Parse#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.parse/cs/parse.cs#2)]
 [!code-vb[Conceptual.String.Parse#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.parse/vb/parse.vb#2)]  
  
## Boolean  
 **Boolean** 数据类型包含 **Parse** 方法，此方法可用于将表示 Boolean 值的字符串转换为实际 **Boolean** 类型。  此方法不区分大小写，可成功分析包含“True”或“False”字符的字符串。与 **Boolean** 类型相关的 **Parse** 方法还可以分析周围有空格的字符串。  如果传递任何其他字符串，则将引发 <xref:System.FormatException>。  
  
 下面的代码示例使用 **Parse** 方法将字符串转换为 Boolean 值。  
  
 [!code-cpp[Conceptual.String.Parse#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.parse/cpp/parse.cpp#3)]
 [!code-csharp[Conceptual.String.Parse#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.parse/cs/parse.cs#3)]
 [!code-vb[Conceptual.String.Parse#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.parse/vb/parse.vb#3)]  
  
## Enumeration  
 您可以使用静态 **Parse** 方法将字符串的值初始化为枚举类型。  此方法接受正在分析的枚举类型、要分析的字符串和指明分析是否区分大小写的可选 Boolean 标志。  分析的字符串可包含几个用逗号隔开的值，值的前后可留有一个或多个空格。  当字符串包含多个值时，返回对象的值是所有与按位“或”运算组合的指定值。  
  
 下面的示例使用 **Parse** 方法将字符串表示形式转换为枚举值。  <xref:System.DayOfWeek> 枚举从字符串中初始化为 **Thursday**。  
  
 [!code-cpp[Conceptual.String.Parse#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.parse/cpp/parse.cpp#4)]
 [!code-csharp[Conceptual.String.Parse#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.parse/cs/parse.cs#4)]
 [!code-vb[Conceptual.String.Parse#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.parse/vb/parse.vb#4)]  
  
## 请参阅  
 [分析字符串](../../../docs/standard/base-types/parsing-strings.md)   
 [格式化类型](../../../docs/standard/base-types/formatting-types.md)   
 [.NET Framework 中的类型转换](../../../docs/standard/base-types/type-conversion.md)