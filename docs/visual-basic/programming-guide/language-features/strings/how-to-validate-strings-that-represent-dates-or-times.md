---
title: "如何：验证表示日期或时间的字符串 (Visual Basic) | Microsoft Docs"
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
  - "String 数据类型, 验证"
  - "字符串 [Visual Basic], 验证"
ms.assetid: ae7d4b29-3436-4032-bdbf-4650eb1c8e19
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 如何：验证表示日期或时间的字符串 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

下面的代码示例设置一个 `Boolean` 值，该值指明字符串是否代表有效的日期或时间。  
  
## 示例  
 [!code-vb[VbVbcnRegEx#2](../../../../visual-basic/programming-guide/language-features/strings/codesnippet/VisualBasic/how-to-validate-strings-that-represent-dates-or-times_1.vb)]  
  
## 编译代码  
 将 `("01/01/03")` 和 `"9:30 PM"` 替换为想要验证的日期和时间。  可以将字符串替换为另一个硬编码的字符串、替换为 `String` 变量，或替换为返回字符串的方法（如 `InputBox`）。  
  
## 可靠编程  
 在尝试将 `String` 转换为 `DateTime` 变量时，请使用此方法来验证字符串。  通过首先检查日期或时间，您可以避免在运行时产生异常。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Information.IsDate%2A>   
 <xref:Microsoft.VisualBasic.Interaction.InputBox%2A>   
 [验证字符串 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/strings/validating-strings.md)