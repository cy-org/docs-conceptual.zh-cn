---
title: "如何：解决不明确的时间 | Microsoft Docs"
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
  - "不明确的时间 [.NET Framework]"
  - "时区 [.NET Framework], 不明确的时间"
ms.assetid: 2cf5fb25-492c-4875-9245-98cac8348e97
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：解决不明确的时间
不明确的时间是指映射到多个协调世界时 \(UTC\) 的时间。  当向回调整时钟时间时（例如某时区在从夏时制转换为标准时间的过程中），就会出现此情况。  在处理不明确的时间时，可执行下列操作之一：  
  
-   就时间映射到 UTC 的方式进行假设。  例如，可以假定某个不明确的时间始终表示为时区的标准时间。  
  
-   如果该不明确的时间是用户输入的数据项，则可将这种多义性留给用户解决。  
  
 本主题介绍如何通过假定不明确的时间表示时区的标准时间来解决它。  
  
### 将不明确的时间映射到时区的标准时间  
  
1.  调用 <xref:System.TimeZoneInfo.IsAmbiguousTime%2A> 方法以确定时间是否明确。  
  
2.  如果时间不明确，请从时区的 <xref:System.TimeZoneInfo.BaseUtcOffset%2A> 属性返回的 <xref:System.TimeSpan> 对象中减去该时间。  
  
3.  调用 `static`（在 Visual Basic .NET 中为 `Shared`）<xref:System.DateTime.SpecifyKind%2A> 方法，以将 UTC 日期和时间值的 <xref:System.DateTime.Kind%2A> 属性设置为 <xref:System.DateTimeKind?displayProperty=fullName>。  
  
## 示例  
 下面的示例演示如何将不明确的时间转换为 UTC。此示例假定该不明确的时间表示本地时区的标准时间。  
  
 [!code-csharp[System.TimeZone2.Concepts#10](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#10)]
 [!code-vb[System.TimeZone2.Concepts#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#10)]  
  
 该示例包含一个名为 `ResolveAmbiguousTime` 的方法，该方法可确定传递给它的 <xref:System.DateTime> 值是否为不明确的。  如果该值是不明确的，该方法将返回一个表示相应 UTC 时间的 <xref:System.DateTime> 值。  该方法通过从本地时间中减去本地时区的 <xref:System.TimeZoneInfo.BaseUtcOffset%2A> 属性值来处理此转换。  
  
 通常，处理不明确的时间的方法是调用 <xref:System.TimeZoneInfo.GetAmbiguousTimeOffsets%2A> 方法以检索 <xref:System.TimeSpan> 对象的数组，这些对象包含不明确时间的各种可能的 UTC 偏移量。  但是，此示例进行了主观假设：不明确的时间应始终映射到时区的标准时间。  <xref:System.TimeZoneInfo.BaseUtcOffset%2A> 属性返回 UTC 和时区标准时间之间的偏移量。  
  
 在此示例中，本地时区都通过 <xref:System.TimeZoneInfo.Local%2A?displayProperty=fullName> 属性来引用，而从未分配给对象变量。  这是一种建议做法，因为调用 <xref:System.TimeZoneInfo.ClearCachedData%2A?displayProperty=fullName> 方法会使分配了本地时区的任何对象都失效。  
  
## 编译代码  
 此示例需要：  
  
-   在项目中添加一个对 System.Core.dll 的引用。  
  
-   使用 `using` 语句导入 <xref:System> 命名空间（在 C\# 代码中需要）。  
  
## 请参阅  
 [日期、时间和时区](../../../docs/standard/datetime/index.md)   
 [如何：让用户解决不明确的时间](../../../docs/standard/datetime/let-users-resolve-ambiguous-times.md)