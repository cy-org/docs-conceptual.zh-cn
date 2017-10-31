---
title: "如何：在日期和时间算法中使用时区 | Microsoft Docs"
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
  - "日期 [.NET Framework], 加和减"
  - "时区 [.NET Framework], 算术运算"
ms.assetid: 83dd898d-1338-415d-8cd6-445377ab7871
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：在日期和时间算法中使用时区
通常，在使用 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 值执行日期和时间的算术运算时，所得的结果并不能反映任何时区调整规则。  即使可以清楚地识别日期和时间值的时区（例如，当 <xref:System.DateTime.Kind%2A> 属性设置为 <xref:System.DateTimeKind> 时），情况也是如此。  本主题介绍如何对属于某一特定时区的日期和时间值执行算术运算。  这种算术运算的结果将反映时区的调整规则。  
  
### 对日期和时间算法应用调整规则  
  
1.  通过实现某种方法将日期和时间值与其所属的时区紧密耦合起来。  例如，声明一个同时包含日期和时间值及其时区的结构。  下面的示例使用此方法将 <xref:System.DateTime> 值与其时区关联起来。  
  
     [!code-csharp[System.DateTimeOffset.Conceptual#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual6.cs#6)]
     [!code-vb[System.DateTimeOffset.Conceptual#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual6.vb#6)]  
  
2.  通过调用 <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A> 方法或 <xref:System.TimeZoneInfo.ConvertTime%2A> 方法将时间转换为协调世界时 \(UTC\)。  
  
3.  对 UTC 时间执行算术运算。  
  
4.  通过调用 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTime%2CSystem.TimeZoneInfo%29?displayProperty=fullName> 方法将时间从 UTC 转换为与原始时间关联的时区。  
  
## 示例  
 下面的示例向中部标准时间 2008 年 3 月 9 日凌晨 1:30 添加了两小时三十分钟。  三十分钟后（即 2008 年 3 月 9 日凌晨 2:00）会发生夏时令的时区转换。  由于该示例遵从了上一节中列出的四个步骤，因此它将结果时间正确地报告为 2008 年 3 月 9 日凌晨 5:00。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual8.cs#8)]
 [!code-vb[System.DateTimeOffset.Conceptual#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual8.vb#8)]  
  
 <xref:System.DateTime> 和 <xref:System.DateTimeOffset> 值都会与它们可能所属的任何时区解除关联。  若要在执行日期和时间算术运算时自动应用时区调整规则，任何日期和时间值所属的时区都必须可以立即识别。  这意味着，任何日期和时间均必须和与之关联的时区紧密耦合在一起。  有多种方法可以实现此目的，其中包括：  
  
-   假定应用程序中使用的所有时间都属于某个特定的时区。  虽然此方法在某些情况下可行，但它的灵活性有限，可迁移性也可能不大。  
  
-   定义一种类型，并将日期和时间以及与之关联的时区作为两个字段包含在该类型中，从而将二者紧密地耦合在一起。  代码示例中使用的就是此方法，该示例定义了一个结构，并将日期和时间以及时区作为两个成员字段存储在该结构中。  
  
 该示例演示如何对 <xref:System.DateTime> 值执行算术运算，以便向结果应用时区调整规则。  但是，<xref:System.DateTimeOffset> 值有更简单的使用方法。  下面的示例演示如何改写原始示例中的代码，以使用 <xref:System.DateTimeOffset> 代替 <xref:System.DateTime> 值。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual6.cs#7)]
 [!code-vb[System.DateTimeOffset.Conceptual#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual6.vb#7)]  
  
 请注意，如果在未将 <xref:System.DateTimeOffset> 值转换为 UTC 的情况下便直接对其执行此加法运算，其结果将反映正确的时间点，但其偏移量将不会反映该时间的指定时区的偏移量。  
  
## 编译代码  
 此示例需要：  
  
-   在项目中添加一个对 System.Core.dll 的引用。  
  
-   使用 `using` 语句导入 <xref:System> 命名空间（在 C\# 代码中需要）。  
  
## 请参阅  
 [日期、时间和时区](../../../docs/standard/datetime/index.md)   
 [使用日期和时间执行算术运算](../../../docs/standard/datetime/performing-arithmetic-operations.md)