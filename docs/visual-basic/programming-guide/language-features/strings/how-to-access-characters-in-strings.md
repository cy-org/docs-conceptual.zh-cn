---
title: "如何：在 Visual Basic 中访问字符串中的字符 | Microsoft Docs"
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
  - "字符 [Visual Basic], 在字符串中访问"
  - "字符串 [Visual Basic], 访问字符"
ms.assetid: 02c5206c-ffab-494d-b648-3b2ea358dc34
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 如何：在 Visual Basic 中访问字符串中的字符
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

此示例演示如何使用 <xref:System.String.Chars%2A> 属性访问位于字符串中指定位置的字符。  
  
## 示例  
 有时，了解字符串中的字符以及这些字符在字符串中的位置会很有用。  可将字符串视为字符（`Char` 实例）的数组；并可通过 <xref:System.String.Chars%2A> 属性引用字符的索引来检索特定字符。  
  
 [!code-vb[VbVbalrStrings#49](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-access-characters-in-strings_1.vb)]  
  
 <xref:System.String.Chars%2A> 属性的 `index` 参数是从零开始的。  
  
## 可靠编程  
 <xref:System.String.Chars%2A> 属性返回位于指定位置的字符。  但是，某些 Unicode 字符可由多个字符表示。  有关如何使用 Unicode 字符的更多信息，请参见 [如何：将字符串转换为字节数组](../../../../visual-basic/programming-guide/language-features/strings/how-to-convert-a-string-to-an-array-of-characters.md)。  
  
 如果 `index` 参数大于或等于该字符串的长度，或者小于零，则 <xref:System.String.Chars%2A> 属性会引发 <xref:System.IndexOutOfRangeException> 异常。  
  
## 请参阅  
 <xref:System.String.Chars%2A>   
 [如何：将字符串转换为字节数组](../../../../visual-basic/programming-guide/language-features/strings/how-to-convert-a-string-to-an-array-of-characters.md)   
 [Visual Basic 中字符串和其他数据类型间的转换](../../../../visual-basic/programming-guide/language-features/strings/converting-between-strings-and-other-data-types.md)   
 [字符串](../../../../visual-basic/programming-guide/language-features/strings/index.md)