---
title: "时区概述 | Microsoft Docs"
ms.custom: ""
ms.date: "04/10/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "调整规则 [.NET Framework]"
  - "不明确的时间 [.NET Framework]"
  - "夏时制 [.NET Framework]"
  - "固定规则 [.NET Framework]"
  - "浮动规则 [.NET Framework]"
  - "无效时间 [.NET Framework]"
  - "时区 [.NET Framework], 关于时区"
  - "时区 [.NET Framework], 创建"
  - "时区 [.NET Framework], 术语"
  - "TimeZoneInfo 类, 关于 TimeZoneInfo 类"
  - "转换时间 [.NET Framework]"
ms.assetid: c4b7ed01-5e38-4959-a3b6-ef9765d6ccf1
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# 时区概述
<xref:System.TimeZoneInfo> 类可简化时区识别应用程序的创建。  <xref:System.TimeZone> 类支持使用本地时区和协调世界时 \(UTC\)。  <xref:System.TimeZoneInfo> 类除了支持上述两种时区外，还支持注册表中已预定义其相关信息的任何时区。  使用 <xref:System.TimeZoneInfo> 还可以定义系统尚不具有其相关信息的自定义时区。  
  
## 时区要点  
 时区是使用同一时间的地理区域。  通常情况下，两个相邻时区之间相差一个小时，但情况并非总是如此。  世界上任何时区的时间都可以表示为协调世界时 \(UTC\) 的一个偏移量。  
  
 世界上的很多时区都支持夏时制。  夏时制会在春季或初夏将时间向前调一个小时，而在夏末或秋季将时间调回正常（或标准）时间，从而来尽量延长白昼时间。  这些在夏时制和标准时间之间的来回变更称为调整规则。  
  
 在特定的时区中，夏时制的来回转换既可以由固定调整规则定义，也可以由浮动调整规则定义。  固定调整规则会指定一个特定的日期，并在每年的这一天进行夏时制的来回转换。  例如，夏时制在每年的 10 月 25 日转换为标准时间，这遵循的便是固定调整规则。  更为常见的是浮动调整规则，这种规则会指定特定月份中特定星期的一个特定日期，并在这一天进行夏时制的来回转换。  例如，如果规定在 3 月的第三个星期日从标准时间转换为夏时制，这遵循的便是浮动调整规则。  
  
 在支持调整规则的时区中，夏时制的来回转换会产生两种反常时间：无效时间和不明确的时间。  无效时间是指因从标准时间转换为夏时制而产生的不存在的时间。  例如，如果这一转换发生在某一天凌晨 2:00 并导致时间改变为 3:00 AM，每次在凌晨 2:00到 2:59: 99 AM之间的间隔无效。  不明确的时间是指可在一个时区中映射为两个不同时间的时间。  这种情况是在从夏时制转换为标准时间时出现的。  例如，如果这一转换发生在某一天凌晨 2:00 并导致时间为 1:00 AM，每次在凌晨1:00到1:59: 99 AM之间的间隔可以解释为标准时间或夏时制。  
  
## 时区术语  
 下表定义了在使用时区和开发时区识别应用程序时常用的术语。  
  
|术语|定义|  
|--------|--------|  
|调整规则|一种规则，用于定义从标准时间转换为夏时制以及从夏时制转换回标准时间的时间。  每个调整规则都包含以下要素：一个定义规则有效期的开始日期和结束日期（例如，调整规则的有效期为 1986 年 1 月 1 日到 2006 年 12 月 31 日）、一个增量（因施行调整规则而使标准时间更改的时间量）以及有关调整期内发生转换的特定日期和时间的信息。  转换可遵循固定规则，也可以遵循浮动规则。|  
|不明确的时间|指可在一个时区中映射为两个不同时间的时间。  当向回调整时钟时间时（例如某时区在从夏时制转换为标准时间的过程中），就会出现此情况。  例如，如果这一转换发生在某一天凌晨 2:00 并导致时间为 1:00 AM，每次在凌晨1:00到1:59: 99 AM之间的间隔可以解释为标准时间或夏时制。|  
|固定规则|一种调整规则，它会指定一个特定的日期，并在这一天进行夏时制的来回转换。  例如，夏时制在每年的 10 月 25 日转换为标准时间，这遵循的便是固定调整规则。|  
|浮动规则|一种调整规则，它会指定特定月份中特定星期的一个特定日期，并在这一天进行夏时制的来回转换。  例如，如果规定在 3 月的第三个星期日从标准时间转换为夏时制，这遵循的便是浮动调整规则。|  
|无效时间|指因从标准时间转换为夏时制而产生的不存在的时间。  当向前调整时钟时间时（例如某时区在从标准时间转换为夏时制的过程中），就会出现此情况。  例如，如果这一转换发生在某一天凌晨 2:00 并导致时间改变为 3:00 AM，每次在凌晨 2:00到 2:59: 99 AM之间的间隔无效。|  
|转换时间|有关特定时区中的特定时间更改的信息，例如从夏时制更改为标准时间，或从标准时间更改为夏时制。|  
  
## 时区和 TimeZoneInfo 类  
 在 .NET Framework 中，<xref:System.TimeZoneInfo> 对象表示时区。  <xref:System.TimeZoneInfo> 类包含一个 <xref:System.TimeZoneInfo.GetAdjustmentRules%2A> 方法，该方法可返回 <xref:System.TimeZoneInfo.AdjustmentRule> 对象的数组。  此数组中的每个元素均提供有关在特定时间段内来回转换夏时制的信息。（对于不支持夏时制的时区，该方法会返回一个空数组。）每个 <xref:System.TimeZoneInfo.AdjustmentRule> 对象都有一个 <xref:System.TimeZoneInfo.AdjustmentRule.DaylightTransitionStart%2A> 和 <xref:System.TimeZoneInfo.AdjustmentRule.DaylightTransitionEnd%2A> 属性，用于定义来回转换夏时制的特定日期和时间。  <xref:System.TimeZoneInfo.TransitionTime.IsFixedDateRule%2A> 属性指示转换是属于固定转换，还是浮动转换。  
  
 .NET Framework 依赖 Windows 操作系统所提供的以及注册表中所存储的时区信息进行工作。  由于世界上有很多时区，并非所有现有时区在注册表中都有相应的表示形式。  此外，由于注册表是一个动态结构，用户可以在注册表中添加或移除预定义时区。  因此，注册表并不一定包含历史时区数据。  例如，在 Windows XP 中，注册表只包含一组时区调整数据。  Windows Vista 支持动态时区数据，这意味着一个时区可以有多个适用于特定年份间隔的调整规则。  但是，Windows Vista 注册表中定义的支持夏时制的大多数时区都只具有一两个预定义调整规则。  
  
 <xref:System.TimeZoneInfo> 类对注册表的依赖关系表明，时区识别应用程序不能确定注册表中是否定义了某个特定的时区。  因此，在尝试实例化特定时区（本地时区或表示 UTC 的时区除外）时应使用异常处理。  此外，还应该提供某种方法，以便让应用程序在无法从注册表中实例化所需的 <xref:System.TimeZoneInfo> 对象时仍可以继续运行。  
  
 为了应对所需时区不存在的情况，<xref:System.TimeZoneInfo> 类包含了一个 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 方法，使用此方法可以创建未在注册表中找到的自定义时区。  有关创建自定义时区的详细信息，请参见[如何：创建不带调整规则的时区](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md)和[如何：创建带有调整规则的时区](../../../docs/standard/datetime/create-time-zones-with-adjustment-rules.md)。  此外，还可以使用 <xref:System.TimeZoneInfo.ToSerializedString%2A> 方法将新创建的时区转换为字符串并将它保存在数据存储区（例如数据库、文本文件、注册表或应用程序资源）中。  以后您就可以使用 <xref:System.TimeZoneInfo.FromSerializedString%2A> 方法将此字符串转换回 <xref:System.TimeZoneInfo> 对象。  有关详细信息，请参见[如何：将时区保存到嵌入的资源中](../../../docs/standard/datetime/save-time-zones-to-an-embedded-resource.md)和[如何：从嵌入的资源还原时区](../../../docs/standard/datetime/restore-time-zones-from-an-embedded-resource.md)。  
  
 由于每个时区都可以用一个基本 UTC 偏移量加上一个反映任何现有调整规则的 UTC 偏移量来表示，因此可以轻松地将一个时区中的时间转换为另一个时区中的时间。  为实现此目的，<xref:System.TimeZoneInfo> 对象包含了几种转换方法，其中包括：  
  
-   <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A>，用于将 UTC 转换为指定时区中的时间。  
  
-   <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A>，用于将指定时区中的时间转换为 UTC。  
  
-   <xref:System.TimeZoneInfo.ConvertTime%2A>，用于将一个指定时区中的时间转换为另一个指定时区中的时间。  
  
-   <xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A>，此方法使用时区标识符（而不是 <xref:System.TimeZoneInfo> 对象）作为参数，可将一个指定时区中的时间转换为另一个指定时区中的时间。  
  
 有关在不同时区之间转换时间的详细信息，请参见[在不同时区之间转换时间](../../../docs/standard/datetime/converting-between-time-zones.md)。  
  
## 请参阅  
 [日期、时间和时区](../../../docs/standard/datetime/index.md)