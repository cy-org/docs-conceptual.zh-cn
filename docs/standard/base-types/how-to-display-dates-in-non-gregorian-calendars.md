---
title: "如何：用非公历日历显示日期 | Microsoft Docs"
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
  - "日期 [.NET Framework]，格式设置"
  - "日历 [.NET Framework]，显示日期"
  - "显示日期和时间数据"
ms.assetid: ed324eff-4aff-4a76-b6c0-04e6c0d8f5a9
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：用非公历日历显示日期
<xref:System.DateTime> 和 <xref:System.DateTimeOffset> 类型将公历作为它们的默认日历。  这意味着，调用日期和时间值的 `ToString` 方法将以公历显示该日期和时间的字符串表示形式，即使该日期和时间是使用其他日历创建的也是如此。  下面的示例对此进行了阐释。此示例采用两种不同的方式来创建以波斯历表示的日期和时间值，但在调用 <xref:System.DateTime.ToString%2A> 方法时，仍然会以公历来显示这些日期和时间值。  此示例反映了两种常用但不正确的以特定日历显示日期的方法。  
  
 [!code-csharp[Formatting.HowTo.Calendar#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Calendar/cs/Calendar1.cs#1)]
 [!code-vb[Formatting.HowTo.Calendar#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Calendar/vb/Calendar1.vb#1)]  
  
 若要以特定日历显示日期，可以使用两种不同的方法。  第一种方法要求该日历为特定区域性的默认日历。  第二种方法可用于任何日历。  
  
### 显示区域性默认日历的日期  
  
1.  实例化一个从表示要使用的日历的 <xref:System.Globalization.Calendar> 类派生的日历对象。  
  
2.  实例化一个 <xref:System.Globalization.CultureInfo> 对象，该对象表示将用于显示日期的格式的区域性。  
  
3.  调用 <xref:System.Array.Exists%2A?displayProperty=fullName> 方法，确定该日历对象是否是 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=fullName> 属性返回的数组的成员。  如果是，则指示该日历可用作 <xref:System.Globalization.CultureInfo> 对象的默认日历。  如果不是该数组的成员，请按照“以任意日历显示日期”一节中的说明进行操作。  
  
4.  将该日历对象分配给由 <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=fullName> 属性返回的 <xref:System.Globalization.DateTimeFormatInfo> 对象的 <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A> 属性。  
  
    > [!NOTE]
    >  <xref:System.Globalization.CultureInfo> 类还具有 <xref:System.Globalization.CultureInfo.Calendar%2A> 属性。  但是，它是一个只读常量；它不会更改来反映分配给 <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A?displayProperty=fullName> 属性的新默认日历。  
  
5.  调用 <xref:System.DateTime.ToString%2A> 或 <xref:System.DateTime.ToString%2A> 方法，并向其传递默认日历已在上一步中修改的 <xref:System.Globalization.CultureInfo> 对象。  
  
### 以任意日历显示日期  
  
1.  实例化一个从表示要使用的日历的 <xref:System.Globalization.Calendar> 类派生的日历对象。  
  
2.  确定哪些日期和时间元素应出现在日期和时间值的字符串表示形式中。  
  
3.  对于每个要显示的日期和时间元素，请调用日历对象的 `Get`… 方法。  有下列方法可供使用：  
  
    -   <xref:System.Globalization.Calendar.GetYear%2A>，用于以适当的日历显示年份。  
  
    -   <xref:System.Globalization.Calendar.GetMonth%2A>，用于以适当的日历显示月份。  
  
    -   <xref:System.Globalization.Calendar.GetDayOfMonth%2A>，用于以适当的日历显示月份中的日期。  
  
    -   <xref:System.Globalization.Calendar.GetHour%2A>，用于以适当的日历显示天中的小时。  
  
    -   <xref:System.Globalization.Calendar.GetMinute%2A>，用于以适当的日历显示小时中的分钟数。  
  
    -   <xref:System.Globalization.Calendar.GetSecond%2A>，用于以适当的日历显示分钟中的秒数。  
  
    -   <xref:System.Globalization.Calendar.GetMilliseconds%2A>，用于以适当的日历显示秒钟中的毫秒数。  
  
## 示例  
 该示例使用两种不同的日历显示日期。  它在将回历定义为 ar\-JO 区域性的默认日历后显示日期，并使用波斯历（fa\-IR 区域性并不将其视为受支持的可选日历）显示该日期。  
  
 [!code-csharp[Formatting.HowTo.Calendar#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.Calendar/cs/Calendar1.cs#2)]
 [!code-vb[Formatting.HowTo.Calendar#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.Calendar/vb/Calendar1.vb#2)]  
  
 每个 <xref:System.Globalization.CultureInfo> 对象都可以支持一个或多个日历，这些日历由 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A> 属性指示。  其中一个日历将被指定为区域性的默认日历，并由只读的 <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=fullName> 属性返回。  您也可以将另一个可选日历指定为默认日历，方法是将表示该日历的 <xref:System.Globalization.Calendar> 对象分配给 <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=fullName> 属性返回的 <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A?displayProperty=fullName> 属性。  但是，某些日历（例如由 <xref:System.Globalization.PersianCalendar> 类表示的波斯历）不能作为任何区域性的可选日历。  
  
 该示例定义了一个可重用的日历实用工具类 `CalendarUtility`，目的是处理用特定日历生成日期的字符串表示形式时的很多细节。  `CalendarUtility` 类具有下列成员：  
  
-   一个参数化构造函数，它唯一的参数是要用于表示日期的 <xref:System.Globalization.Calendar> 对象。  它将被分配给该类的私有字段。  
  
-   `CalendarExists`，此私有方法将返回一个布尔值，用于指示由 `CalendarUtility` 对象表示的日历是否受以参数形式传递给该方法的 <xref:System.Globalization.CultureInfo> 对象支持。  该方法包装对 <xref:System.Array.Exists%2A?displayProperty=fullName> 方法的调用，并向其传递 <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=fullName> 数组。  
  
-   `HasSameName`，此私有方法被分配给以参数形式传递给 <xref:System.Array.Exists%2A?displayProperty=fullName> 方法的 <xref:System.Predicate%601> 委托。  将向该方法传递数组的每个成员，直至该方法返回 `true`。  该方法确定可选日历是否与 `CalendarUtility` 对象表示的日历同名。  
  
-   `DisplayDate`，此重载的公共方法将获得两个参数：一个是 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 值（以便用 `CalendarUtility` 对象表示的日历表示），另一个是要使用其格式化规则的区域性。  其返回日期字符串表示形式的行为取决于目标日历是否受要使用其格式化规则的区域性支持。  
  
 在此示例中，无论使用何种日历创建 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 值，该值通常都将表示为公历日期。  这是因为，<xref:System.DateTime> 和 <xref:System.DateTimeOffset> 类型并不保留任何日历信息。  在内部，它们表示为从 0001 年 1 月 1 日午夜算起已过去的时间。  该数字的具体解释取决于所使用的日历。  大多数区域性的默认日历都是公历。  
  
## 编译代码  
 此示例需要引用 System.Core.dll。  
  
 在命令行处使用 csc.exe 或 vb.exe 编译代码。  若要在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中编译代码，请将代码置于控制台应用程序项目模板中。  
  
## 请参阅  
 [执行格式设置操作](../../../docs/standard/base-types/performing-formatting-operations.md)