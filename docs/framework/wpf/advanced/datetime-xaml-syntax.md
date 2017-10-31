---
title: "DateTime XAML 语法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "DateTime XAML 语法 [WPF]"
  - "DateTime XAML 语法 [WPF], 格式字符串"
  - "DateTime XAML 语法 [WPF], 字符串"
  - "DateTime XAML 语法 [WPF], 使用场合"
  - "DateTime XAML 文本 [WPF]"
  - "短日期格式 [WPF], DateTime"
ms.assetid: 5901710a-609b-40c8-9d65-f0016cd9090b
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# DateTime XAML 语法
一些控件，如 <xref:System.Windows.Controls.Calendar> 和 <xref:System.Windows.Controls.DatePicker>，具有使用 <xref:System.DateTime> 类型的属性。  虽然通常会在运行时在代码隐藏文件中指定这些控件的初始日期或时间，但您可以在 XAML 中指定初始日期或时间。  WPF XAML 分析器使用内置的 XAML 文本语法对 <xref:System.DateTime> 的值进行分析。  本主题介绍 <xref:System.DateTime> XAML 文本语法的具体内容。  
  
   
  
<a name="where_datetime_xaml_syntax_is_used"></a>   
## 使用 DateTime XAML 语法的时间  
 无需经常对 XAML 中的日期进行设置，而且设置也可能并不合适。  例如，可以使用 <xref:System.DateTime.Now%2A?displayProperty=fullName> 属性在运行时初始化一个日期，或者可以基于用户输入的代码隐藏为日历的所有日期进行调整。  但是，有些情况下，您可能要硬编码日期到控件模板的 <xref:System.Windows.Controls.Calendar> 和 <xref:System.Windows.Controls.DatePicker> 中。  这些场合必须使用 <xref:System.DateTime> XAML 语法。  
  
### Datetime XAML 语法是本机行为  
 <xref:System.DateTime> 是在 CLR 基类库中定义的类。  出于基类库与 CLR 的其余部分相关的方法的原因，所以不可能将 <xref:System.ComponentModel.TypeConverterAttribute> 应用于类，也不可能在运行时对象模式下使用类型转换器处理 XAML 中的字符串并将它们转换为 <xref:System.DateTime>。  没有提供转换类型的 `DateTimeConverter` 类；本主题中描述的转换类型派生至 WPF XAML 分析器。  
  
<a name="format_strings_for_datetime_xaml_syntax"></a>   
## DateTime XAML 语法的格式字符串  
 可通过格式字符串指定 <xref:System.DateTime> 的格式。  格式字符串会规范可用于创建值的文本语法。  现有 WPF 的 <xref:System.DateTime> 值通常只使用 <xref:System.DateTime> 的日期组件而不是时间组件。  
  
 当指定 XAML 中的 <xref:System.DateTime> 时，可以交替使用任何格式字符串。  
  
 您还可以使用格式和未在本主题中专门显示的格式字符串。  从技术上讲，指定的并之后由 WPF XAML 解析的 <xref:System.DateTime> 值使用内部 <xref:System.DateTime.Parse%2A?displayProperty=fullName> 调用，因此可使用 <xref:System.DateTime.Parse%2A?displayProperty=fullName> 接受的任何字符串用于 XAML 输入。  有关更多信息，请参见 <xref:System.DateTime.Parse%2A?displayProperty=fullName>。  
  
> [!IMPORTANT]
>  DateTime XAML 语法中始终将 `en-us` 用作 <xref:System.Globalization.CultureInfo>，用于其固有转换。  这不会受 <xref:System.Windows.FrameworkElement.Language%2A> 值或在 XAML 中的 `xml:lang` 值影响，这是由于 XAML 特性级别类型转换可在没上下文情况下作用。  出于区域性差异的原因，请不要尝试插入此处显示的格式字符串，如显示日和月的顺序。  如下所示的格式字符串是准确的格式字符串，其在解析 XAML 时使用，而不考虑其他区域性设置。  
  
 以下各节描述一些 <xref:System.DateTime> 格式字符串。  
  
### 短日期模式（“d”）  
 如下显示了 XAML 中 <xref:System.DateTime> 的短日期格式：  
  
 `M/d/YYYY`  
  
 这是最简单的形式，指定 WPF 控件一般使用的必需信息，并且不受偶然时区偏移和时间组件影响，因此比其他格式更适用。  
  
 例如，要指定日期 2010 年 6 月 1 日，则使用下列字符串：  
  
 `3/1/2010`  
  
 有关更多信息，请参见 <xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A?displayProperty=fullName>。  
  
### 可排序 DateTime 模式（“s”）  
 以下显示 XAML中可排序的 <xref:System.DateTime> 模式。  
  
 `yyyy'-'MM'-'dd'T'HH':'mm':'ss`  
  
 例如，要指定日期 2010 年 6 月 1 日，则使用下列字符串（时间组件全部输入为 0）：  
  
 `2010-06-01T000:00:00`  
  
### RFC1123 模式 \("r"\)  
 RFC1123 模式很有用，因为它可以是来自其他字符生成器的字符串输入，这个字符生成器出于区域性固定原因同样使用 RFC1123。  以下显示 XAML中的 RFC1123 <xref:System.DateTime> 模式。  
  
 `ddd, dd MMM yyyy HH':'mm':'ss 'UTC'`  
  
 例如，要指定日期 2010 年 6 月 1 日，则使用下列字符串（时间组件全部输入为 0）：  
  
 `Mon, 01 Jun 2010 00:00:00 UTC`  
  
### 其他格式和模式  
 如上所述，XAML 中的 <xref:System.DateTime> 可以指定为任何可接受的，作为 <xref:System.DateTime.Parse%2A?displayProperty=fullName> 输入的字符串。  这包括其他正式的格式（例如 <xref:System.Globalization.DateTimeFormatInfo.UniversalSortableDateTimePattern%2A>\) 和不规范化为特定的 <xref:System.Globalization.DateTimeFormatInfo> 窗体的格式。  例如，作为 <xref:System.DateTime.Parse%2A?displayProperty=fullName>输入的窗体 `YYYY/mm/dd` 可被接受。  本主题不会尝试描述所有可能的格式的工作，并转而推荐作为标准做法的短日期模式。  
  
## 请参阅  
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)