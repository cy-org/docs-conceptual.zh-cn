---
title: "使用日期和时间执行算术运算 | Microsoft Docs"
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
  - "算术运算 [.NET Framework], 日期和时间"
  - "日期 [.NET Framework], 算术运算"
  - "日期 [.NET Framework], 比较"
  - "DateTime 结构, 算术运算"
  - "DateTimeOffset 结构, 算术运算"
  - "时区 [.NET Framework], 算术运算"
  - "时间 [.NET Framework], 算术运算"
ms.assetid: 87c7ddf2-f15e-48af-8602-b3642237e6d0
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# 使用日期和时间执行算术运算
虽然 <xref:System.DateTime> 和 <xref:System.DateTimeOffset> 结构都提供对其值执行算术运算的成员，但是算术运算的结果却截然不同。  本主题将分析这些差异，将它们与日期和时间数据中的时区识别能力的程度相关联，并讨论如何使用日期和时间数据执行完全时区识别运算。  
  
## 使用 DateTime 值进行比较和算术运算  
 从 .NET Framework 2.0 版开始，<xref:System.DateTime> 值具有有限程度的时区识别能力。  <xref:System.DateTime.Kind%2A?displayProperty=fullName> 属性允许将 <xref:System.DateTimeKind> 值赋给日期和时间，以指示它表示的是本地时间、协调世界时 \(UTC\) 还是未指定的时区中的时间。  但是，当比较 <xref:System.DateTime> 值或对其执行日期和时间算术运算时将忽略这些有限的时区信息。  下面的示例阐释了这一点，它对当前的本地时间与当前的 UTC 时间进行比较。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual2.cs#2)]
 [!code-vb[System.DateTimeOffset.Conceptual#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual2.vb#2)]  
  
 <xref:System.DateTime.CompareTo%28System.DateTime%29>方法报告本地时间比 UTC 时间早（或小），并且减法操作暗示 U.S. Pacific Standard Time的系统的UTC和本地化时间的时差是7个小时。  但由于这两个值提供了单个时间点的不同表示形式，因此，在本例中很明显这个时间间隔完全可归因于本地时区相对于 UTC 的偏移量。  
  
 一般来说，<xref:System.DateTime.Kind%2A?displayProperty=fullName> 属性虽然能够影响对 <xref:System.DateTime> 比较和算术方法返回的结果的解释，但是它不会影响这些结果（正如对两个相同的时间点的比较所指示的那样）。  例如：  
  
-   对两个其 <xref:System.DateTime.Kind%2A?displayProperty=fullName> 属性都等于 <xref:System.DateTimeKind> 的日期和时间值执行的任何算术运算的结果都反映这两个值之间实际的时间间隔。  同样，对两个此类日期和时间值的比较准确反映两个时间之间的关系。  
  
-   对两个其 <xref:System.DateTime.Kind%2A?displayProperty=fullName> 属性都等于 <xref:System.DateTimeKind> 的日期和时间值或者对两个其 <xref:System.DateTime.Kind%2A?displayProperty=fullName> 属性值不同的日期和时间值执行的任何算术或比较运算的结果都反映这两个值在时钟时间上的差异。  
  
-   对本地日期和时间值执行的算术或比较运算不考虑某个特定值是否是不明确的或无效的，也不考虑由于本地时区与夏时制之间的转换带来的任何调整规则的影响。  
  
-   任何比较或计算 UTC 与本地时间之差的运算的结果中都包括一个等于本地时区相对于 UTC 的偏移量的时间间隔。  
  
-   任何比较或计算未指定的时间与 UTC 或本地时间之差的运算都反映简单的时钟时间。  不会考虑时区差异，并且结果不反映时区调整规则的应用。  
  
-   任何比较或计算两个未指定的时间之差的运算都可能包括未知的时间间隔以反映两个不同的时区中的时间的差异。  
  
 有许多这样的方案，在这些方案中，时区差异不会影响日期和时间计算（有关其中一些方案的讨论，请参见[在 DateTime、DateTimeOffset、TimeSpan 和 TimeZoneInfo 之间进行选择](../../../docs/standard/datetime/choosing-between-datetime.md)），或者在这些方案中日期和时间数据的上下文定义比较或算术运算的含义。  
  
## 使用 DateTimeOffset 值进行比较和算术运算  
 <xref:System.DateTimeOffset> 值不仅包括日期和时间，而且还包括一个偏移量，它明确地定义该日期和时间相对于 UTC 的偏移量。  这使得可以定义与 <xref:System.DateTime> 值稍有不同的相等关系。  然而，如果它们的日期和时间值相同，则 <xref:System.DateTime> 值相等；如果它们指的都是同一个时间点，则 <xref:System.DateTimeOffset> 值相等。  这使得当在比较和大多数确定两个日期和时间之间的时间间隔的算术运算中使用时，<xref:System.DateTimeOffset> 值更精确，需要的解释更少。  下面的示例阐释了这种行为差异，它等效于前面的比较本地和 UTC <xref:System.DateTime> 值的示例，只是它是针对 <xref:System.DateTimeOffset> 的。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual3.cs#3)]
 [!code-vb[System.DateTimeOffset.Conceptual#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual3.vb#3)]  
  
 在本示例中，<xref:System.DateTimeOffset.CompareTo%2A> 方法指示当前本地时间与当前 UTC 时间相等，而 <xref:System.DateTimeOffset> 值的减法运算指示这两个时间之差是 <xref:System.TimeSpan.Zero?displayProperty=fullName>。  
  
 在日期和时间算术中使用 <xref:System.DateTimeOffset> 值的主要限制是虽然 <xref:System.DateTimeOffset> 值具有一定的时区识别能力，但它们没有完全的时区识别能力。  虽然首次为 <xref:System.DateTimeOffset> 变量赋值时 <xref:System.DateTimeOffset> 值的偏移量反映时区相对于 UTC 的偏移量，但以后它就与时区解除关联了。  由于它不再直接与可识别的时间关联，因此日期和时间间隔的加减运算不考虑时区的调整规则。  
  
 为了说明，美国中部标准时间区域中夏时制的转换发生在 2008 年 3 月 9 日凌晨 2:00 。  这意味为2008 年 3 月 9 日凌晨 1:30 的中部标准时间增加两个或一半个时间间隔 ，应生成 2008 年 3 月 9 日凌晨 5:00 的日期和时间。  但是，如下面的示例所示，加法运算的结果是2008 年 3 月 9 日凌晨 4:00。  请注意，虽然此运算的这个结果并不是我们感兴趣的时区中的时间（即，它没有预期的时区偏移量），但它确实表示正确的时间点。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual4.cs#4)]
 [!code-vb[System.DateTimeOffset.Conceptual#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual4.vb#4)]  
  
## 使用时区中的时间执行算术运算  
 <xref:System.TimeZoneInfo> 类包括多种转换方法，这些转换方法在将时间从一个时区转换为另一个时区时会自动应用调整。  这些要求包括：  
  
-   <xref:System.TimeZoneInfo.ConvertTime%2A> 和 <xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A> 方法，在任意两个时区之间转换时间。  
  
-   <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A> 和 <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A> 方法，将某个特定的时区中的时间转换为 UTC，或者将 UTC 转换为某个特定的时区中的时间。  
  
 有关详细信息，请参见[在不同时区之间转换时间](../../../docs/standard/datetime/converting-between-time-zones.md)。  
  
 <xref:System.TimeZoneInfo> 类并没有提供任何在您执行日期和时间算术运算时自动应用调整规则的方法。  但是，您可以通过以下操作来实现这一点：将某个时区中的时间转换为 UTC，执行算术运算，然后从 UTC 转换回该时区中的时间。  有关详细信息，请参见[如何：在日期和时间算法中使用时区](../../../docs/standard/datetime/use-time-zones-in-arithmetic.md)。  
  
 例如，下面的代码类似于前面向2008 年 3 月 9 日凌晨 2:00 增加两个半小时的代码。  但是，由于它在执行日期和时间算术运算之前将中部标准时间转换成了 UTC，然后再将结果从 UTC 转换回中部标准时间，因此得到的时间反映了中部标准时区到夏时制的转换。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual5.cs#5)]
 [!code-vb[System.DateTimeOffset.Conceptual#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual5.vb#5)]  
  
## 请参阅  
 [日期、时间和时区](../../../docs/standard/datetime/index.md)   
 [如何：在日期和时间算法中使用时区](../../../docs/standard/datetime/use-time-zones-in-arithmetic.md)