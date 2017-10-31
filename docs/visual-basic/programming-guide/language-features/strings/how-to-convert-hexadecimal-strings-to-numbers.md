---
title: "如何：将十六进制字符串转换为数字 (Visual Basic) | Microsoft Docs"
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
  - "小数, 十六进制"
  - "示例 [Visual Basic], 字符串转换"
  - "十六进制, 小数"
  - "数字, 十六进制"
  - "字符串转换, 十六进制到数字"
ms.assetid: 76675807-eadb-4c08-bd50-e6c6ff4b8ced
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 如何：将十六进制字符串转换为数字 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

本示例使用 <xref:System.Convert.ToInt32%2A> 方法将十六进制字符串转换为整数。  
  
### 将十六进制字符串转换为数字  
  
-   使用 <xref:System.Convert.ToInt32%2A> 方法将以十六进制表达的数字转换为整数。  
  
     <xref:System.Convert.ToInt32%2A> 方法的第一个参数是要转换的字符串。  第二个参数描述了表示数字的基数，十六进制的基数为 16。  
  
     [!code-vb[VbVbalrStrings#62](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-convert-hexadecimal-strings-to-numbers_1.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Conversion.Hex%2A>   
 <xref:System.Convert.ToInt32%2A>