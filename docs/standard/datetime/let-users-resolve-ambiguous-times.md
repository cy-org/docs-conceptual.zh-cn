---
title: "如何：让用户解决不明确的时间 | Microsoft Docs"
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
ms.assetid: bca874ee-5b68-4654-8bbd-3711220ef332
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：让用户解决不明确的时间
不明确的时间是指映射到多个协调世界时 \(UTC\) 的时间。  当向回调整时钟时间时（例如某时区在从夏时制转换为标准时间的过程中），就会出现此情况。  在处理不明确的时间时，可执行下列操作之一：  
  
-   如果该不明确的时间是用户输入的数据项，则可将这种多义性留给用户解决。  
  
-   就时间映射到 UTC 的方式进行假设。  例如，可以假定某个不明确的时间始终表示为时区的标准时间。  
  
 本主题介绍如何让用户解决不明确的时间。  
  
### 让用户解决不明确的时间  
  
1.  获取用户输入的日期和时间。  
  
2.  调用 <xref:System.TimeZoneInfo.IsAmbiguousTime%2A> 方法以确定时间是否明确。  
  
3.  如果时间不明确，请调用 <xref:System.TimeZoneInfo.GetAmbiguousTimeOffsets%2A> 方法以检索 <xref:System.TimeSpan> 对象的数组。  该数组中的每个元素都包含不明确的时间可以映射到的一个 UTC 偏移量。  
  
4.  让用户选择所需的偏移量。  
  
5.  通过从本地时间中减去用户选择的偏移量来得到 UTC 日期和时间。  
  
6.  调用 `static`（在 Visual Basic .NET 中为 `Shared`）<xref:System.DateTime.SpecifyKind%2A> 方法，将 UTC 日期和时间值的 <xref:System.DateTime.Kind%2A> 属性设置为 <xref:System.DateTimeKind?displayProperty=fullName>。  
  
## 示例  
 下面的示例提示用户输入一个日期和时间；如果输入的值不明确，则让用户选择不明确的时间映射到的 UTC 时间。  
  
 [!code-csharp[System.TimeZone2.Concepts#11](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#11)]
 [!code-vb[System.TimeZone2.Concepts#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#11)]  
  
 该代码示例的核心使用 <xref:System.TimeSpan> 对象的数组指示不明确时间的各个可能的 UTC 偏移量。  但是，这些偏移量对用户不可能有意义。  为了阐明偏移量的含义，该代码还通过注释说明了偏移量表示的是本地时区的标准时间还是其夏时制。  该代码通过将偏移量与 <xref:System.TimeZoneInfo.BaseUtcOffset%2A> 属性的值进行比较来确定哪个时间是标准时间，哪个时间是夏时制时间。  此属性指示 UTC 与时区标准时间之差。  
  
 在此示例中，本地时区都通过 <xref:System.TimeZoneInfo.Local%2A?displayProperty=fullName> 属性来引用，而从未分配给对象变量。  这是一种建议做法，因为调用 <xref:System.TimeZoneInfo.ClearCachedData%2A?displayProperty=fullName> 方法会使分配了本地时区的任何对象都失效。  
  
## 编译代码  
 此示例需要：  
  
-   在项目中添加一个对 System.Core.dll 的引用。  
  
-   使用 `using` 语句导入 <xref:System> 命名空间（在 C\# 代码中需要）。  
  
## 请参阅  
 [日期、时间和时区](../../../docs/standard/datetime/index.md)   
 [如何：解决不明确的时间](../../../docs/standard/datetime/resolve-ambiguous-times.md)