---
title: "在 .NET Framework 中从字符串剪裁和移除字符 | Microsoft Docs"
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
  - "Remove 方法"
  - "移除字符"
  - "字符串 [.NET Framework], 移除字符"
  - "Trim 方法"
  - "TrimEnd 方法"
  - "剪裁字符"
  - "TrimStart 方法"
ms.assetid: ab248dab-70d4-4413-81c6-542d153fd195
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# 在 .NET Framework 中从字符串剪裁和移除字符
如果将一个句子分析成单个的单词，则最后的结果可能是单词的一端或另一端带有空格（也称为空白）。  在这种情形下，可以使用 **System.String** 类中的剪裁方法之一来从字符串中的指定位置移除任何数量的空格或其他字符。  下表描述了可用的剪裁方法。  
  
|方法名|用途|  
|---------|--------|  
|<xref:System.String.Trim%2A?displayProperty=fullName>|从字符串的开头和结尾移除空白的或者指定的字符|  
|<xref:System.String.TrimEnd%2A?displayProperty=fullName>|从字符串的结尾处移除在字符数组中指定的字符。|  
|<xref:System.String.TrimStart%2A?displayProperty=fullName>|从字符串的开头移除在字符数组中指定的字符。|  
|<xref:System.String.Remove%2A?displayProperty=fullName>|从字符串中的指定索引位置移除指定数量的字符。|  
  
## Trim  
 使用<xref:System.String.Trim%2A?displayProperty=fullName>方法可以很方便地从字符串的两端移除空白，如下面的示例所示。  
  
 [!code-cpp[Conceptual.String.BasicOps#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#17)]
 [!code-csharp[Conceptual.String.BasicOps#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#17)]
 [!code-vb[Conceptual.String.BasicOps#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#17)]  
  
 还可以从字符串的开始和结尾移除指定的字符  下面的示例移除空白字符、句号和星号。  
  
 [!code-csharp[Conceptual.String.BasicOps#22](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trim2.cs#22)]
 [!code-vb[Conceptual.String.BasicOps#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trim2.vb#22)]  
  
## TrimEnd  
 **String.TrimEnd** 方法从字符串的结尾移除字符，同时创建新的字符串对象。  通过为此方法传递一个字符数组来指定要移除的字符。  字符数组中的元素顺序并不影响剪裁操作。  当找到未在数组中指定的字符时，剪裁停止。  
  
 下面的示例使用 **TrimEnd** 方法移除字符串最后面的字母。  在此示例中，`'r'` 字符和 `'W'` 字符的位置反转，以阐释数组中字符的顺序并不重要。  请注意，此代码移除 `MyString` 的最后一个单词和第一个单词的一部分。  
  
 [!code-cpp[Conceptual.String.BasicOps#18](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#18)]
 [!code-csharp[Conceptual.String.BasicOps#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#18)]
 [!code-vb[Conceptual.String.BasicOps#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#18)]  
  
 此代码将 `He` 显示到控制台。  
  
 下面的示例使用 **TrimEnd** 方法移除字符串的最后一个单词。  在此代码中，单词 `Hello` 后尾随一个逗号，而由于在要剪除的字符的数组中没有指定逗号，因此剪裁在逗号处结束。  
  
 [!code-cpp[Conceptual.String.BasicOps#19](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#19)]
 [!code-csharp[Conceptual.String.BasicOps#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#19)]
 [!code-vb[Conceptual.String.BasicOps#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#19)]  
  
 此代码将 `Hello,` 显示到控制台。  
  
## TrimStart  
 **String.TrimStart** 方法类似于 **String.TrimEnd** 方法，不同之处在于它通过从现有字符串对象的开头移除字符来创建新的字符串。  通过向 **TrimStart** 方法传递一个字符数组来指定要移除的字符。  使用 **TrimEnd** 方法时，字符数组中元素的顺序并不影响剪裁操作。  当找到未在数组中指定的字符时，剪裁停止。  
  
 下面的示例移除字符串的第一个单词。  在此示例中，颠倒了 `'l'` 字符和 `'H'` 字符的位置，以指明字符在数组中的顺序并不重要。  
  
 [!code-cpp[Conceptual.String.BasicOps#20](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#20)]
 [!code-csharp[Conceptual.String.BasicOps#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#20)]
 [!code-vb[Conceptual.String.BasicOps#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#20)]  
  
 此代码将 `World!` 显示到控制台。  
  
## 移除  
 <xref:System.String.Remove%2A?displayProperty=fullName>方法，从现有字符串的指定位置开始，移除指定数量的字符。  此方法采用从零开始的索引。  
  
 下面的示例从字符串的从零开始的索引的第五个位置开始，从该字符串中移除十个字符。  
  
 [!code-cpp[Conceptual.String.BasicOps#21](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.string.basicops/cpp/trimming.cpp#21)]
 [!code-csharp[Conceptual.String.BasicOps#21](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/trimming.cs#21)]
 [!code-vb[Conceptual.String.BasicOps#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/trimming.vb#21)]  
  
 可以使用 <xref:System.String.Replace%28System.String%2CSystem.String%29?displayProperty=fullName>方法从字符串中移除指定字符或子字符串。也可以用\(<xref:System.String.Empty?displayProperty=fullName>\)代替。  下面的示例从字符串中移除所有逗号。  
  
 [!code-csharp[Conceptual.String.BasicOps#23](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/replace1.cs#23)]
 [!code-vb[Conceptual.String.BasicOps#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/replace1.vb#23)]  
  
## 请参阅  
 [基本字符串操作](../../../docs/standard/base-types/basic-string-operations.md)