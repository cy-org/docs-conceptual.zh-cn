---
title: "UInteger 数据类型 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.uinteger"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数据类型 [Visual Basic], 整数"
  - "整数数字"
  - "整数, 数据类型"
  - "整数, 类型"
  - "整数数据类型"
  - "文本类型的字符, 用户界面"
  - "数字, integer"
  - "数字, 整个"
  - "UI 文本类型字符"
  - "UInteger 数据类型"
  - "整数"
ms.assetid: db7ddd34-4f23-46f5-84dd-8b0f83bb8729
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# UInteger 数据类型
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

保存排列按值从 0 到 4,294,967,295 的无符号 32 位 \(4 字节整数\)。  
  
## 备注  
 `UInteger` 提供的数据类型在最有效的数据宽度的最大的无符号值。  
  
 `UInteger` 的默认值为 0。  
  
## 编程提示  
 `UInteger` 和 `Integer` 数据类型在 32 位处理器提供最佳性能，，因为更小整数类型 \(`UShort`、 `Short`、 `Byte`和 `SByte`\)，因此，即使它们使用更少的位，占用更多时间加载，存储和获取。  
  
-   **负数。** 由于 `UInteger` 是无符号类型，它不能表示负数。  如果使用一元负 \(计算键入 `UInteger`表达式的`-`\) 运算符， Visual Basic 首先将表达式转换为 `Long` 。  
  
-   **CLS 遵从性。** `UInteger` 数据类型不是 \(cls\) 的 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) 一部分，因此，符合 CLS 的代码不能使用该组件。  
  
-   **互操作注意事项。** 如果您针对使用 .NET framework 编写的组件，例如自动或 COM 对象，请记住类型 \(如 `uint` 都可以有不同的数据宽度 \(16 位\) 在其他环境中。  如果将 16 位参数传递给此类元素，则将其声明为 `UShort` 而不是在托管 Visual Basic 代码的 `UInteger` 。  
  
-   **扩大到。** `UInteger` 数据类型扩大到 `Long`、 `ULong`、 `Decimal`、 `Single`和 `Double`。  这意味着您可以将 `UInteger` 为任何类型，而不会遇到 <xref:System.OverflowException?displayProperty=fullName> 错误。  
  
-   **键入字符。** 追加该文本类型与文本值的字符 `UI` 强制到 `UInteger` 数据类型。  `UInteger` 没有标识符类型字符。  
  
-   **结构类型。** 相应键入 .NET framework 是 <xref:System.UInt32?displayProperty=fullName> 结构。  
  
## 请参阅  
 <xref:System.UInt32>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [如何：调用采用无符号类型的 Windows 函数](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)