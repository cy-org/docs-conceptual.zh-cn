---
title: "在 .NET Framework 中分析数值字符串 | Microsoft Docs"
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
  - "分析字符串，数值字符串"
  - "数值字符串"
  - "枚举 [.NET Framework]，分析字符串"
  - "基类型，分析字符串"
ms.assetid: e39324ee-72e5-42d4-a80d-bf3ee7fc6c59
caps.latest.revision: 20
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 20
---
# 在 .NET Framework 中分析数值字符串
所有数值类型都具有两种静态分析方法（`Parse` 和 `TryParse`），可以使用这些方法将数字的字符串表示形式转换为数值类型。  您可以使用这些方法分析使用 [标准数字格式字符串](../../../docs/standard/base-types/standard-numeric-format-strings.md) 和 [自定义数字格式字符串](../../../docs/standard/base-types/custom-numeric-format-strings.md) 中记录的格式字符串生成的字符串。  默认情况下，`Parse` 和 `TryParse` 方法可成功地将只包含十进制整数的字符串转换为整数值。  它们可以成功地将包含整数和小数十进制数、组分隔符和小数分隔符的字符串转换为浮点值。  如果操作失败，`Parse` 方法将引发异常，而 `TryParse` 方法会返回 `false`。  
  
## 分析和格式提供程序  
 通常，数值的字符串表示形式因区域性而异。  数值字符串的元素都会因区域性而异，包括如货币符号、组（或千位）分隔符、和所有被区域性改变的十进制分隔符。  分析方法隐式或显式地使用识别这些特定区域性差异的格式提供程序。  如果没有在对 `Parse` 或 `TryParse` 方法的调用中指定格式提供程序，将使用与当前线程区域性（由 <xref:System.Globalization.NumberFormatInfo.CurrentInfo%2A?displayProperty=fullName> 属性返回的 <xref:System.Globalization.NumberFormatInfo> 对象）相关联的格式提供程序。  
  
 格式提供程序由 <xref:System.IFormatProvider> 实现表示。  此接口具有一个成员（<xref:System.IFormatProvider.GetFormat%2A> 方法），该成员的唯一参数是表示要设置格式的类型的 <xref:System.Type> 对象。  此方法返回提供格式设置信息的对象。  .NET Framework 支持以下两种用于分析数值字符串的 <xref:System.IFormatProvider> 实现：  
  
-   <xref:System.Globalization.CultureInfo> 对象，其 <xref:System.Globalization.CultureInfo.GetFormat%2A?displayProperty=fullName> 方法返回提供特定区域性格式设置信息的 <xref:System.Globalization.NumberFormatInfo> 对象。  
  
-   <xref:System.Globalization.NumberFormatInfo> 对象，其 <xref:System.Globalization.NumberFormatInfo.GetFormat%2A?displayProperty=fullName> 方法返回其自身。  
  
 以下示例尝试将数组中的每个字符串转换为 <xref:System.Double> 值。  它首先尝试使用反映英语（美国）区域性约定的格式提供程序来分析字符串。  如果此操作引发 <xref:System.FormatException>，它将尝试使用反映法语（法国）区域性约定的格式提供程序来分析字符串。  
  
 [!code-csharp[Parsing.Numbers#1](../../../samples/snippets/csharp/VS_Snippets_CLR/parsing.numbers/cs/formatproviders1.cs#1)]
 [!code-vb[Parsing.Numbers#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/parsing.numbers/vb/formatproviders1.vb#1)]  
  
## 分析和 NumberStyles 值  
 分析操作可处理的样式元素（例如空格、组分隔符和小数分隔符）由 <xref:System.Globalization.NumberStyles> 枚举值定义。  默认情况下，使用 <xref:System.Globalization.NumberStyles?displayProperty=fullName> 值来分析表示整数值的字符串，该值只允许数字、前导和尾随空格以及前导符号。  可使用 <xref:System.Globalization.NumberStyles?displayProperty=fullName> 和 <xref:System.Globalization.NumberStyles?displayProperty=fullName> 值的组合来分析表示浮点值的字符串；这种复合样式允许使用数字以及前导和尾随空格、前导符号、小数分隔符、组分隔符以及指数。  通过调用包括 <xref:System.Globalization.NumberStyles> 类型参数的 `Parse` 或 `TryParse` 方法的重载，并设置一个或多个 <xref:System.Globalization.NumberStyles> 标记，您可以控制可显示在字符串中的样式元素，以确保分析操作成功。  
  
 例如，包含组分隔符的字符串使用 <xref:System.Int32.Parse%28System.String%29?displayProperty=fullName> 方法不能转换为 <xref:System.Int32> 值。  但是，如果使用 <xref:System.Globalization.NumberStyles?displayProperty=fullName> 标记，可成功转换，如下面的示例所阐释。  
  
 [!code-csharp[Parsing.Numbers#2](../../../samples/snippets/csharp/VS_Snippets_CLR/parsing.numbers/cs/styles1.cs#2)]
 [!code-vb[Parsing.Numbers#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/parsing.numbers/vb/styles1.vb#2)]  
  
> [!WARNING]
>  分析操作始终使用特定区域性的格式设置约定。  如果没有通过传递 <xref:System.Globalization.CultureInfo> 或 <xref:System.Globalization.NumberFormatInfo> 对象来指定区域性，会使用与当前线程相关联的区域性。  
  
 下表列出了 <xref:System.Globalization.NumberStyles> 枚举的成员并描述了它们对分析操作产生的影响。  
  
|NumberStyles 值|对要分析的字符串的影响|  
|--------------------|-----------------|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|仅允许数字。|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|允许小数分隔符和小数位。  对于整数值，只允许将零作为小数位。  有效的小数分隔符由 <xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A?displayProperty=fullName> 或 <xref:System.Globalization.NumberFormatInfo.CurrencyDecimalSeparator%2A?displayProperty=fullName> 属性确定。|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|“e”或“E”字符可用来指示指数计数法。  有关其他信息，请参见 <xref:System.Globalization.NumberStyles>。|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|允许前导空格。|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|允许尾随空格。|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|数字的前面可带有正负号。|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|数字的后面可带有正负号。|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|可使用括号表示负值。|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|允许组分隔符。  组分隔符由 <xref:System.Globalization.NumberFormatInfo.NumberGroupSeparator%2A?displayProperty=fullName> 或 <xref:System.Globalization.NumberFormatInfo.CurrencyGroupSeparator%2A?displayProperty=fullName> 属性确定。|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|允许货币符号。  货币符号由 <xref:System.Globalization.NumberFormatInfo.CurrencySymbol%2A?displayProperty=fullName> 属性定义。|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|要分析的字符串被解释为十六进制数。  它可以包括十六进制数字 0\-9、A\-F 和 a\-f。  此标记只用来分析整数值。|  
  
 此外，<xref:System.Globalization.NumberStyles> 枚举还提供了以下复合样式，其中包括多个 <xref:System.Globalization.NumberStyles> 标记。  
  
|复合 NumberStyles 值|包括成员|  
|-----------------------|----------|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|包括 <xref:System.Globalization.NumberStyles?displayProperty=fullName>、<xref:System.Globalization.NumberStyles?displayProperty=fullName> 和 <xref:System.Globalization.NumberStyles?displayProperty=fullName> 样式。  这是用来分析整数值的默认样式。|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|包括 <xref:System.Globalization.NumberStyles?displayProperty=fullName>、<xref:System.Globalization.NumberStyles?displayProperty=fullName>、<xref:System.Globalization.NumberStyles?displayProperty=fullName>、<xref:System.Globalization.NumberStyles?displayProperty=fullName>、<xref:System.Globalization.NumberStyles?displayProperty=fullName> 和 <xref:System.Globalization.NumberStyles?displayProperty=fullName> 样式。|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|包括 <xref:System.Globalization.NumberStyles?displayProperty=fullName>、<xref:System.Globalization.NumberStyles?displayProperty=fullName>、<xref:System.Globalization.NumberStyles?displayProperty=fullName>、 <xref:System.Globalization.NumberStyles?displayProperty=fullName> 和 <xref:System.Globalization.NumberStyles?displayProperty=fullName> 样式。|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|包括除 <xref:System.Globalization.NumberStyles?displayProperty=fullName> 和 <xref:System.Globalization.NumberStyles?displayProperty=fullName> 以外的其他所有样式。|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|包括除 <xref:System.Globalization.NumberStyles?displayProperty=fullName> 以外的其他所有样式。|  
|<xref:System.Globalization.NumberStyles?displayProperty=fullName>|包括 <xref:System.Globalization.NumberStyles?displayProperty=fullName>、<xref:System.Globalization.NumberStyles?displayProperty=fullName> 和 <xref:System.Globalization.NumberStyles?displayProperty=fullName> 样式。|  
  
## 分析和 Unicode 数字  
 Unicode 标准为各种编写系统中的数字定义了码位。  例如，从 U\+0030 到 U\+0039 的码位表示从 0 到 9 的基本拉丁文数字，从 U\+09E6 到 U\+09EF 的码位表示从 0 到 9 的孟加拉文数字，而从 U\+FF10 到 U\+FF19 的码位表示从 0 到 9 的全角数字。  但是，分析方法唯一识别的数字是基本拉丁文数字 0\-9 （码位从 U\+0030 到 U\+0039）。  如果将数值分析方法传递给包含任何其他数字的字符串，该方法将引发 <xref:System.FormatException>。  
  
 以下代码示例使用 <xref:System.Int32.Parse%2A?displayProperty=fullName> 方法来分析由不同编写系统的数字组成的字符串。  正如示例输出所示，虽然尝试分析基本拉丁文数字获得成功，但分析全角、阿拉伯 \- 印度文以及孟加拉文数字的尝试将失败。  
  
 [!code-csharp[Parsing.Numbers#3](../../../samples/snippets/csharp/VS_Snippets_CLR/parsing.numbers/cs/unicode1.cs#3)]
 [!code-vb[Parsing.Numbers#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/parsing.numbers/vb/unicode1.vb#3)]  
  
## 请参阅  
 <xref:System.Globalization.NumberStyles>   
 [分析字符串](../../../docs/standard/base-types/parsing-strings.md)   
 [格式化类型](../../../docs/standard/base-types/formatting-types.md)