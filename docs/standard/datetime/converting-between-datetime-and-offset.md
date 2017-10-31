---
title: "在 DateTime 与 DateTimeOffset 之间进行转换 | Microsoft Docs"
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
  - "转换 DateTimeOffset 和 DateTime 值"
  - "转换时间"
  - "日期数据类型, 转换"
  - "日期 [.NET Framework], 转换"
  - "DateTime 结构, 转换"
  - "DateTimeOffset 结构, 转换"
  - "本地时间转换"
  - "时区 [.NET Framework], 转换"
  - "UTC 时间, 转换"
ms.assetid: b605ff97-0c45-4c24-833f-4c6a3e8be64c
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# 在 DateTime 与 DateTimeOffset 之间进行转换
虽然与 <xref:System.DateTime> 结构相比 <xref:System.DateTimeOffset> 结构提供了更高程度的时区识别能力，但在方法调用中 <xref:System.DateTime> 参数更常用。  因此，将 <xref:System.DateTimeOffset> 值转换为 <xref:System.DateTime> 值（反之亦然）的能力就尤为重要。  本主题演示如何在保留尽可能多的时区信息的情况下执行这些转换。  
  
> [!NOTE]
>  表示时区中的时间时，<xref:System.DateTime> 和 <xref:System.DateTimeOffset> 类型都有一些限制。  通过其 <xref:System.DateTime.Kind%2A> 属性，<xref:System.DateTime> 只能反映协调世界时 \(UTC\) 和系统的本地时区。  <xref:System.DateTimeOffset> 反映时间相对于 UTC 的偏移量，但它不反映该偏移量所属的实际时区。  有关时间值和对时区的支持的详细信息，请参见[在 DateTime、DateTimeOffset、TimeSpan 和 TimeZoneInfo 之间进行选择](../../../docs/standard/datetime/choosing-between-datetime.md)。  
  
## 从 DateTime 到 DateTimeOffset 的转换  
 <xref:System.DateTimeOffset> 结构提供了两种等效的方式来执行从 <xref:System.DateTime> 到 <xref:System.DateTimeOffset> 的转换，这两种方式适用于大多数转换：  
  
-   <xref:System.DateTimeOffset.%23ctor%2A> 构造函数，它根据 <xref:System.DateTime> 值创建新的 <xref:System.DateTimeOffset> 对象。  
  
-   隐式转换运算符，它允许您为 <xref:System.DateTimeOffset> 对象分配一个 <xref:System.DateTime> 值。  
  
 对于 UTC 和本地 <xref:System.DateTime> 值，得到的 <xref:System.DateTimeOffset> 值的 <xref:System.DateTimeOffset.Offset%2A> 属性准确反映 UTC 或本地时区偏移量。  例如，下面的代码将 UTC 时间转换为与之等效的 <xref:System.DateTimeOffset> 值。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#1)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#1)]  
  
 在此例中，`utcTime2` 变量的偏移量为 00:00。  同样，下面的代码将本地时间转换为与之等效的 <xref:System.DateTimeOffset> 值。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#2)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#2)]  
  
 但是，对于其 <xref:System.DateTime.Kind%2A>属性为<xref:System.DateTimeKind?displayProperty=fullName>的<xref:System.DateTime>值，这两种转换方法将产生一个偏移量为本地时区的偏移量的<xref:System.DateTimeOffset>值。  下面的示例对此进行了演示，该示例使用美国太平洋标准时区。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#3)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#3)]  
  
 如果 <xref:System.DateTime> 值反映的是除本地时区或 UTC 之外的其他的日期和时间，您可以将它转换为 <xref:System.DateTimeOffset> 值，并通过调用重载的 <xref:System.DateTimeOffset.%23ctor%2A> 构造函数保留其时区信息。  例如，下面的示例实例化一个反映中部标准时间的 <xref:System.DateTimeOffset> 对象。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#4)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#4)]  
  
 此构造函数重载的第二个参数，应该通过调用该时间对应的时区的 <xref:System.TimeZoneInfo.GetUtcOffset%28System.DateTime%29?displayProperty=fullName>方法检索一个表示该时间相对于 UTC 的偏移量的<xref:System.TimeSpan>对象。  该方法的单个参数是表示要转换的日期和时间的 <xref:System.DateTime> 值。  如果时区支持夏时制，此参数将允许该方法确定这个特定日期和时间相应的偏移量。  
  
## 从 DateTimeOffset 到 DateTime 的转换  
 <xref:System.DateTimeOffset.DateTime%2A> 属性最常用于执行从 <xref:System.DateTimeOffset> 到 <xref:System.DateTime> 的转换。  但它返回一个其 <xref:System.DateTime.Kind%2A> 属性为 <xref:System.DateTimeKind> 的 <xref:System.DateTime> 值，如下面的示例所示。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#5)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#5)]  
  
 这意味着，如果使用了 <xref:System.DateTimeOffset.DateTime%2A> 属性，有关 <xref:System.DateTimeOffset> 值与 UTC 的关系的所有信息都将在转换中丢失。  这会影响对应于 UTC 时间或系统的本地时间的 <xref:System.DateTimeOffset> 值，因为 <xref:System.DateTimeOffset.DateTime%2A> 结构在其 <xref:System.DateTime.Kind%2A> 属性中只反映这两个时区。  
  
 若要在将 <xref:System.DateTimeOffset> 转换为 <xref:System.DateTime> 值时保留尽可能多的时区信息，您可以使用 <xref:System.DateTimeOffset.UtcDateTime%2A?displayProperty=fullName> 和 <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=fullName> 属性。  
  
### 转换 UTC 时间  
 若要指示一个转换的 <xref:System.DateTimeOffset.DateTime%2A> 值是 UTC 时间，您可以检索 <xref:System.DateTimeOffset.UtcDateTime%2A?displayProperty=fullName> 属性的值。  它在以下两个方面与 <xref:System.DateTimeOffset.DateTime%2A> 属性不同：  
  
-   它返回一个其 <xref:System.DateTime.Kind%2A> 属性为 <xref:System.DateTimeKind> 的 <xref:System.DateTime> 值。  
  
-   如果 <xref:System.DateTimeOffset.Offset%2A> 属性值不等于 <xref:System.TimeSpan.Zero?displayProperty=fullName>，它会将时间转换成 UTC。  
  
> [!NOTE]
>  如果您的应用程序要求转换的 <xref:System.DateTime> 值明确地标识单个时间点，那么您应该考虑使用 <xref:System.DateTimeOffset.UtcDateTime%2A?displayProperty=fullName> 属性来处理所有从 <xref:System.DateTimeOffset> 到 <xref:System.DateTime> 的转换。  
  
 下面的代码使用<xref:System.DateTimeOffset.UtcDateTime%2A>属性将其偏移量等于 <xref:System.TimeSpan.Zero?displayProperty=fullName>的 <xref:System.DateTimeOffset> 值转换为<xref:System.DateTime>值。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#6)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#6)]  
  
 下面的代码使用 <xref:System.DateTimeOffset.UtcDateTime%2A> 属性对 <xref:System.DateTimeOffset> 值同时执行时区转换和类型转换。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#12](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#12)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#12)]  
  
### 转换本地时间  
 若要指示一个<xref:System.DateTimeOffset>值表示本地时间，您可以将  <xref:System.DateTimeOffset.DateTime%2A?displayProperty=fullName>属性返回的<xref:System.DateTime>值传递给 `static`（在 Visual Basic 中为`Shared`）<xref:System.DateTime.SpecifyKind%2A>方法。  该方法将传递给它的日期和时间作为其第一个参数返回，并将 <xref:System.DateTime.Kind%2A> 属性设置为其第二个参数指定的值。  下面的代码使用 <xref:System.DateTime.SpecifyKind%2A> 方法转换其偏移量对应于本地时区偏移量的 <xref:System.DateTimeOffset> 值。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#7)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#7)]  
  
 您还可以使用 <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=fullName> 属性将 <xref:System.DateTimeOffset> 值转换为本地 <xref:System.DateTime> 值。  返回的 <xref:System.DateTime> 值的 <xref:System.DateTime.Kind%2A> 属性是 <xref:System.DateTimeKind>。  下面的代码使用 <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=fullName> 属性转换其偏移量对应于本地时区偏移量的 <xref:System.DateTimeOffset> 值。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#10](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#10)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#10)]  
  
 当您使用 <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=fullName>属性检索<xref:System.DateTime>值时，该属性的`get`访问器首先将<xref:System.DateTimeOffset> 值转换为 UTC，然后再通过调用 <xref:System.DateTimeOffset.ToLocalTime%2A>方法将其转换为本地时间。  这意味着您可以从 <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=fullName> 属性中检索一个值，以便在执行类型转换的同时执行时区转换。  这还意味着，在执行转换的过程中将应用本地时区的调整规则。  下面的代码阐释如何使用 <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=fullName> 属性同时执行类型转换和时区转换。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#11](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#11)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#11)]  
  
### 通用转换方法  
 下面的示例定义一个名为 `ConvertFromDateTimeOffset` 的方法，该方法将 <xref:System.DateTimeOffset> 值转换为 <xref:System.DateTime> 值。  根据其偏移量，它确定 <xref:System.DateTimeOffset> 值是 UTC 时间、本地时间，还是其他时间，并相应地定义返回的日期和时间值的 <xref:System.DateTime.Kind%2A> 属性。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#8)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#8)]  
  
 下面的示例调用 `ConvertFromDateTimeOffset` 方法转换<xref:System.DateTimeOffset> 值，这些值表示 UTC 时间，本地时间和美国中部标准时区的时间。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Conversions#9](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#9)]
 [!code-vb[System.DateTimeOffset.Conceptual.Conversions#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#9)]  
  
 请注意，此代码做出了两个假设，根据应用程序及其日期和时间值的来源，这两个假设并非始终有效：  
  
-   它假设其偏移量为 <xref:System.TimeSpan.Zero?displayProperty=fullName> 的日期和时间值表示 UTC。  实际上，UTC 不是某个特定的时区中的时间，而是世界上的时区中的时间相对它进行标准化的时间。  时区的偏移量还可以是 <xref:System.TimeSpan.Zero>。  
  
-   它假设其偏移量等于本地时区偏移量的日期和时间表示本地时区。  由于日期和时间值与其原始时区解除了关联，情况不一定是这样的；日期和时间可能源自偏移量相同的另一个时区。  
  
## 请参阅  
 [日期、时间和时区](../../../docs/standard/datetime/index.md)