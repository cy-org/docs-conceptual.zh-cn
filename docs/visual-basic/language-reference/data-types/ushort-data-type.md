---
title: "UShort 数据类型 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.ushort"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数据类型 [Visual Basic], 整数"
  - "整数数字"
  - "整数, 数据类型"
  - "整数, 类型"
  - "整数数据类型"
  - "文本类型的字符, US"
  - "数字, integer"
  - "数字, 整个"
  - "US 文本类型字符"
  - "UShort 数据类型"
  - "整数"
ms.assetid: 138db892-665d-4ba8-9cae-d8d91c4a8f39
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# UShort 数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

保存 16 位（双字节）无符号整数，取值范围为 0 到 65,535。  
  
## 备注  
 使用 `UShort` 数据类型包含对 `Byte` 来说太大的二进制数据。  
  
 `UShort` 的默认值为 0。  
  
## 编程提示  
  
-   **负数。**因为 `UShort` 是无符号类型，所以不能表示负数。  如果对计算结果为类型 `UShort` 的表达式使用一元负 \(`-`\) 运算符，则 Visual Basic 首先将该表达式转换为 `Integer`。  
  
-   **CLS 遵从性。** `UShort` 数据类型不是 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\) 的一部分，因此如果一个组件使用该数据类型，则符合 CLS 的代码就不能使用该组件。  
  
-   **扩大。** `UShort` 数据类型扩大为 `Integer`、`UInteger`、`Long`、`ULong`、`Decimal`、`Single` 和 `Double`。  这意味着您可以将 `UShort` 转换为这些类型中的任何一种，而不会遇到 <xref:System.OverflowException?displayProperty=fullName> 错误。  
  
-   **类型字符。**在文本后追加文本类型字符 `US` 会将其强制转换成 `UShort` 数据类型。  `UShort` 不具有标识符类型字符。  
  
-   **Framework 类型。**.NET Framework 中的对应类型是 <xref:System.UInt16?displayProperty=fullName> 结构。  
  
## 请参阅  
 <xref:System.UInt16>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [如何：调用采用无符号类型的 Windows 函数](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)