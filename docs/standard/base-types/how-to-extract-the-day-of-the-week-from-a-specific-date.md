---
title: "如何：从特定日期中提取星期几 | Microsoft Docs"
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
  - "格式设置 [.NET Framework]，日期"
  - "DateTime.DayOfWeek 属性"
  - "DateTime.ToString 方法"
  - "日期 [.NET Framework], 检索周信息"
  - "DateTimeOffset.DayOfWeek 属性"
  - "日期 [.NET Framework], 星期几"
  - "Weekday 函数"
  - "星期几 [.NET Framework]"
  - "提取星期几"
  - "星期几名称"
  - "WeekdayName 函数"
  - "数字 [.NET Framework], 星期几"
  - "格式设置 [.NET Framework], 时间"
  - "DateTimeOffset.ToString 方法"
  - "完整星期几名称"
ms.assetid: 1c9bef76-5634-46cf-b91c-9b9eb72091d7
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：从特定日期中提取星期几
利用 .NET Framework，可以很容易地确定某个特定日期是星期几，以及显示某个特定日期的本地化星期几名称。 指示与特定日期相对应的星期几的枚举值可以从 <xref:System.DateTime.DayOfWeek%2A> 或 <xref:System.DateTimeOffset.DayOfWeek%2A> 属性中获取。 与此不同的是，检索星期几名称是一项格式化操作，可通过调用格式化方法来执行，例如日期和时间值的 `ToString` 方法或 <xref:System.String.Format%2A?displayProperty=fullName> 方法。 本主题演示如何执行这些格式化操作。  
  
### 从特定日期中提取指示星期几的数字  
  
1.  如果要使用日期的字符串表示形式，请使用静态 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 方法将其转换为 <xref:System.DateTime.Parse%2A?displayProperty=fullName> 或 <xref:System.DateTimeOffset.Parse%2A?displayProperty=fullName> 值。  
  
2.  使用 <xref:System.DateTime.DayOfWeek%2A?displayProperty=fullName> 或 <xref:System.DateTimeOffset.DayOfWeek%2A?displayProperty=fullName> 属性检索指示星期几的 <xref:System.DayOfWeek> 值。  
  
3.  如有必要，可将 <xref:System.DayOfWeek> 值强制转换（在 C\# 中）或转换（在 Visual Basic 中）为整数。  
  
 下面的示例将显示一个整数，用于表示特定日期的星期几。  
  
 [!code-csharp[Formatting.Howto.WeekdayName#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/weekdaynumber7.cs#7)]
 [!code-vb[Formatting.Howto.WeekdayName#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/weekdaynumber7.vb#7)]  
  
### 从特定日期中提取缩写的星期几名称  
  
1.  如果要使用日期的字符串表示形式，请使用静态 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 方法将其转换为 <xref:System.DateTime.Parse%2A?displayProperty=fullName> 或 <xref:System.DateTimeOffset.Parse%2A?displayProperty=fullName> 值。  
  
2.  你可以提取当前区域性或特定区域性的缩写的星期几名称：  
  
    1.  若要提取当前区域性的缩写的星期几名称，请调用日期和时间值的 <xref:System.DateTime.ToString%28System.String%29?displayProperty=fullName> 或 <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=fullName> 实例方法，并以 `format` 参数的形式传递字符串“ddd”。 下面的示例演示 <xref:System.DateTime.ToString%28System.String%29> 方法的调用。  
  
         [!code-csharp[Formatting.Howto.WeekdayName#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/abbrname1.cs#1)]
         [!code-vb[Formatting.Howto.WeekdayName#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/abbrname1.vb#1)]  
  
    2.  若要提取特定区域性的缩写的星期几名称，请调用日期和时间值的 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName> 或 <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName> 实例方法。 同时以 `format` 参数形式传递字符串“ddd”。 以 <xref:System.Globalization.CultureInfo> 参数的形式传递表示要检索其星期几名称的区域性的 <xref:System.Globalization.DateTimeFormatInfo> 或 `provider` 对象。 下面的代码阐释如何使用表示 fr\-FR 区域性的 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29> 对象调用 <xref:System.Globalization.CultureInfo> 方法。  
  
         [!code-csharp[Formatting.Howto.WeekdayName#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/abbrname2.cs#2)]
         [!code-vb[Formatting.Howto.WeekdayName#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/abbrname2.vb#2)]  
  
### 从特定日期中提取完整的星期几名称  
  
1.  如果要使用日期的字符串表示形式，请使用静态 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 方法将其转换为 <xref:System.DateTime.Parse%2A?displayProperty=fullName> 或 <xref:System.DateTimeOffset.Parse%2A?displayProperty=fullName> 值。  
  
2.  你可以提取当前区域性或特定区域性的完整的星期几名称：  
  
    1.  若要提取当前区域性的缩写的星期几名称，请调用日期和时间值的 <xref:System.DateTime.ToString%28System.String%29?displayProperty=fullName> 或 <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=fullName> 实例方法，并以 `format` 参数的形式传递字符串“dddd”。 下面的示例演示 <xref:System.DateTime.ToString%28System.String%29> 方法的调用。  
  
         [!code-csharp[Formatting.Howto.WeekdayName#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/fullname4.cs#4)]
         [!code-vb[Formatting.Howto.WeekdayName#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/fullname4.vb#4)]  
  
    2.  若要提取特定区域性的星期几名称，请调用日期和时间值的 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName> 或 <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName> 实例方法。 同时以 `format` 参数形式传递字符串“dddd”。 以 <xref:System.Globalization.CultureInfo> 参数的形式传递表示要检索其星期几名称的区域性的 <xref:System.Globalization.DateTimeFormatInfo> 或 `provider` 对象。 下面的代码阐释如何使用表示 es\-ES 区域性的 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29> 对象调用 <xref:System.Globalization.CultureInfo> 方法。  
  
         [!code-csharp[Formatting.Howto.WeekdayName#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/fullname5.cs#5)]
         [!code-vb[Formatting.Howto.WeekdayName#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/fullname5.vb#5)]  
  
## 示例  
 该示例演示如何调用 <xref:System.DateTime.DayOfWeek%2A?displayProperty=fullName> 和 <xref:System.DateTimeOffset.DayOfWeek%2A?displayProperty=fullName> 属性以及 <xref:System.DateTime.ToString%2A?displayProperty=fullName> 和 <xref:System.DateTimeOffset.ToString%2A?displayProperty=fullName> 方法，以检索特定日期中表示星期几的数字、缩写的星期几名称和完整的星期几名称。  
  
 [!code-csharp[Formatting.Howto.WeekdayName#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/example6.cs#6)]
 [!code-vb[Formatting.Howto.WeekdayName#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/example6.vb#6)]  
  
 个别语言可能提供与 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 所提供的功能相同或互为补充的功能。 例如，Visual Basic 包括这样的两个函数：  
  
-   `Weekday`，它返回指示特定日期中表示星期几的数字。 此函数将一周中第一天的序数值视为一，而 <xref:System.DateTime.DayOfWeek%2A?displayProperty=fullName> 属性却将其视为零。  
  
-   `WeekdayName`，它返回当前区域性中与特定星期几相对应的周的名称。  
  
 下面的示例演示了 Visual Basic `Weekday` 和 `WeekdayName` 函数的用法。  
  
 [!code-vb[Formatting.HowTo.WeekdayName#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/example9.vb#9)]  
  
 也可以使用 <xref:System.DateTime.DayOfWeek%2A?displayProperty=fullName> 属性返回的值检索特定日期的星期几名称。 此过程只需对 <xref:System.Enum.ToString%2A> 属性返回的值调用 <xref:System.DayOfWeek> 方法。 但是，此技术并不生成当前区域性的本地化星期几名称，如下面的示例所示。  
  
 [!code-csharp[Formatting.HowTo.WeekdayName#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/Howto1.cs#8)]
 [!code-vb[Formatting.HowTo.WeekdayName#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/Howto1.vb#8)]  
  
## 请参阅  
 [执行格式设置操作](../../../docs/standard/base-types/performing-formatting-operations.md)   
 [标准日期和时间格式字符串](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)   
 [自定义日期和时间格式字符串](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)