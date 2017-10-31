---
title: "在 .NET Framework 中分析日期和时间字符串 | Microsoft Docs"
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
  - "基类型, 分析字符串"
  - "日期和时间字符串"
  - "DateTime 对象"
  - "枚举 [.NET Framework], 分析字符串"
  - "ParseExact 方法"
  - "分析字符串, 日期和时间字符串"
  - "时间字符串"
ms.assetid: 43bae51e-9b1d-41a6-a187-772c0d096d90
caps.latest.revision: 24
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 24
---
# 在 .NET Framework 中分析日期和时间字符串
分析方法将日期和时间的字符串表示形式转换为等效的 <xref:System.DateTime> 对象。  <xref:System.DateTime.Parse%2A> 和 <xref:System.DateTime.TryParse%2A> 方法可转换日期和时间的若干常用表示形式的任何一种。  <xref:System.DateTime.ParseExact%2A> 和 <xref:System.DateTime.TryParseExact%2A> 方法可转换符合日期和时间格式字符串所指定的模式的字符串表示形式。（请参见有关[标准日期和时间格式字符串](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)和[自定义日期和时间格式字符串](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)的主题。）  
  
 分析受格式提供程序的属性影响，该格式提供程序将提供诸如用作日期和时间分隔符的字符串以及月份、日和纪元的名称等信息。  格式提供程序是当前的 <xref:System.Globalization.DateTimeFormatInfo> 对象，其由当前线程区域性隐式提供或由分析方法的 <xref:System.IFormatProvider> 参数显式提供。  对于 <xref:System.IFormatProvider> 参数，可指定一个表示区域性的 <xref:System.Globalization.CultureInfo> 对象或指定一个 <xref:System.Globalization.DateTimeFormatInfo> 对象。  
  
 要分析的日期的字符串表示形式必须包括月份并至少带有日或年份之一。  时间的字符串表示形式必须包括小时并至少带有分钟或 AM\/PM 指示符之一。  但是分析会提供默认值以用于可能的省略组成部分。  缺少日期时将默认为当前日期，缺少年份时将默认为当前年份，缺少月中日期时将默认为该月第一天，缺少时间时将默认为午夜。  
  
 如果字符串表示形式仅指定了时间，则分析将返回一个 <xref:System.DateTime> 对象，它的 <xref:System.DateTime.Year%2A>、<xref:System.DateTime.Month%2A> 和 <xref:System.DateTime.Day%2A> 属性设置为 <xref:System.DateTime.Today%2A> 属性的对应值。  但是，如果在分析方法中指定了 <xref:System.Globalization.DateTimeStyles> 常量，则得到的年份、月份和日属性将设置为值 `1`。  
  
 除了日期和时间组成部分外，日期和时间的字符串表示形式还可以包括一个偏移量，以指示该时间与协调世界时 \(UTC\) 之差。  例如，字符串“2\/14\/2007 5:32:00 \-7:00”定义的时间比 UTC 早七个小时。  如果从时间的字符串表示形式中省略了偏移量，则分析将返回一个 <xref:System.DateTime.Kind%2A> 属性设置为 <xref:System.DateTimeKind?displayProperty=fullName> 的 <xref:System.DateTime> 对象。  如果指定了偏移量，则分析将返回一个 <xref:System.DateTime.Kind%2A> 属性设置为 <xref:System.DateTimeKind> 且值已调整为计算机的本地时区的 <xref:System.DateTime> 对象。  可以通过与分析方法一起使用 <xref:System.Globalization.DateTimeStyles> 常量来修改此行为。  
  
 格式提供程序还可用于解释不明确的数值日期。  例如，由字符串“02\/03\/04”所表示的日期中与月份、日和年份对应的组成部分不明确。  在这种情况下，将根据格式提供程序中相似日期格式的顺序解释各组成部分。  
  
## Parse  
 下面的代码示例阐释如何使用 **Parse** 方法将字符串转换为 **DateTime**。  此示例使用与当前线程相关的区域性来执行分析。  如果与当前区域性关联的 <xref:System.Globalization.CultureInfo> 无法分析输入字符串，则会引发 <xref:System.FormatException>。  
  
 [!code-csharp[Parsing.DateAndTime#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Parsing.DateAndTime/cs/Example.cs#1)]
 [!code-vb[Parsing.DateAndTime#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Parsing.DateAndTime/vb/Example.vb#1)]  
  
 您也可以将 **CultureInfo** 集指定为该对象定义的某个区域性，或是指定由 <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=fullName> 属性返回的标准 <xref:System.Globalization.DateTimeFormatInfo> 对象之一。  下面的代码示例使用格式提供程序将德语字符串分析为 **DateTime** 对象。  表示 de\-DE 区域性的 **CultureInfo** 经过定义后，与被分析的字符串一起传递，这样可确保成功分析此特定字符串。  这样就排除了 **CurrentThread** 的 **CurrentCulture** 中的任何设置。  
  
 [!code-csharp[Parsing.DateAndTime#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Parsing.DateAndTime/cs/Example2.cs#2)]
 [!code-vb[Parsing.DateAndTime#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Parsing.DateAndTime/vb/Example2.vb#2)]  
  
 不过，虽然可以使用 <xref:System.DateTime.Parse%2A> 方法的重载指定自定义格式提供程序，但该方法并不支持使用非标准的格式提供程序。  若要分析以非标准格式表示的日期和时间，请改用 <xref:System.DateTime.ParseExact%2A> 方法。  
  
 下面的代码示例使用 <xref:System.Globalization.DateTimeStyles> 枚举来指定不应将当前日期和时间信息添加至字符串未定义的字段的 **DateTime**。  
  
 [!code-csharp[Parsing.DateAndTime#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Parsing.DateAndTime/cs/Example3.cs#3)]
 [!code-vb[Parsing.DateAndTime#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Parsing.DateAndTime/vb/Example3.vb#3)]  
  
## ParseExact  
 <xref:System.DateTime.ParseExact%2A?displayProperty=fullName> 方法可将符合指定字符串模式的字符串转换为 **DateTime** 对象。  向此方法传递非指定格式的字符串时，会引发 <xref:System.FormatException>。  您可以指定一种标准日期和时间格式说明符，或指定自定义日期和时间格式说明符的限定组合。  使用自定义格式说明符，可以构造自定义识别字符串。  有关说明符的解释，请参见有关[标准日期和时间格式字符串](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)和[自定义日期和时间格式字符串](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)的主题。  
  
 <xref:System.DateTime.ParseExact%2A> 方法的每个重载还具有一个 <xref:System.IFormatProvider> 参数，此参数通常提供有关字符串格式的区域性特定的信息。  通常情况下，此 <xref:System.IFormatProvider> 对象是一个表示标准区域性的 <xref:System.Globalization.CultureInfo> 对象，或是一个由 <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=fullName> 属性返回的 <xref:System.Globalization.DateTimeFormatInfo> 对象。  但是，与其他日期和时间分析函数不同，此方法还支持定义非标准日期和时间格式的 <xref:System.IFormatProvider>。  
  
 在下面的代码示例中，依次将字符串对象、格式说明符、**CultureInfo** 对象传递至 **ParseExact** 方法进行分析。  此 **ParseExact** 方法只能分析在 en\-US 区域性中显示长日期模式的字符串。  
  
 [!code-csharp[Parsing.DateAndTime#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Parsing.DateAndTime/cs/Example4.cs#4)]
 [!code-vb[Parsing.DateAndTime#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Parsing.DateAndTime/vb/Example4.vb#4)]  
  
## 请参阅  
 [分析字符串](../../../docs/standard/base-types/parsing-strings.md)   
 [格式化类型](../../../docs/standard/base-types/formatting-types.md)   
 [.NET Framework 中的类型转换](../../../docs/standard/base-types/type-conversion.md)