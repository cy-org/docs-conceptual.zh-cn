---
title: "Single 数据类型 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Single"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "! 标识符类型字符"
  - "0 个字符, 尾随"
  - "数据类型 [Visual Basic], 分配"
  - "F 文本类型字符"
  - "浮点数字, Single 数据类型"
  - "标识符类型字符串, !"
  - "文本类型的字符, F"
  - "数字, 浮点"
  - "数字, 实数"
  - "实数"
  - "Single 数据类型"
  - "单精度数"
  - "尾随 0 个字符"
  - "尾随零"
  - "零, 尾随"
ms.assetid: 224a2795-4cd5-496c-8f7a-a4f05a06d45d
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Single 数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

存储有符号的 IEEE 32 位（4 个字节）单精度浮点数，负数取值范围为 \-3.4028235E\+38 到 \-1.401298E\-45，正数取值范围为 1.401298E\-45 到 3.4028235E\+38。  单精度数值存储实数数值的近似值。  
  
## 备注  
 使用 `Single` 数据类型包含不需要 `Double` 的完整数据宽度的浮点值。  在某些情况下，公共语言运行时可以将 `Single` 变量紧密地打包在一起，以节省内存消耗。  
  
 `Single` 的默认值为 0。  
  
## 编程提示  
  
-   **精度。**使用浮点数字时，请记住它们在内存中不一定有精确的表示形式。  对于某些操作（例如值比较和 `Mod` 运算符），这可能导致意外的结果。  有关更多信息，请参见 [数据类型疑难解答](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)。  
  
-   **扩大。** `Single` 数据类型扩大至 `Double`。  这意味着可以将 `Single` 转换为 `Double`，而不会出现 <xref:System.OverflowException?displayProperty=fullName> 错误。  
  
-   **尾随零。**浮点数据类型没有尾随 0 字符的任何内部表示形式。  例如，它们不能区别 4.2000 和 4.2。  因此，在显示或输出浮点值时，尾随 0 字符不会出现。  
  
-   **类型字符。**将文本类型字符 `F` 追加到文本会将其强制转换成 `Single` 数据类型。  将标识符类型字符 `!` 追加到任何标识符会将其强制转换成 `Single`。  
  
-   **Framework 类型。**.NET Framework 中的对应类型是 <xref:System.Single?displayProperty=fullName> 结构。  
  
## 请参阅  
 <xref:System.Single?displayProperty=fullName>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Decimal 数据类型](../../../visual-basic/language-reference/data-types/decimal-data-type.md)   
 [Double 数据类型](../../../visual-basic/language-reference/data-types/double-data-type.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)   
 [数据类型疑难解答](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)