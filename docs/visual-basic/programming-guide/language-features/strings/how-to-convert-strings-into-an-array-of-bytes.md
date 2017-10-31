---
title: "如何：在 Visual Basic 中将字符串转换为字节数组 | Microsoft Docs"
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
  - "数组 [Visual Basic], 字节数组"
  - "数组 [Visual Basic], 将字符串转换为"
  - "字节数组"
  - "示例 [Visual Basic], 字符串转换"
  - "字符串转换, 数组"
ms.assetid: f477d35c-a3fc-4a30-b1d4-cd0d353aae1d
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 如何：在 Visual Basic 中将字符串转换为字节数组
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

本主题说明如何将字符串转换为字节数组。  
  
## 示例  
 本示例使用 <xref:System.Text.Encoding.Unicode%2A?displayProperty=fullName> 编码类的 <xref:System.Text.Encoding.GetBytes%2A> 方法将字符串转换为字节数组。  
  
 [!code-vb[VbVbalrStrings#74](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-convert-strings-into-an-array-of-bytes_1.vb)]  
  
 可以从几种编码选项中选择一种将字符串转换为字节数组：  
  
-   <xref:System.Text.Encoding.ASCII%2A?displayProperty=fullName>：获取 ASCII（7 位）字符集的编码。  
  
-   <xref:System.Text.Encoding.BigEndianUnicode%2A?displayProperty=fullName>：使用 Big\-Endian 字节顺序获取 UTF\-16 格式的编码。  
  
-   <xref:System.Text.Encoding.Default%2A?displayProperty=fullName>：获取系统当前 ANSI 代码页的编码。  
  
-   <xref:System.Text.Encoding.Unicode%2A?displayProperty=fullName>：使用 Little\-Endian 字节顺序获取 UTF\-16 格式的编码。  
  
-   <xref:System.Text.Encoding.UTF32%2A?displayProperty=fullName>：使用 Little\-Endian 字节顺序获取 UTF\-32 格式的编码。  
  
-   <xref:System.Text.Encoding.UTF7%2A?displayProperty=fullName>：获取 UTF\-7 格式的编码。  
  
-   <xref:System.Text.Encoding.UTF8%2A?displayProperty=fullName>：获取 UTF\-8 格式的编码。  
  
## 请参阅  
 <xref:System.Text.Encoding?displayProperty=fullName>   
 <xref:System.Text.Encoding.GetBytes%2A>   
 [如何：在 Visual Basic 中将字节数组转换为字符串](../../../../visual-basic/programming-guide/language-features/strings/how-to-convert-an-array-of-bytes-into-a-string.md)