---
title: "如何：往返日期和时间值 | Microsoft Docs"
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
  - "往返行程日期和时间值"
  - "日期 [.NET Framework]，往返值"
  - "时区 [.NET Framework]，往返日期和时间值"
  - "时间 [.NET Framework]，往返值"
  - "格式设置字符串 [.NET Framework]，往返值"
ms.assetid: b609b277-edc6-4c74-b03e-ea73324ecbdb
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：往返日期和时间值
在许多应用程序中，日期和时间值可用于明确地标识单个时间点。  本主题演示如何将 <xref:System.DateTime> 值、<xref:System.DateTimeOffset> 值以及日期和时间值与时区信息一起进行保存和还原，以便还原值可以标识与保存值相同的时间。  
  
### 保存\/还原 DateTime 值  
  
1.  通过使用“o”格式说明符调用  <xref:System.DateTime.ToString%28System.String%29?displayProperty=fullName>方法，将 <xref:System.DateTime>值转换为相应的字符串表示形式。  
  
2.  将 <xref:System.DateTime> 值的字符串表示形式保存到文件中，或跨越进程、应用程序域或计算机边界传递它。  
  
3.  检索表示 <xref:System.DateTime> 值的字符串。  
  
4.  调用 <xref:System.DateTime.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=fullName> 方法，并将 <xref:System.Globalization.DateTimeStyles?displayProperty=fullName> 作为 `styles` 参数的值传递。  
  
 下面的示例说明如何保存\/还原 <xref:System.DateTime> 值。  
  
 [!code-csharp[Formatting.HowTo.RoundTrip#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#1)]
 [!code-vb[Formatting.HowTo.RoundTrip#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#1)]  
  
 保存\/还原 <xref:System.DateTime> 值时，此方法可成功地保留所有本地时间和世界时间的时间。  例如，如果本地 <xref:System.DateTime> 值保存在美国太平洋标准时区系统上并且在美国中部标准时区的系统上的被还原，还原的日期和时间将比原始时间晚两个小时，这反映了两个时区之间的时差。  但是，此方法对于未明确的时间不一定准确。  其 <xref:System.DateTime.Kind%2A> 属性为 <xref:System.DateTimeKind> 的所有 <xref:System.DateTime> 值都会作为本地时间进行处理。  如果不是这样，<xref:System.DateTime> 将不会成功标识正确的时间点。  此限制的解决方法是在保存和还原操作中将日期和时间值与对应的时区紧密耦合在一起。  
  
### 保存\/还原 DateTimeOffset 值  
  
1.  通过使用“o”格式说明符调用<xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=fullName>方法，将<xref:System.DateTimeOffset> 值转换为相应的字符串表示形式。  
  
2.  将 <xref:System.DateTimeOffset> 值的字符串表示形式保存到文件中，或跨越进程、应用程序域或计算机边界传递它。  
  
3.  检索表示 <xref:System.DateTimeOffset> 值的字符串。  
  
4.  调用 <xref:System.DateTimeOffset.Parse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%29?displayProperty=fullName> 方法，并将 <xref:System.Globalization.DateTimeStyles?displayProperty=fullName> 作为 `styles` 参数的值传递。  
  
 下面的示例说明如何保存\/还原 <xref:System.DateTimeOffset> 值。  
  
 [!code-csharp[Formatting.HowTo.RoundTrip#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#2)]
 [!code-vb[Formatting.HowTo.RoundTrip#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#2)]  
  
 此方法始终可以将 <xref:System.DateTimeOffset> 值明确标识为单个时间点。  然后，可以通过调用 <xref:System.DateTimeOffset.ToUniversalTime%2A?displayProperty=fullName> 方法将该值转换为协调世界时 \(UTC\)，或通过调用 <xref:System.DateTimeOffset.ToOffset%2A?displayProperty=fullName> 或 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=fullName> 方法将该值转换为某个特定时区的时间。  此方法的主要限制是日期和时间算法，当对表示某个特定时区中的时间的 <xref:System.DateTimeOffset> 值执行日期和时间算法时，可能不会得到对应于该时区的准确结果。  这是因为在实例化 <xref:System.DateTimeOffset> 值时，该值会与其时区解除关联。  因此，当执行日期和时间计算时，不会再应用该时区的调整规则。  通过定义包括日期和时间值以及其相应时区的自定义类型，可以解决此问题。  
  
### 保存\/还原带有时区的日期和时间值  
  
1.  定义带有两个字段的类或结构。  第一个字段是 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 对象，第二个字段是 <xref:System.TimeZoneInfo> 对象。  下面的示例是此类型的一个简单版本。  
  
     [!code-csharp[Formatting.HowTo.RoundTrip#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#3)]
     [!code-vb[Formatting.HowTo.RoundTrip#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#3)]  
  
2.  使用 <xref:System.SerializableAttribute> 特性标记该类。  
  
3.  使用 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Serialize%2A?displayProperty=fullName> 方法序列化对象。  
  
4.  使用 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter.Deserialize%2A> 方法还原对象。  
  
5.  将反序列化对象强制转换（在 C\# 中）或转换（在 Visual Basic 中）为相应类型的对象。  
  
 下面的示例演示如何保存\/还原存储日期和时间以及时区信息的对象。  
  
 [!code-csharp[Formatting.HowTo.RoundTrip#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/cs/RoundTrip.cs#4)]
 [!code-vb[Formatting.HowTo.RoundTrip#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.RoundTrip/vb/RoundTrip.vb#4)]  
  
 在保存和还原日期和时间值的前后，此方法都应始终明确地反映正确的时间点，前提是日期和时间与时区的组合对象的实现不允许日期值与时间值不同步。  
  
## 编译代码  
 这些示例要求：  
  
-   使用 C\# `using` 语句或 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] `Imports` 语句导入下列命名空间：  
  
    -   <xref:System>（仅用于 C\#）  
  
    -   <xref:System.Globalization?displayProperty=fullName>.  
  
    -   <xref:System.IO?displayProperty=fullName>.  
  
    -   <xref:System.Runtime.Serialization?displayProperty=fullName>.  
  
    -   <xref:System.Runtime.Serialization.Formatters.Binary?displayProperty=fullName>.  
  
-   对 System.Core.dll 的引用。  
  
-   除 `DateInTimeZone` 类之外的每个代码示例，应包含在一个类或 Visual Basic 模型中，并包装在方法中，然后从 `Main` 方法调用。  
  
## 请参阅  
 [执行格式设置操作](../../../docs/standard/base-types/performing-formatting-operations.md)   
 [在 DateTime、DateTimeOffset、TimeSpan 和 TimeZoneInfo 之间进行选择](../../../ocs/standard/datetime/choosing-between-datetime.md)   
 [标准日期和时间格式字符串](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)