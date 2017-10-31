---
title: "如何：在 Visual Basic 中将字符串转换为字符数组 | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数组 [Visual Basic], 将字符串转换为"
  - "字符数组, 转换字符串"
  - "示例 [Visual Basic], 字符串转换"
  - "字符串转换 [Visual Basic], 数组"
  - "字符串 [Visual Basic], 转换为数组"
ms.assetid: 1b54b686-ab29-413b-adce-6bd5422376eb
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# 如何：在 Visual Basic 中将字符串转换为字符数组
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

有时，了解字符串中的字符以及这些字符在字符串中所处的位置会很有用，例如在需要分析字符串的时候。  此示例演示如何通过调用字符串的 <xref:System.String.ToCharArray%2A> 方法来获得字符串中字符的数组。  
  
## 示例  
 此示例演示如何将字符串拆分为 `Char` 数组，以及如何将字符串拆分为其 Unicode 文本字符的 `String` 数组。  进行这种区分的原因是：Unicode 文本字符可以由两个或更多个 `Char` 字符组成（例如，代理项对或组合字符序列）。  有关更多信息，请参见 <xref:System.Globalization.TextElementEnumerator> 以及位于 http:\/\/www.unicode.org 的“Unicode Standard”（Unicode 标准）。  
  
 [!code-vb[VbVbalrStrings#75](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-convert-a-string-to-an-array-of-characters_1.vb)]  
  
## 示例  
 将字符串拆分为它的 Unicode 文本字符会比较困难，但如果您需要与字符串的可视化表示形式有关的信息，这是必需的。  此示例使用 <xref:System.Globalization.StringInfo.SubstringByTextElements%2A> 方法获取组成字符串的 Unicode 文本字符的有关信息。  
  
 [!code-vb[VbVbalrStrings#76](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-convert-a-string-to-an-array-of-characters_2.vb)]  
  
## 请参阅  
 <xref:System.String.Chars%2A>   
 <xref:System.Globalization.StringInfo?displayProperty=fullName>   
 [如何：访问字符串中的字符](../../../../visual-basic/programming-guide/language-features/strings/how-to-access-characters-in-strings.md)   
 [Visual Basic 中字符串和其他数据类型间的转换](../../../../visual-basic/programming-guide/language-features/strings/converting-between-strings-and-other-data-types.md)   
 [字符串](../../../../visual-basic/programming-guide/language-features/strings/index.md)