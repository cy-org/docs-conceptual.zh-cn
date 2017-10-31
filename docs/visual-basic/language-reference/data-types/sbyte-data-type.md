---
title: "SByte 数据类型 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.sbyte"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数据类型 [Visual Basic], 整数"
  - "整数数字"
  - "整数, 数据类型"
  - "整数, 类型"
  - "整数数据类型"
  - "数字, integer"
  - "数字, 整个"
  - "SByte 数据类型"
  - "整数"
ms.assetid: 5c38374a-18a1-4cc2-b493-299e3dcaa60f
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# SByte 数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

保存 8 位（1 字节）有符号整数，值的范围为 \-128 到 127。  
  
## 备注  
 使用 `SByte` 数据类型来保存整数值，该整数值的长度无需为 `Integer` 数据长度的全长，甚至可以仅为 `Short` 数据长度的一半。  在某些情况下，公共语言运行时可以将 `SByte` 变量紧密地打包在一起，以节省内存消耗。  
  
 `SByte` 的默认值为 0。  
  
## 编程提示  
  
-   **CLS 遵从性。** `SByte` 数据类型不是 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\) 的一部分，因此如果一个组件使用该数据类型，则符合 CLS 的代码就不能使用该组件。  
  
-   **扩大。** `SByte` 数据类型可扩大为 `Short`、`Integer`、`Long`、`Decimal`、`Single` 和 `Double`。  这意味着您可以将 `SByte` 转换为这些类型中的任何一种，而不会遇到 <xref:System.OverflowException?displayProperty=fullName> 错误。  
  
-   **类型字符。** `SByte` 不包含文本类型字符或标识符类型字符。  
  
-   **Framework 类型。**.NET Framework 中的对应类型是 <xref:System.SByte?displayProperty=fullName> 结构。  
  
## 请参阅  
 <xref:System.SByte?displayProperty=fullName>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [Short 数据类型](../../../visual-basic/language-reference/data-types/short-data-type.md)   
 [Integer 数据类型](../../../visual-basic/language-reference/data-types/integer-data-type.md)   
 [Long 数据类型](../../../visual-basic/language-reference/data-types/long-data-type.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)