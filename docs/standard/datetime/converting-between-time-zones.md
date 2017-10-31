---
title: "在不同时区之间转换时间 | Microsoft Docs"
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
  - "转换时间"
  - "本地时间转换"
  - "时区 [.NET Framework], 转换"
  - "时间 [.NET Framework], 转换"
  - "UTC 时间, 转换"
ms.assetid: a51e1a3b-c983-4320-b31a-1f9fa3cf824a
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# 在不同时区之间转换时间
对于处理日期和时间的任何应用程序而言，正确处理不同时区之间的差异愈发重要。  应用程序不能再假定所有时间都可以表示为本地时间（<xref:System.DateTime> 结构中的时间）。  例如，显示美国东部当前时间的网页对于东亚地区的客户来说便缺乏可信度。  本主题将说明如何在不同时区之间转换时间，以及如何转换可提供有限时区识别能力的 <xref:System.DateTimeOffset> 值。  
  
## 转换为协调世界时  
 协调世界时 \(UTC\) 是一个高精度的原子时间标准。  世界上的所有时区都可以表示为 UTC 加上或减去一个偏移量。  因此，UTC 提供了一种与时区无关（或非特定于时区）的时间。  如果日期和时间在计算机之间的可迁移性非常重要，则建议使用 UTC 时间。（有关详细信息以及使用日期和时间的其他最佳方案，请参见 [Coding Best Practices Using DateTime in the .NET Framework](http://go.microsoft.com/fwlink/?LinkId=92342)。）通过将各个时区转换为 UTC，可以简化时间的比较。  
  
> [!NOTE]
>  还可以序列化 <xref:System.DateTimeOffset> 结构，以便明确地表示单个时间点。  由于 <xref:System.DateTimeOffset> 对象存储了日期和时间值及其 UTC 偏移量，因此它们表示的特定时间点始终与 UTC 有关。  
  
 若要将时间转换为 UTC，最简单的方法是调用 `static`（在 Visual Basic 中为 `Shared`）<xref:System.TimeZoneInfo.ConvertTimeToUtc%28System.DateTime%29?displayProperty=fullName> 方法。  该方法所执行的具体转换取决于 `dateTime` 参数的 <xref:System.DateTime.Kind%2A> 属性值，如下表所示。  
  
|DateTime.Kind 属性|转换|  
|----------------------|--------|  
|<xref:System.DateTimeKind?displayProperty=fullName>|将本地时间转换为 UTC。|  
|<xref:System.DateTimeKind?displayProperty=fullName>|将 `dateTime` 参数假定为本地时间并将本地时间转换为 UTC。|  
|<xref:System.DateTimeKind?displayProperty=fullName>|返回未更改的 `dateTime` 参数。|  
  
 下面的代码将当前本地时间转换为 UTC 并将结果显示在控制台上。  
  
 [!code-csharp[System.TimeZone2.Concepts#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#6)]
 [!code-vb[System.TimeZone2.Concepts#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#6)]  
  
> [!NOTE]
>  <xref:System.TimeZoneInfo.ConvertTimeToUtc%28System.DateTime%29?displayProperty=fullName> 方法生成的结果不必与 <xref:System.TimeZone.ToUniversalTime%2A?displayProperty=fullName> 和 <xref:System.DateTime.ToUniversalTime%2A?displayProperty=fullName> 方法相同。  如果主机系统的本地时区包含多个调整规则，<xref:System.TimeZoneInfo.ConvertTimeToUtc%28System.DateTime%29?displayProperty=fullName> 将向特定的日期和时间应用相应的规则。  其他两个方法始终应用最新的调整规则。  
  
 如果日期和时间值不表示本地时间或 UTC，<xref:System.DateTime.ToUniversalTime%2A> 方法将可能返回错误的结果。  但是，可以使用 <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A?displayProperty=fullName> 方法转换指定时区的日期和时间（有关检索表示目标时区的 <xref:System.TimeZoneInfo> 对象的详细信息，请参见[查找在本地系统上定义的时区](../../../docs/standard/datetime/finding-the-time-zones-on-local-system.md)）。下面的代码使用 <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A?displayProperty=fullName> 方法将东部标准时间转换为 UTC。  
  
 [!code-csharp[System.TimeZone2.Concepts#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#7)]
 [!code-vb[System.TimeZone2.Concepts#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#7)]  
  
 请注意，如果 <xref:System.DateTime> 对象的 <xref:System.DateTime.Kind%2A> 属性与时区不匹配，此方法将引发 <xref:System.ArgumentException>。  如果 <xref:System.DateTime.Kind%2A> 属性为 <xref:System.DateTimeKind?displayProperty=fullName> 但 <xref:System.TimeZoneInfo> 对象并不表示本地时区，或者如果 <xref:System.DateTime.Kind%2A> 属性为 <xref:System.DateTimeKind?displayProperty=fullName> 但 <xref:System.TimeZoneInfo> 对象并不等于 <xref:System.DateTimeKind?displayProperty=fullName>，则将出现不匹配的情况。  
  
 所有这些方法都将 <xref:System.DateTime> 值作为参数并返回一个 <xref:System.DateTime> 值。  对于 <xref:System.DateTimeOffset> 值，<xref:System.DateTimeOffset> 结构都有一个 <xref:System.DateTimeOffset.ToUniversalTime%2A> 实例方法，该方法可将当前实例的日期和时间转换为 UTC。下面的示例通过调用 <xref:System.DateTimeOffset.ToUniversalTime%2A> 方法将本地时间以及几个其他时间转换为协调世界时 \(UTC\)。  
  
 [!code-csharp[System.DateTimeOffset.Methods#16](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Methods/cs/Methods.cs#16)]
 [!code-vb[System.DateTimeOffset.Methods#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Methods/vb/Methods.vb#16)]  
  
## 将 UTC 转换为指定的时区  
 若要将 UTC 转换为本地时间，请参见下面的“将 UTC 转换为本地时间”一节。  若要将 UTC 转换为任何指定时区中的时间，请调用 <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A> 方法。  该方法有两个参数：  
  
-   要转换的 UTC。  此参数必须是<xref:System.DateTime.Kind%2A>属性设置为<xref:System.DateTimeKind?displayProperty=fullName> 或<xref:System.DateTimeKind?displayProperty=fullName>的<xref:System.DateTime>值。  
  
-   要将 UTC 转换到的时区。  
  
 下面的代码将 UTC 转换为中部标准时间。  
  
 [!code-csharp[System.TimeZone2.Concepts#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#8)]
 [!code-vb[System.TimeZone2.Concepts#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#8)]  
  
## 将 UTC 转换为本地时间  
 若要将 UTC 转换为本地时间，请调用要转换其时间的 <xref:System.DateTime> 对象的 <xref:System.DateTime.ToLocalTime%2A> 方法。  该方法的具体行为取决于该对象的 <xref:System.DateTime.Kind%2A> 属性值，如下表所示。  
  
|`DateTime.Kind` 属性|转换|  
|------------------------|--------|  
|`DateTimeKind.Local`|返回未更改的 <xref:System.DateTime> 值。|  
|`DateTimeKind.Unspecified`|假定 <xref:System.DateTime> 值为 UTC 并将 UTC 转换为本地时间。|  
|`DateTimeKind.Utc`|将 <xref:System.DateTime> 值转换为本地时间。|  
  
 **注意**：<xref:System.TimeZone.ToLocalTime%2A?displayProperty=fullName> 方法的行为与 `DateTime.ToLocalTime` 方法完全相同。该方法带有一个参数，即要转换的日期和时间值。  
  
 另外，您还可以使用 `static`（在 Visual Basic 中为 `Shared`）<xref:System.TimeZoneInfo.ConvertTime%2A?displayProperty=fullName> 方法将任何指定时区中的时间转换为本地时间。  下一节将对此技术加以讨论。  
  
## 在任意两个时区之间转换  
 通过使用 <xref:System.TimeZoneInfo> 类的以下两个 `static`（在 Visual Basic 中为 `Shared`）方法当中的任意一个，可以在任意两个时区之间进行转换：  
  
-   <xref:System.TimeZoneInfo.ConvertTime%2A>  
  
     此方法有三个参数：要转换的日期和时间值、一个表示该日期和时间值的时区的 `TimeZoneInfo` 对象以及一个表示要将该日期和时间值转换到的时区的 `TimeZoneInfo` 对象。  
  
-   <xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A>  
  
     此方法也有三个参数：要转换的日期和时间值、该日期和时间值的时区的标识符以及要将该日期和时间值转换到的时区的标识符。  
  
 这两个方法都要求让要转换的日期和时间值的 <xref:System.DateTime.Kind%2A> 属性与表示其时区的 <xref:System.TimeZoneInfo> 对象或时区标识符相互对应。  否则会引发 <xref:System.ArgumentException>。  例如，如果日期和时间值的 `Kind` 属性为 `DateTimeKind.Local`，则当作为参数传递给方法的 `TimeZoneInfo` 对象不等于 `TimeZoneInfo.Local` 时，便会引发异常。  另外，如果作为参数传递给方法的标识符不等于 `TimeZoneInfo.Local.Id`，则也会引发异常。  
  
 下面的示例使用 <xref:System.TimeZoneInfo.ConvertTime%2A> 方法将夏威夷标准时间转换为本地时间。  
  
 [!code-csharp[System.TimeZone2.Concepts#9](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#9)]
 [!code-vb[System.TimeZone2.Concepts#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#9)]  
  
## 转换 DateTimeOffset 值  
 通过由 <xref:System.DateTimeOffset> 对象表示的日期和时间值并不能完全确定时区，因为该对象在实例化时会解除与其时区的关联。  但在很多情况下，应用程序只需基于两个不同的 UTC 偏移量而不是特定时区中的时间即可完成日期和时间的转换。  若要执行此转换，可以调用当前实例的 <xref:System.DateTimeOffset.ToOffset%2A> 方法。  该方法有一个参数，即该方法要返回的新日期和时间值的偏移量。  
  
 例如，如果已知用户请求网页的日期和时间，且该日期和时间已用 MM\/dd\/yyyy hh:mm:ss zzzz 格式序列化为一个字符串，则下面的 `ReturnTimeOnServer` 方法会将此日期和时间值转换为 Web 服务器上的日期和时间。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.OffsetConversions#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/cs/TimeConversions.cs#1)]
 [!code-vb[System.DateTimeOffset.Conceptual.OffsetConversions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/vb/TimeConversions.vb#1)]  
  
 如果向该方法传递字符串“9\/1\/2007 5:32:07 \-05:00”（表示比 UTC 早五个小时的时区中的日期和时间），则对于处在美国太平洋标准时区中的服务器，  
  
 <xref:System.TimeZoneInfo> 类还包含 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=fullName> 方法的重载，该重载使用 <xref:System.DateTimeOffset> 值执行时区转换。  该方法有两个参数：一个是 <xref:System.DateTimeOffset> 值，另一个是对要将时间转换到的时区的引用。  该方法调用会返回 <xref:System.DateTimeOffset> 值。  例如，可按以下方式重写上一示例中的 `ReturnTimeOnServer` 方法，以调用 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29> 方法。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.OffsetConversions#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/cs/timeconversions2.cs#2)]
 [!code-vb[System.DateTimeOffset.Conceptual.OffsetConversions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.OffsetConversions/vb/TimeConversions2.vb#2)]  
  
## 请参阅  
 <xref:System.TimeZoneInfo>   
 [日期、时间和时区](../../../docs/standard/datetime/index.md)   
 [查找在本地系统上定义的时区](../../../docs/standard/datetime/finding-the-time-zones-on-local-system.md)