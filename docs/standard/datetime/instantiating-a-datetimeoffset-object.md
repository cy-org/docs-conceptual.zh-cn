---
title: "实例化 DateTimeOffset 对象 | Microsoft Docs"
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
  - "实例化时区对象"
  - "时区对象 [.NET Framework]，实例化"
  - "DateTimeOffset 结构，转换为 DateTime"
  - "DateTimeOffset 结构，实例化"
ms.assetid: 9648375f-d368-4373-a976-3332ece00c0a
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# 实例化 DateTimeOffset 对象
<xref:System.DateTimeOffset> 结构提供了多种创建新的 <xref:System.DateTimeOffset> 值的方法。  其中的许多方法都直接与可用于实例化新的 <xref:System.DateTime> 值的方法相对应，只是增加了增强功能，允许您指定日期和时间值相对于协调世界时 \(UTC\) 的偏移量。  具体而言，您可以使用下列方式实例化 <xref:System.DateTimeOffset> 值：  
  
-   使用日期和时间文本。  
  
-   调用 <xref:System.DateTimeOffset> 构造函数。  
  
-   将某个值隐式转换为 <xref:System.DateTimeOffset> 值。  
  
-   分析日期和时间的字符串表示形式。  
  
 本主题提供更详细的信息和代码示例来阐释这些实例化新的 <xref:System.DateTimeOffset> 值的方法。  
  
## 日期和时间文本  
 对于支持这项功能的语言，最常用的实例化 <xref:System.DateTime> 值的方法之一就是将日期和时间作为硬编码的文本值来提供。  例如，下面的 Visual Basic 代码创建一个 <xref:System.DateTime> 对象，其值是 2008 年 1 月 1 日上午 10:00。  
  
 [!code-vb[System.DateTimeOffset.Conceptual.Instantiate#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#1)]  
  
 如果使用支持 <xref:System.DateTime> 文本的语言，则还可以使用日期和时间文本初始化 <xref:System.DateTimeOffset> 值。  例如，下面的 Visual Basic 代码创建一个 <xref:System.DateTimeOffset> 对象。  
  
 [!code-vb[System.DateTimeOffset.Conceptual.Instantiate#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#2)]  
  
 如控制台输出所示，使用这种方式创建的 <xref:System.DateTimeOffset> 值被分配了本地时区的偏移量。  这意味着，如果在不同的计算机上运行该代码，那么使用字符文本分配的 <xref:System.DateTimeOffset> 值并不标识单个时间点。  
  
## DateTimeOffset 构造函数  
 <xref:System.DateTimeOffset> 类型定义了六个构造函数。  其中有四个直接对应于 <xref:System.DateTime> 构造函数，只是增加了一个 <xref:System.TimeSpan> 类型的参数，该参数定义相对于 UTC 的日期和时间偏移量。  这些允许您根据单独的日期和时间组成部分的值来定义 <xref:System.DateTimeOffset> 值。  例如，下面的代码通过这四个构造函数用相同的值 \(7\/1\/2008 12:05 AM \+01:00\) 实例化 <xref:System.DateTimeOffset> 对象。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#3)]
 [!code-vb[System.DateTimeOffset.Conceptual.Instantiate#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#3)]  
  
 请注意，如果使用 <xref:System.Globalization.PersianCalendar> 对象作为其构造函数的其中一个参数实例化的 <xref:System.DateTimeOffset> 对象的值显示到控制台上，它将被表示为公历日期，而非波斯历日期。  若要使用波斯历输出日期，请参见 <xref:System.Globalization.PersianCalendar> 主题中的示例。  
  
 另外两个构造函数根据 <xref:System.DateTime> 值创建一个 <xref:System.DateTimeOffset> 对象。  其中第一个构造函数有一个参数，即要转换为 <xref:System.DateTimeOffset> 值的 <xref:System.DateTime> 值。  得到的 <xref:System.DateTimeOffset> 值的偏移量取决于该构造函数的单个参数的 <xref:System.DateTime.Kind%2A> 属性。  如果它的值是 <xref:System.DateTimeKind?displayProperty=fullName>，偏移量将被设置为等于 <xref:System.TimeSpan.Zero?displayProperty=fullName>。  否则，其偏移量将被设置为等于本地时区的偏移量。  下面的示例阐释如何使用此构造函数实例化表示 UTC 和本地时区的 <xref:System.DateTimeOffset> 对象：  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#4)]
 [!code-vb[System.DateTimeOffset.Conceptual.Instantiate#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#4)]  
  
> [!NOTE]
>  调用带有一个 <xref:System.DateTime> 参数的 <xref:System.DateTimeOffset> 构造函数重载与将 <xref:System.DateTime> 值隐式转换为 <xref:System.DateTimeOffset> 值是等效的。  
  
 根据 <xref:System.DateTime> 值创建一个 <xref:System.DateTimeOffset> 对象的第二个构造函数有两个参数：要转换的 <xref:System.DateTime> 值，以及表示日期和时间相对于 UTC 的偏移量的 <xref:System.TimeSpan> 值。  此偏移量值必须与该构造函数的第一个参数的 <xref:System.DateTime.Kind%2A> 属性相对应，否则将引发 <xref:System.ArgumentException>。  如果第一个参数的 <xref:System.DateTime.Kind%2A> 属性是 <xref:System.DateTimeKind?displayProperty=fullName>，则第二个参数的值必须是 <xref:System.TimeSpan.Zero?displayProperty=fullName>。  如果第一个参数的 <xref:System.DateTime.Kind%2A> 属性是 <xref:System.DateTimeKind?displayProperty=fullName>，则第二个参数的值必须是本地系统所在时区的偏移量。  如果第一个参数的 <xref:System.DateTime.Kind%2A> 属性是 <xref:System.DateTimeKind?displayProperty=fullName>，那么偏移量可以是任意有效值。  下面的代码阐释调用此构造函数将 <xref:System.DateTime> 转换为 <xref:System.DateTimeOffset> 值。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#5)]
 [!code-vb[System.DateTimeOffset.Conceptual.Instantiate#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#5)]  
  
## 隐式类型转换  
 <xref:System.DateTimeOffset> 类型支持一种隐式类型转换：即从 <xref:System.DateTime> 值到 <xref:System.DateTimeOffset> 值的转换。（隐式类型转换是从一种类型到另一种类型的转换，它不需要显式强制转换（在 C\# 中）或转换（在 Visual Basic 中），并且不会丢失信息。  它使得类似于以下内容的代码可以实现。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#6)]
 [!code-vb[System.DateTimeOffset.Conceptual.Instantiate#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#6)]  
  
 得到的 <xref:System.DateTimeOffset> 值的偏移量取决于 <xref:System.DateTime.Kind%2A?displayProperty=fullName> 属性值。  如果它的值是 <xref:System.DateTimeKind?displayProperty=fullName>，偏移量将被设置为等于 <xref:System.TimeSpan.Zero?displayProperty=fullName>。  如果它的值是 <xref:System.DateTimeKind?displayProperty=fullName> 或 <xref:System.DateTimeKind?displayProperty=fullName>，偏移量将被设置为等于本地时区的偏移量。  
  
## 分析日期和时间的字符串表示形式  
 <xref:System.DateTimeOffset> 类型支持四种方法，使您能够将日期和时间的字符串表示形式转换为 <xref:System.DateTimeOffset> 值：  
  
-   <xref:System.DateTimeOffset.Parse%2A>，它尝试将日期和时间的字符串表示形式转换为 <xref:System.DateTimeOffset> 值，如果转换失败则引发异常。  
  
-   <xref:System.DateTimeOffset.TryParse%2A>，它尝试将日期和时间的字符串表示形式转换为 <xref:System.DateTimeOffset> 值，如果转换失败则返回 `false`。  
  
-   <xref:System.DateTimeOffset.ParseExact%2A>，它尝试将指定格式的日期和时间的字符串表示形式转换为 <xref:System.DateTimeOffset> 值。  如果转换失败，该方法将引发异常。  
  
-   <xref:System.DateTimeOffset.TryParseExact%2A>，它尝试将指定格式的日期和时间的字符串表示形式转换为 <xref:System.DateTimeOffset> 值。  如果转换失败，该方法将返回 `false`。  
  
 下面的示例阐释分别调用这四个字符串转换方法中的每一个来实例化 <xref:System.DateTimeOffset> 值。  
  
 [!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#7)]
 [!code-vb[System.DateTimeOffset.Conceptual.Instantiate#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#7)]  
  
## 请参阅  
 [日期、时间和时区](../../../docs/standard/datetime/index.md)