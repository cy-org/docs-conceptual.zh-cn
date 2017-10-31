---
title: "更改 .NET Framework 中的大小写 | Microsoft Docs"
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
  - "区分大小写"
  - "lowercase"
  - "字符串 [.NET Framework], 大小写"
  - "ToLower 方法"
  - "ToUpper 方法"
  - "大写"
ms.assetid: 6805f81b-e9ad-4387-9f4c-b9bdb21b87c0
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# 更改 .NET Framework 中的大小写
如果编写可接受用户输入的应用程序，永远无法确定用户以哪种大小写输入数据。  通常，你希望字符串统一采用大写或小写，尤其是在用户界面显示时。  下表介绍 3 种更改大小写的方法：  前两个方法提供可接受区域性的重载。  
  
|方法名称|使用|  
|----------|--------|  
|<xref:System.String.ToUpper%2A?displayProperty=fullName>|将字符串中的所有字符均转换为大写。|  
|<xref:System.String.ToLower%2A?displayProperty=fullName>|将字符串中的所有字符均转换为小写。|  
|<xref:System.Globalization.TextInfo.ToTitleCase%2A?displayProperty=fullName>|将字符串转换为首字母大写。|  
  
> [!WARNING]
>  请注意，为了对 <xref:System.String.ToUpper%2A?displayProperty=fullName> 和 <xref:System.String.ToLower%2A?displayProperty=fullName> 方法进行比较或测试它们是否相等，这两种方法不应用于转换字符串。  有关详细信息，请参阅[比较混合大小写的字符串](#Comparing)部分。  
  
<a name="Comparing"></a>   
## 比较混合大小写的字符串  
 若要比较混合大小写的字符串以确定它们的顺序，请调用具有 <xref:System.String.CompareTo%2A?displayProperty=fullName> 方法中具有 `comparisonType` 参数的其中一个重载，并向 `comparisonType` 参数提供 <xref:System.StringComparison?displayProperty=fullName>、<xref:System.StringComparison?displayProperty=fullName> 或 <xref:System.StringComparison?displayProperty=fullName> 的值。  对于使用特定区域性（而非当前区域性）的比较，请调用 <xref:System.String.CompareTo%2A?displayProperty=fullName> 方法中具有 `culture` 和 `options` 参数的重载，并提供 <xref:System.Globalization.CompareOptions?displayProperty=fullName> 的值作为 `options` 参数。  
  
 若要比较混合大小写的字符串以确定它们是否相等，请调用 <xref:System.String.Equals%2A?displayProperty=fullName> 方法中具有 `comparisonType` 参数的其中一个重载，并向 `comparisonType` 参数提供 <xref:System.StringComparison?displayProperty=fullName>、<xref:System.StringComparison?displayProperty=fullName> 或 <xref:System.StringComparison?displayProperty=fullName> 的值。  
  
 有关详细信息，请参阅[针对使用字符串的最佳做法](../../../docs/standard/base-types/best-practices-strings.md)。  
  
## ToUpper  
 <xref:System.String.ToUpper%2A?displayProperty=fullName> 方法将字符串中的所有字符均更改为大写。  以下示例将字符串“Hello World\!”从混合大小写转换为大写。  
  
 [!code-csharp[Strings.ChangingCase#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.ChangingCase/cs/Example.cs#1)]
 [!code-vb[Strings.ChangingCase#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.ChangingCase/vb/Example.vb#1)]  
  
 默认情况下，上述示例区分区域性；它应用当前区域性的大小写约定。  若要执行不区分区域性的大小写更改或应用特定区域性的大小写约定，请使用 <xref:System.String.ToUpper%28System.Globalization.CultureInfo%29?displayProperty=fullName> 方法重载并提供 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> 的值或 <xref:System.Globalization.CultureInfo?displayProperty=fullName> 对象（表示 *culture* 参数的指定区域性）。  有关演示如何使用 <xref:System.String.ToUpper%2A> 方法执行不区分区域性的大小写更改的示例，请参阅[执行不区分区域性的大小写更改](../../../ocs/standard/globalization-localization/performing-culture-insensitive-case-changes.md)。  
  
## ToLower  
 <xref:System.String.ToLower%2A?displayProperty=fullName> 方法与上述方法类似，但改为将字符串中的所有字符均转换为小写。  以下示例将字符串“Hello World\!”转换为小写。  
  
 [!code-csharp[Strings.ChangingCase#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Strings.ChangingCase/cs/Example.cs#2)]
 [!code-vb[Strings.ChangingCase#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Strings.ChangingCase/vb/Example.vb#2)]  
  
 默认情况下，上述示例区分区域性；它应用当前区域性的大小写约定。  若要执行不区分区域性的大小写更改或应用特定区域性的大小写约定，请使用 <xref:System.String.ToLower%28System.Globalization.CultureInfo%29?displayProperty=fullName> 方法重载并提供 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> 的值或 <xref:System.Globalization.CultureInfo?displayProperty=fullName> 对象（表示 *culture* 参数的指定区域性）。  有关演示如何使用 <xref:System.String.ToLower%28System.Globalization.CultureInfo%29> 方法执行不区分区域性的大小写更改的示例，请参阅[执行不区分区域性的大小写更改](../../../ocs/standard/globalization-localization/performing-culture-insensitive-case-changes.md)。  
  
## ToTitleCase  
 <xref:System.Globalization.TextInfo.ToTitleCase%2A?displayProperty=fullName> 将每个单词的第一个字符转换为大写并将其余字符转换为小写。  但是，全部大写的单词被假定为缩写词且不会转换。  
  
 <xref:System.Globalization.TextInfo.ToTitleCase%2A?displayProperty=fullName> 方法区分区域性；即是，它使用特定区域性的大小写约定。  为了调用方法，首先要从特定区域性的 <xref:System.Globalization.CultureInfo.TextInfo%2A?displayProperty=fullName> 属性中检索表示特定区域性的大小写约定的 <xref:System.Globalization.TextInfo> 对象。  
  
 下面的示例将数组中的每个字符串传递至 <xref:System.Globalization.TextInfo.ToTitleCase%2A?displayProperty=fullName> 方法。  字符串包含适当的标题字符串以及首字母缩写词。  通过使用英语（美国）区域性的大小写约定将字符串转换为首字母大写。  
  
 [!code-csharp[System.Globalization.TextInfo.ToTitleCase#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.globalization.textinfo.totitlecase/cs/totitlecase2.cs#1)]
 [!code-vb[System.Globalization.TextInfo.ToTitleCase#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.globalization.textinfo.totitlecase/vb/totitlecase2.vb#1)]  
  
 请注意，<xref:System.Globalization.TextInfo.ToTitleCase%2A?displayProperty=fullName> 方法虽然区分区域性，但不提供语言方面的正确大小写规则。  例如，在上述示例中，方法将“a tale of two cities”转换为“A Tale Of Two Cities”。  但是，对于 en\-US 区域性，语言方面的正确首字母大小写应为“A Tale of Two Cities”。  
  
## 请参阅  
 [基本字符串操作](../../../docs/standard/base-types/basic-string-operations.md)   
 [执行不区分区域性的字符串操作](../../../ocs/standard/globalization-localization/performing-culture-insensitive-string-operations.md)