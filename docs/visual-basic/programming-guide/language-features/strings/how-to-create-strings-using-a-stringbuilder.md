---
title: "如何：在 Visual Basic 中使用 StringBuilder 创建字符串 | Microsoft Docs"
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
  - "StringBuilder 类"
  - "字符串 [Visual Basic], 使用 StringBuilder"
ms.assetid: 9c042880-aa16-432e-9ccb-cd00abda9ae3
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 如何：在 Visual Basic 中使用 StringBuilder 创建字符串
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

此示例使用 <xref:System.Text.StringBuilder> 类由许多较短的字符串构造一个长字符串。  对于串连许多字符串，<xref:System.Text.StringBuilder> 类比 `&=` 运算符效率更高。  
  
## 示例  
 下面的示例创建 <xref:System.Text.StringBuilder> 类的实例，将 1,000 个字符串追加到该实例，然后返回其字符串表示形式。  
  
 [!code-vb[VbVbalrStrings#70](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-to-create-strings-using-a-stringbuilder_1.vb)]  
  
## 请参阅  
 [使用 StringBuilder 类](../Topic/Using%20the%20StringBuilder%20Class%20in%20the%20.NET%20Framework.md)   
 [&\= 运算符](../../../../visual-basic/language-reference/operators/and-assignment-operator.md)   
 [字符串](../../../../visual-basic/programming-guide/language-features/strings/index.md)   
 [创建新字符串](../Topic/Creating%20New%20Strings%20in%20the%20.NET%20Framework.md)   
 [操作字符串](../Topic/Manipulating%20Strings%20in%20the%20.NET%20Framework.md)   
 [Strings Sample](http://msdn.microsoft.com/zh-cn/be9e82a3-dc95-4aaa-9396-61b66e467e02)