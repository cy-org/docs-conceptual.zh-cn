---
title: "如何：在字符串内搜索 (Visual Basic) | Microsoft Docs"
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
  - "示例 [Visual Basic], 字符串"
  - "字符串 [Visual Basic], 查找"
  - "字符串 [Visual Basic], 搜索"
ms.assetid: ae4c79e0-08ea-489f-bdb2-5eb6d355f284
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# 如何：在字符串内搜索 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

此示例调用 <xref:System.String> 对象的 <xref:System.String.IndexOf%2A> 方法报告子字符串的第一个匹配项的索引。  
  
## 示例  
 [!code-vb[VbVbalrStrings#71](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-search-within-a-string_1.vb)]  
  
## 编译代码  
 此示例需要:  
  
-   指定 <xref:System> 命名空间的 `Imports` 语句。  有关更多信息，请参见 [Imports 语句（.NET 命名空间和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)。  
  
## 可靠编程  
 <xref:System.String.IndexOf%2A> 方法报告子字符串的第一次出现的第一个字符的位置。  索引从 0 开始，这意味着字符串的第一个字符的索引为 0。  
  
 如果 <xref:System.String.IndexOf%2A> 没有找到该子字符串，则返回 \-1。  
  
 <xref:System.String.IndexOf%2A> 方法区分大小写并使用当前区域性。  
  
 为了优化错误控件，可以在 `Try` 中使用字符串搜索块 [Try...Catch...Finally 语句](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md) 结构。  
  
## 请参阅  
 <xref:System.String.IndexOf%2A>   
 [Try...Catch...Finally 语句](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [字符串介绍 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)   
 [字符串](../../../../visual-basic/programming-guide/language-features/strings/index.md)