---
title: "ULong 数据类型 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.ulong"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数据类型 [Visual Basic], 整数"
  - "整数数字"
  - "整数, 数据类型"
  - "整数, 类型"
  - "整数数据类型"
  - "文本类型的字符, UL"
  - "数字, integer"
  - "数字, 整个"
  - "UL 文本类型字符"
  - "Ulong 数据类型"
  - "整数"
ms.assetid: 017e0702-774e-44ae-bedc-786b424ca84e
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# ULong 数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

存储从 0 到 18,446,744,073,709,551,615（超过 10 ^ 19 的 1.84 倍）之间的 64 位（8 字节）无符号整数。  
  
## 备注  
 使用 `ULong` 数据类型来包含对于 `UInteger` 而言太大的二进制数据，或包含可能的最大无符号整数值。  
  
 `ULong` 的默认值为 0。  
  
## 编程提示  
  
-   **负数。**因为 `ULong` 是无符号类型，所以不能表示负数。  如果对计算结果为类型 `ULong` 的表达式使用一元负 \(`-`\) 运算符，则 Visual Basic 首先将该表达式转换为 `Decimal`。  
  
-   **CLS 遵从性。** `ULong` 数据类型不是 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\) 的一部分，因此如果一个组件使用该数据类型，则符合 CLS 的代码就不能使用该组件。  
  
-   **互操作注意事项。**如果正在与不是为 .NET Framework 而编写的组件（例如自动化或 COM 对象）互操作，请记住在其他环境中 `ulong` 等类型可以有不同的数据宽度（32 位）。  若将一个 32 位参数传递给这样的组件，在托管的 Visual Basic 代码中应将其声明为 `UInteger` 而不是 `ULong`。  
  
     此外，自动化在 Windows 95、Windows 98、Windows ME 或 Windows 2000 上不支持 64 位整数。  不能将 Visual Basic `ULong` 参数传递给这些平台上的自动化组件。  
  
-   **扩大。** `ULong` 数据类型扩大为 `Decimal`、`Single` 和 `Double`。  这意味着您可以将 `ULong` 转换为这些类型中的任何一种，而不会遇到 <xref:System.OverflowException?displayProperty=fullName> 错误。  
  
-   **类型字符。**在文本后追加文本类型字符 `UL` 会将其强制转换成 `ULong` 数据类型。  `ULong` 不具有标识符类型字符。  
  
-   **Framework 类型。**.NET Framework 中的对应类型是 <xref:System.UInt64?displayProperty=fullName> 结构。  
  
## 请参阅  
 <xref:System.UInt64>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [如何：调用采用无符号类型的 Windows 函数](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)