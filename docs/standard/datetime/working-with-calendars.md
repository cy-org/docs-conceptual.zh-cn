---
title: "使用日历 | Microsoft Docs"
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
  - "日历, 全局应用程序"
  - "区域性, 日历"
  - "全局应用程序, 日历"
  - "全球化 [.NET Framework], 日历"
  - "国际应用程序 [.NET Framework], 日历"
  - "世界通用的应用程序, 日历"
ms.assetid: 0c1534e5-979b-4c8a-a588-1c24301aefb3
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# 使用日历
尽管日期和时间值表示时间中的某一刻，但其字符串表示形式区分区域性，并取决于特定区域性显示日期和时间值所用的约定以及该区域性使用的日历。  本主题研究 .NET Framework 中对日历的支持，并探讨在使用日期值时如何使用日历类。  
  
## .NET Framework 中的日历  
 .NET Framework 中的所有日历均派生自 <xref:System.Globalization.Calendar?displayProperty=fullName> 类，该类提供了基本日历实现。  从 <xref:System.Globalization.Calendar> 类继承的类之一是 <xref:System.Globalization.EastAsianLunisolarCalendar> 类，该类是所有阴阳历的基类。  .NET Framework 包括以下日历实现：  
  
-   <xref:System.Globalization.ChineseLunisolarCalendar>，表示中国阴阳历。  
  
-   <xref:System.Globalization.GregorianCalendar>，表示公历。  此日历进一步细分为 <xref:System.Globalization.GregorianCalendarTypes?displayProperty=fullName> 枚举定义的子类型（如阿拉伯和中东法国）。  <xref:System.Globalization.GregorianCalendar.CalendarType%2A?displayProperty=fullName> 属性指定公历的子类型。  
  
-   <xref:System.Globalization.HebrewCalendar>，表示希伯来历。  
  
-   <xref:System.Globalization.HijriCalendar>，表示回历。  
  
-   <xref:System.Globalization.JapaneseCalendar>，表示日本历。  
  
-   <xref:System.Globalization.JapaneseLunisolarCalendar>，表示日本阴阳历。  
  
-   <xref:System.Globalization.JulianCalendar>，表示罗马儒略历。  
  
-   <xref:System.Globalization.KoreanCalendar>，表示朝鲜历。  
  
-   <xref:System.Globalization.KoreanLunisolarCalendar>，表示朝鲜阴阳历。  
  
-   <xref:System.Globalization.PersianCalendar>，表示波斯历。  
  
-   <xref:System.Globalization.TaiwanCalendar>，表示台湾历。  
  
-   <xref:System.Globalization.TaiwanLunisolarCalendar>，表示台湾阴阳历。  
  
-   <xref:System.Globalization.ThaiBuddhistCalendar>，表示泰国佛历。  
  
-   <xref:System.Globalization.UmAlQuraCalendar>，表示古兰经历。  
  
 可通过以下两种方法之一来使用日历：  
  
-   作为特定区域性使用的日历。  每个 <xref:System.Globalization.CultureInfo> 对象都有当前日历，这是该对象当前使用的日历。  所有日期和时间值的字符串表示形式会自动反映当前的区域性及其当前日历。  通常，当前的日历是该区域性的默认日历。  <xref:System.Globalization.CultureInfo> 对象还具有可选日历，其中包括该区域性可以使用的其他日历。  
  
-   作为与特定区域性无关的独立日历。  在这种情况下，<xref:System.Globalization.Calendar> 方法用于将日期表示为反映日历的值。  
  
 请注意，以下六个日历类只能用作独立日历：<xref:System.Globalization.ChineseLunisolarCalendar>、<xref:System.Globalization.JapaneseLunisolarCalendar>、<xref:System.Globalization.JulianCalendar>、<xref:System.Globalization.KoreanLunisolarCalendar>、<xref:System.Globalization.PersianCalendar> 和 <xref:System.Globalization.TaiwanLunisolarCalendar>。  任何区域性都不将这些日历用作默认日历或可选日历。  
  
## 日历和区域性  
 每个区域性都有默认日历，由 <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=fullName> 属性定义。  <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=fullName> 属性可返回 <xref:System.Globalization.Calendar> 对象的数组，该数组指定特定区域性支持的所有日历，包括该区域性的默认日历。  
  
 下面的示例演示 <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=fullName> 和 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=fullName> 属性。  该示例为泰语（泰国）和日语（日本）区域性创建 `CultureInfo` 对象，并显示它们的默认和可选日历。  请注意，在这两种情况下，区域性的默认日历也包括在 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=fullName> 集合中。  
  
 [!code-csharp[Conceptual.Calendars#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/calendarinfo1.cs#1)]
 [!code-vb[Conceptual.Calendars#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/calendarinfo1.vb#1)]  
  
 特定 <xref:System.Globalization.CultureInfo> 对象当前正在使用的日历由区域性的 <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A?displayProperty=fullName> 属性定义。  区域性的 <xref:System.Globalization.DateTimeFormatInfo> 对象由 <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=fullName> 属性返回。  创建区域性时，其默认值与 <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=fullName> 属性的值相同。  但是，可将区域性的当前日历更改为 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=fullName> 属性返回的数组中包含的任何日历。  如果尝试将当前日历设置为 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=fullName> 属性值中不包括的日历，则会引发 <xref:System.ArgumentException>。  
  
 以下示例将更改阿拉伯（沙特阿拉伯）区域性使用的日历。  它首先实例化一个 <xref:System.DateTime> 值并使用当前区域性（在此示例中，为英语（美国））和当前区域性的日历（在此示例中，为公历）显示该值。  接下来，该示例将当前区域性更改为阿拉伯语（沙特阿拉伯），并使用其默认的古兰经历显示该日期。  然后，该示例调用 `CalendarExists` 方法来确定阿拉伯语（沙特阿拉伯）区域性是否支持该回历。  因为该日历受支持，所以该示例将当前日历更改为回历并再次显示日期。  请注意，在每种情况下，均使用当前区域性的当前日历来显示日期。  
  
 [!code-csharp[Conceptual.Calendars#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/changecalendar2.cs#2)]
 [!code-vb[Conceptual.Calendars#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/changecalendar2.vb#2)]  
  
## 日期和日历  
 除包括 <xref:System.Globalization.Calendar> 类型参数并允许日期的元素（即月、日和年）以指定日历反映值的构造函数外，<xref:System.DateTime> 和 <xref:System.DateTimeOffset> 值始终基于公历。  例如，这意味着 <xref:System.DateTime.Year%2A?displayProperty=fullName> 属性返回公历的年，<xref:System.DateTime.Day%2A?displayProperty=fullName> 属性返回公历的当月日期。  
  
> [!IMPORTANT]
>  请记住，日期值与其字符串表示形式之间是有差异的，这一点很重要。  前者基于公历，后者基于特定区域性的当前日历。  
  
 下面的示例演示了 <xref:System.DateTime> 属性与其对应的 <xref:System.Globalization.Calendar> 方法之间的这一差异。  在此示例中，当前区域性为阿拉伯语（埃及），当前日历为古兰经历。  <xref:System.DateTime> 值设置为 2011 年 7 月 15 日。  很显然，该值被解释为公历日期，因为这些相同的值是由 <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=fullName> 方法在使用不变区域性的约定时返回的。  使用当前区域性的约定设置格式后，该日期的字符串表示形式为 14\/08\/32，与古兰经历中的日期等效。  接下来，使用 `DateTime` 和 `Calendar` 的成员返回 <xref:System.DateTime> 值的日、月和年。  在每种情况下，<xref:System.DateTime> 成员返回的值反映公历中的值，而 <xref:System.Globalization.UmAlQuraCalendar> 成员返回的值反映古兰经历中的值。  
  
 [!code-csharp[Conceptual.Calendars#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/datesandcalendars2.cs#3)]
 [!code-vb[Conceptual.Calendars#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/datesandcalendars2.vb#3)]  
  
### 根据日历实例化日期  
 由于 <xref:System.DateTime> 和 <xref:System.DateTimeOffset> 值基于公历，因此如果要使用不同日历中的日、月或年的值，必须调用包括 <xref:System.Globalization.Calendar> 类型参数的重载构造函数来实例化日期值。  还可以调用特定日历的 <xref:System.Globalization.Calendar.ToDateTime%2A?displayProperty=fullName> 方法的重载之一，以基于特定日历的值来实例化 <xref:System.DateTime> 对象。  
  
 下面的示例通过向 <xref:System.DateTime> 构造函数传递一个 <xref:System.Globalization.HebrewCalendar> 对象来实例化一个 <xref:System.DateTime> 值，通过调用 <xref:System.Globalization.HebrewCalendar.ToDateTime%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%29?displayProperty=fullName> 方法来实例化另一个 <xref:System.DateTime> 值。  由于这两个值是使用希伯来历中的相同值创建的，因此对 <xref:System.DateTime.Equals%2A?displayProperty=fullName> 方法的调用显示这两个 <xref:System.DateTime> 值相等。  
  
 [!code-csharp[Conceptual.Calendars#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/instantiatehcdate1.cs#4)]
 [!code-vb[Conceptual.Calendars#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/instantiatehcdate1.vb#4)]  
  
### 使用当前日历表示日期  
 在将日期转换为字符串时，日期和时间格式设置方法始终使用当前日历。  这意味着，年、月和当月日期的字符串表示形式反映当前日历，不一定反映公历。  
  
 下面的示例演示当前日历如何影响日期的字符串表示形式。  该示例将当前区域性更改为中文（繁体，台湾），并实例化日期值。  然后，该示例显示当前日历和日期，将当前日历更改为 <xref:System.Globalization.TaiwanCalendar>，并再次显示当前日历和日期。  初次显示日期时，它表示为公历日期。  第二次显示日期时，它表示为台湾日历中的日期。  
  
 [!code-csharp[Conceptual.Calendars#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/currentcalendar1.cs#5)]
 [!code-vb[Conceptual.Calendars#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/currentcalendar1.vb#5)]  
  
### 使用非当前日历表示日期  
 若要使用特定区域性的当前日历之外的日历表示日期，必须调用该 <xref:System.Globalization.Calendar> 对象的方法。  例如，<xref:System.Globalization.Calendar.GetYear%2A?displayProperty=fullName>、<xref:System.Globalization.Calendar.GetMonth%2A?displayProperty=fullName> 和 <xref:System.Globalization.Calendar.GetDayOfMonth%2A?displayProperty=fullName> 方法可将年、月和日转换为反映特定日历的值。  
  
> [!WARNING]
>  由于某些日历不是任何区域性的可选日历，因此用这些日历表示日期始终需要调用日历方法。  对于派生自 <xref:System.Globalization.EastAsianLunisolarCalendar>、<xref:System.Globalization.JulianCalendar> 和 <xref:System.Globalization.PersianCalendar> 类的所有日历而言，均为这种情况。  
  
 下面的示例使用 <xref:System.Globalization.JulianCalendar> 对象实例化罗马儒略历的日期 1905 年 1 月 9 日。  使用默认（公历）日历显示此日期时，该日期表示为 1905 年 1 月 22 日。  通过调用各种 <xref:System.Globalization.JulianCalendar> 方法，可用罗马儒略历表示日期。  
  
 [!code-csharp[Conceptual.Calendars#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/noncurrentcalendar1.cs#6)]
 [!code-vb[Conceptual.Calendars#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/noncurrentcalendar1.vb#6)]  
  
### 日历和日期范围  
 日历支持的最早日期由其 <xref:System.Globalization.Calendar.MinSupportedDateTime%2A?displayProperty=fullName> 属性指示。  对于 <xref:System.Globalization.GregorianCalendar> 类，该日期为公历公元 0001 年 1 月 1 日。.NET Framework 中的其他大多数日历支持更晚的日期。  尝试使用日历支持的最早日期前面的日期和时间值将引发 <xref:System.ArgumentOutOfRangeException> 异常。  
  
 但是，有一个很重要的异常。  <xref:System.DateTime> 对象和 <xref:System.DateTimeOffset> 对象的默认（未初始化的）值等于 <xref:System.Globalization.GregorianCalendar.MinSupportedDateTime%2A?displayProperty=fullName> 值。  如果尝试在不支持公历公元 0001 年 1 月 1 日的日历中设置此日期的格式，且不提供格式说明符，则格式设置方法将使用“s”（可排序的日期\/时间模式）格式说明符，而不使用“G”（常规日期\/时间模式）格式说明符。  因此，格式设置操作将不会引发 <xref:System.ArgumentOutOfRangeException> 异常。  相反，它会返回不受支持的日期。  下面的示例阐释了这一点，在使用日语日历将当前区域性设置为日语（日本）以及使用古兰经历将当前区域性设置为阿拉伯语（埃及）时，它将显示 <xref:System.DateTime.MinValue?displayProperty=fullName> 的值。  它还会将当前区域性设置为英语（美国），并调用 <xref:System.DateTime.ToString%28System.IFormatProvider%29?displayProperty=fullName> 方法以及所有这些 <xref:System.Globalization.CultureInfo> 对象。  在每种情况下，均使用可排序的日期\/时间模式来显示日期。  
  
 [!code-csharp[Conceptual.Calendars#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/minsupporteddatetime1.cs#11)]
 [!code-vb[Conceptual.Calendars#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/minsupporteddatetime1.vb#11)]  
  
## 使用纪元  
 日历通常将日期划分为纪元。  但是，.NET Framework 中的 <xref:System.Globalization.Calendar> 类不支持日历定义的每个纪元，而且大多数 <xref:System.Globalization.Calendar> 类只支持单个纪元。  只有 <xref:System.Globalization.JapaneseCalendar> 和 <xref:System.Globalization.JapaneseLunisolarCalendar> 类支持多个纪元。  
  
### 纪元和纪元名称  
 在 .NET Framework 中，表示特定日历实现支持的纪元的整数以反向顺序存储在 <xref:System.Globalization.Calendar.Eras%2A?displayProperty=fullName> 数组中。  当前纪元的索引为零，对于支持多个纪元的 <xref:System.Globalization.Calendar> 类，每个后续索引反映前一个纪元。  静态的 <xref:System.Globalization.Calendar.CurrentEra?displayProperty=fullName> 属性定义当前纪元在 <xref:System.Globalization.Calendar.Eras%2A?displayProperty=fullName> 数组中的索引；它是一个值始终为零的常数。  各个 <xref:System.Globalization.Calendar> 类还包括可返回当前纪元值的静态字段。  下表中列出了这些字段。  
  
|日历类|当前纪元字段|  
|---------|------------|  
|<xref:System.Globalization.ChineseLunisolarCalendar>|<xref:System.Globalization.ChineseLunisolarCalendar.ChineseEra>|  
|<xref:System.Globalization.GregorianCalendar>|<xref:System.Globalization.GregorianCalendar.ADEra>|  
|<xref:System.Globalization.HebrewCalendar>|<xref:System.Globalization.HebrewCalendar.HebrewEra>|  
|<xref:System.Globalization.HijriCalendar>|<xref:System.Globalization.HijriCalendar.HijriEra>|  
|<xref:System.Globalization.JapaneseLunisolarCalendar>|<xref:System.Globalization.JapaneseLunisolarCalendar.JapaneseEra>|  
|<xref:System.Globalization.JulianCalendar>|<xref:System.Globalization.JulianCalendar.JulianEra>|  
|<xref:System.Globalization.KoreanCalendar>|<xref:System.Globalization.KoreanCalendar.KoreanEra>|  
|<xref:System.Globalization.KoreanLunisolarCalendar>|<xref:System.Globalization.KoreanLunisolarCalendar.GregorianEra>|  
|<xref:System.Globalization.PersianCalendar>|<xref:System.Globalization.PersianCalendar.PersianEra>|  
|<xref:System.Globalization.ThaiBuddhistCalendar>|<xref:System.Globalization.ThaiBuddhistCalendar.ThaiBuddhistEra>|  
|<xref:System.Globalization.UmAlQuraCalendar>|<xref:System.Globalization.UmAlQuraCalendar.UmAlQuraEra>|  
  
 通过将特定纪元编号传递给 <xref:System.Globalization.DateTimeFormatInfo.GetEraName%2A?displayProperty=fullName> 或 <xref:System.Globalization.DateTimeFormatInfo.GetAbbreviatedEraName%2A?displayProperty=fullName> 方法，可检索与该纪元编号对应的名称。  下面的示例调用这些方法来检索有关 <xref:System.Globalization.GregorianCalendar> 类中的纪元支持信息。  
  
 [!code-csharp[Conceptual.Calendars#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/instantiatewithera1.cs#7)]
 [!code-vb[Conceptual.Calendars#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/instantiatewithera1.vb#7)]  
  
 此外，“g”自定义日期和时间格式字符串还包括一个日期和时间的字符串表示形式的日期纪元名称。  有关更多信息，请参见[自定义日期和时间格式字符串](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)。  
  
### 用纪元实例化日期  
 对于支持多个纪元的两个 <xref:System.Globalization.Calendar> 类，由特定年、月和当月日期值构成的日期可能不明确。例如，<xref:System.Globalization.JapaneseCalendar> 的所有四个纪元的年份编号均为 1 至 15。  通常，如果未指定纪元，则日期和时间以及日历方法都假定该值属于当前纪元。  若要在为支持多个纪元的 <xref:System.Globalization.Calendar> 类实例化日期时显式指定纪元，可调用 <xref:System.Globalization.Calendar.ToDateTime%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%29?displayProperty=fullName> 方法。  通过此方法可以显式指定纪元以及日期的年、月、日、小时、分钟、秒和毫秒。  
  
 下面的示例使用 <xref:System.Globalization.Calendar.ToDateTime%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%29?displayProperty=fullName> 方法在 <xref:System.Globalization.JapaneseCalendar> 类支持的每个纪元中实例化相同的日期：第二年的第一个月的第一天。  然后，该示例使用日本日历和公历显示该日期。  它还调用 <xref:System.DateTime> 构造函数，以演示在不指定纪元时，创建日期的方法会以当前纪元创建日期。  
  
 [!code-csharp[Conceptual.Calendars#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/instantiatewithera1.cs#7)]
 [!code-vb[Conceptual.Calendars#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/instantiatewithera1.vb#7)]  
  
### 使用带纪元的日历表示日期  
 如果 <xref:System.Globalization.Calendar> 对象支持纪元并且是 <xref:System.Globalization.CultureInfo> 对象的当前日历，则纪元将包括在完整日期和时间、长日期和短日期模式的日期和时间值的字符串表示形式中。  下面的示例显示当前区域性为日语（日本）并且当前日历为日本日历时的这些日期模式。  
  
 [!code-csharp[Conceptual.Calendars#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings1.cs#8)]
 [!code-vb[Conceptual.Calendars#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings1.vb#8)]  
  
> [!WARNING]
>  <xref:System.Globalization.JapaneseCalendar> 类是 .NET Framework 中既支持多个纪元中的日期又可为 <xref:System.Globalization.CultureInfo> 对象（具体而言，是表示日语（日本）区域性的 <xref:System.Globalization.CultureInfo> 对象）的当前日历的唯一日历类。  
  
 对于所有日历，“g”自定义格式说明符会在结果字符串中包括纪元。  下面的示例使用“MM\-dd\-yyyy g”自定义格式字符串，在当前日历为公历时在结果字符串中包括纪元。  
  
 [!code-csharp[Conceptual.Calendars#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings2.cs#9)]
 [!code-vb[Conceptual.Calendars#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings2.vb#9)]  
  
 当日期的字符串表示形式用非当前日历来表示时，<xref:System.Globalization.Calendar> 类包括一个可与 <xref:System.Globalization.Calendar.GetYear%2A?displayProperty=fullName>、<xref:System.Globalization.Calendar.GetMonth%2A?displayProperty=fullName> 和 <xref:System.Globalization.Calendar.GetDayOfMonth%2A?displayProperty=fullName> 方法一起使用的 <xref:System.Globalization.Calendar.GetEra%2A?displayProperty=fullName> 方法，以明确指示日期及其所属纪元。  下面的示例使用 <xref:System.Globalization.JapaneseLunisolarCalendar> 类来提供演示。  但请注意，在结果字符串中包括有意义的名称或缩写（而不是表示纪元的整数）需要您实例化 <xref:System.Globalization.DateTimeFormatInfo> 对象并使 <xref:System.Globalization.JapaneseCalendar> 成为其当前日历。（<xref:System.Globalization.JapaneseLunisolarCalendar> 日历不能为任何区域性的当前日历，但在此示例中，两个日历共享相同的纪元。）  
  
 [!code-csharp[Conceptual.Calendars#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings3.cs#10)]
 [!code-vb[Conceptual.Calendars#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings3.vb#10)]  
  
## 请参阅  
 [如何：用非公历日历显示日期](../../../docs/standard/base-types/how-to-display-dates-in-non-gregorian-calendars.md)   
 [示例：日历周范围实用工具](http://code.msdn.microsoft.com/NET-Framework-4-Calendar-3360a84a)