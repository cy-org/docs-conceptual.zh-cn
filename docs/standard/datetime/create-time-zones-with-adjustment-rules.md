---
title: "如何：创建带有调整规则的时区 | Microsoft Docs"
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
  - "时区 [.NET Framework], 和调整规则"
  - "时区 [.NET Framework], 创建"
ms.assetid: c52ef192-13a9-435f-8015-3b12eae8c47c
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：创建带有调整规则的时区
在特定的系统上，应用程序需要的精确时区信息可能不存在，这有多种原因：  
  
-   本地系统的注册表中从未定义该时区。  
  
-   有关该时区的数据已被修改或已从注册表中移除。  
  
-   该时区不具有与特定历史时期的时区调整有关的信息。  
  
 在这些情况下，可以调用 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 方法定义应用程序所需的时区。  您可以使用此方法的重载创建带有或不带调整规则的时区。  如果该时区支持夏时制，则可以用固定调整规则或浮动调整规则来定义调整方式（有关这些术语的定义，请参见[时区概述](../../../docs/standard/datetime/time-zone-overview.md)中的“时区术语”一节）。  
  
> [!IMPORTANT]
>  通过调用 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 方法创建的自定义时区不会被添加到注册表中。  它们只能通过由 <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> 方法调用返回的对象引用进行访问。  
  
 本主题介绍如何创建带调整规则的时区。  若要创建不支持夏时制调整规则的时区，请参见[如何：创建不带调整规则的时区](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md)。  
  
### 创建带浮动调整规则的时区  
  
1.  对于每次调整（即每次经过特定的时间间隔对标准时间的来回转换），请执行下列操作：  
  
    1.  定义时区调整的开始转换时间。  
  
         必须调用 <xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A?displayProperty=fullName> 方法并向其传递下列值：一个定义转换时间的 <xref:System.DateTime> 值、一个定义转换发生在哪个月份的整数值、一个定义转换发生在哪个星期的整数值以及一个定义转换发生在星期几的 <xref:System.DayOfWeek> 值。  此方法调用会实例化 <xref:System.TimeZoneInfo.TransitionTime> 对象。  
  
    2.  定义时区调整的结束转换时间。  这需要再次调用 <xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A?displayProperty=fullName> 方法。  此方法调用会实例化另一个 <xref:System.TimeZoneInfo.TransitionTime> 对象。  
  
    3.  调用 <xref:System.TimeZoneInfo.AdjustmentRule.CreateAdjustmentRule%2A> 方法并向其传递以下内容：调整的有效开始日期和结束日期、一个定义转换时间长度的 <xref:System.TimeSpan> 对象、两个分别定义来回转换夏时制的时间的 <xref:System.TimeZoneInfo.TransitionTime> 对象。  此方法调用会实例化 <xref:System.TimeZoneInfo.AdjustmentRule> 对象。  
  
    4.  将 <xref:System.TimeZoneInfo.AdjustmentRule> 对象分配给 <xref:System.TimeZoneInfo.AdjustmentRule> 对象的数组。  
  
2.  定义时区的显示名称。  显示名称应遵循相对标准的格式，其中时区的协调世界时 \(UTC\) 偏移量用括号括起来，后面是一个字符串，用于标识时区、该时区中的一个或多个城市或者该时区中的一个或多个国家\/地区。  
  
3.  定义时区的标准时间名称。  此字符串通常还用作时区的标识符。  
  
4.  定义时区的夏时制名称。  
  
5.  如果要使用不同于时区标准名称的标识符，请定义时区标识符。  
  
6.  实例化定义时区的 UTC 偏移量的 <xref:System.TimeSpan> 对象。  时间晚于 UTC 的时区有正偏移值。  时间早于 UTC 的时区有负偏移值。  
  
7.  调用 [TimeZoneInfo.CreateCustomTimeZone\(String, TimeSpan, String, String, String, TimeZoneInfo.AdjustmentRule\<xref:System.TimeZoneInfo.CreateCustomTimeZone%28System.String%2CSystem.TimeSpan%2CSystem.String%2CSystem.String%2CSystem.String%2CSystem.TimeZoneInfo.AdjustmentRule%5B%5D%29?displayProperty=fullName> 方法可实例化新时区。  
  
## 示例  
 下面的示例定义了一个美国中部标准时区，其中包括从 1918 年至今的多个时间间隔的调整规则。  
  
 [!code-csharp[System.TimeZone2.CreateTimeZone#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#5)]
 [!code-vb[System.TimeZone2.CreateTimeZone#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#5)]  
  
 此示例中创建的时区有多个调整规则。  请注意，必须确保任何调整规则的有效开始日期和结束日期都不与其他调整规则的日期重叠。  如果存在重叠，则将引发 <xref:System.InvalidTimeZoneException>。  
  
 对于浮动调整规则，此示例向 <xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A> 方法的 `week` 参数传递值 5，用于指示转换发生在某个特定月份的最后一个星期。  
  
 在创建要在 [TimeZoneInfo.CreateCustomTimeZone\(String, TimeSpan, String, String, String, TimeZoneInfo.AdjustmentRule\<xref:System.TimeZoneInfo.CreateCustomTimeZone%28System.String%2CSystem.TimeSpan%2CSystem.String%2CSystem.String%2CSystem.String%2CSystem.TimeZoneInfo.AdjustmentRule%5B%5D%29?displayProperty=fullName> 方法调用中使用的 <xref:System.TimeZoneInfo.AdjustmentRule> 对象数组时，该代码可以初始化该数组，以使其大小满足要为时区创建的调整次数的需要。  不过，此代码示例改为调用 <xref:System.Collections.Generic.List%601.Add%2A> 方法，以将每个调整规则添加到 <xref:System.TimeZoneInfo.AdjustmentRule> 对象的泛型集合 <xref:System.Collections.Generic.List%601> 中。  然后，该代码调用 <xref:System.Collections.Generic.List%601.CopyTo%2A> 方法将此集合的成员复制到该数组中。  
  
 该示例还使用 <xref:System.TimeZoneInfo.TransitionTime.CreateFixedDateRule%2A> 方法定义固定日期的调整。  这与调用 <xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A> 方法相似，但此调用只需要转换参数中的时间、月份和日期。  
  
 该示例可使用如下代码进行测试：  
  
 [!code-csharp[System.TimeZone2.CreateTimeZone#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#7)]
 [!code-vb[System.TimeZone2.CreateTimeZone#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#7)]  
  
## 编译代码  
 此示例需要：  
  
-   在项目中添加一个对 System.Core.dll 的引用。  
  
-   导入下列命名空间：  
  
     [!code-csharp[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#6)]
     [!code-vb[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#6)]  
  
## 请参阅  
 [日期、时间和时区](../../../docs/standard/datetime/index.md)   
 [时区概述](../../../docs/standard/datetime/time-zone-overview.md)   
 [如何：创建不带调整规则的时区](../../../docs/standard/datetime/create-time-zones-without-adjustment-rules.md)