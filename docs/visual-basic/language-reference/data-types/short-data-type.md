---
title: "Short 数据类型 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Short"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数据类型 [Visual Basic], 整数"
  - "整数数字"
  - "整数, 数据类型"
  - "整数, 类型"
  - "整数数据类型"
  - "文本类型的字符, S"
  - "数字, integer"
  - "数字, 整个"
  - "S 文本类型字符"
  - "Short 数据类型"
  - "整数"
ms.assetid: 65fcbcf3-a841-400e-885e-301497729a8b
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Short 数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

保存 16 位（2 字节）有符号整数，值的范围为 \-32,768 到 32,767。  
  
## 备注  
 使用 `Short` 数据类型以包含不需要 `Integer` 整个数据宽度的整型值。  在某些情况下，公共语言运行时可以将 `Short` 变量紧密地打包在一起，以节省内存消耗。  
  
 `Short` 的默认值为 0。  
  
## 编程提示  
  
-   **扩大。** `Short` 数据类型扩大为 `Integer`、`Long`、`Decimal`、`Single` 或 `Double`。  这意味着您可以将 `Short` 转换为这些类型中的任一类型，而不会遇到 <xref:System.OverflowException?displayProperty=fullName> 错误。  
  
-   **类型字符。**将文本类型字符 `S` 追加到文本会将其强制转换成 `Short` 数据类型。  `Short` 不具有标识符类型字符。  
  
-   **Framework 类型。**.NET Framework 中的对应类型是 <xref:System.Int16?displayProperty=fullName> 结构。  
  
## 请参阅  
 <xref:System.Int16?displayProperty=fullName>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [Integer 数据类型](../../../visual-basic/language-reference/data-types/integer-data-type.md)   
 [Long 数据类型](../../../visual-basic/language-reference/data-types/long-data-type.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)