---
title: "如何：从 Char 值的数组创建字符串 (Visual Basic) | Microsoft Docs"
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
  - "示例 [Visual Basic], 数组"
  - "示例 [Visual Basic], Char 数据类型"
ms.assetid: 69f94e85-d57c-4ccc-a62a-426e829f5c5e
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 如何：从 Char 值的数组创建字符串 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

此示例从单独的字符创建字符串“abcd”。  
  
## 示例  
 [!code-vb[VbVbalrStrings#61](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-create-a-string-from-an-array-of-char-values_1.vb)]  
  
## 编译代码  
 此方法没有特殊要求。  
  
 语法 `"a"c` 中单个 `c` 跟随在带引号的单个字符后，用于创建一个字符文本。  
  
## 可靠编程  
 在使用该字符串时，该字符串中的空字符（等效于 `Chr(0)`）将导致意外的结果。  该字符串中包括空字符，但在某些情况下跟在空字符后的字符将不会显示。  
  
## 请参阅  
 <xref:System.String>   
 [Char 数据类型](../../../../visual-basic/language-reference/data-types/char-data-type.md)   
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)