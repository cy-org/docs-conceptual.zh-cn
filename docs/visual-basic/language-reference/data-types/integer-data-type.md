---
title: "Integer 数据类型 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Integer"
  - "Integer"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "% 标识符类型字符"
  - "数据类型 [Visual Basic], 分配"
  - "数据类型 [Visual Basic], 整数"
  - "枚举值"
  - "I 文本类型字符"
  - "标识符类型字符串, %"
  - "Integer 数据类型"
  - "整数数字"
  - "整数, 数据类型"
  - "整数, 类型"
  - "整数数据类型"
  - "文本类型的字符, I"
  - "数字, integer"
  - "数字, 整个"
  - "整数"
ms.assetid: a8f233b4-4be3-455c-861b-05af2fbb6c60
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Integer 数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

保存 32 位（4 字节）带符号整数，值的范围为 \-2,147,483,648 到 2,147,483,647。  
  
## 备注  
 `Integer` 数据类型为 32 位处理器提供了优化性能。  其他整数类型在内存中的加载和存储的速度都要稍慢一些。  
  
 `Integer` 的默认值为 0。  
  
## 编程提示  
  
-   **互操作注意事项。**如果你与不是为 .NET Framework 编写的组件（如自动化或 COM 对象）交互，请记住，`Integer` 在其他环境中具有不同的数据宽度（16 位）。  如果将一个 16 位参数传递给此类组件，请在新的 Visual Basic 代码中将其声明为 `Short` 而不是 `Integer`。  
  
-   **Widening。** `Integer` 数据类型加宽到 `Long`、`Decimal`、`Single` 或 `Double`。  这意味着，你可以将 `Integer` 转换为这些类型中的任意类型，而不会遇到 <xref:System.OverflowException?displayProperty=fullName> 错误。  
  
-   **类型字符。**将文本类型字符 `I` 追加到文本会将其强制转换为 `Integer` 数据类型。  将标识符类型字符 `%` 追加到任何标识符会将其强制转换为 `Integer`。  
  
-   **Framework 类型。**.NET Framework 中的对应类型是 <xref:System.Int32?displayProperty=fullName> 结构。  
  
## 范围  
 如果尝试将整型变量设置为其类型范围以外的数字，则将出错。  如果尝试将其设置为小数，则数字将向上或向下舍入为最接近的整数值。  如果数字同样接近两个整数值，则值将舍入为最接近的偶数整数。  这种做法可将因单方向持续舍入中点值而导致的舍入误差降到最低。  下面的代码演示了舍入的示例。  
  
```  
' The valid range of an Integer variable is -2147483648 through +2147483647.  
Dim k As Integer  
' The following statement causes an error because the value is too large.  
k = 2147483648  
' The following statement sets k to 6.  
k = 5.9  
' The following statement sets k to 4  
k = 4.5  
' The following statement sets k to 6  
' Note, Visual Basic uses banker’s rounding (toward nearest even number)  
k = 5.5  
```  
  
## 请参阅  
 <xref:System.Int32?displayProperty=fullName>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Long 数据类型](../../../visual-basic/language-reference/data-types/long-data-type.md)   
 [Short 数据类型](../../../visual-basic/language-reference/data-types/short-data-type.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)