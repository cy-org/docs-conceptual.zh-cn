---
title: "Char 数据类型 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Char"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "C 文本类型字符"
  - "Char 数据类型"
  - "Char 数据类型, 字符文本"
  - "数据类型 [Visual Basic], 分配"
  - "文本类型的字符, C"
ms.assetid: cd7547a9-7855-4e8e-b216-35d74a362657
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Char 数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

保存无符号 16 位 \(2 字节\) 码位范围按从 0 到 65535 的值。  每个 *码位*，或者字符代码，表示单个 Unicode 字符。  
  
## 备注  
 ，您需要保存只有一个字符，且不需要开销 `String`时，请使用 `Char` 数据类型。  有时您可以使用 `Char()`，数组 `Char` 元素，该元素包含多个字符。  
  
 `Char` 的默认值与编码字符点 0。  
  
## Unicode 字符  
 码位的前 128 \(0\-127\) Unicode 对应于字母和符号在标准美国。  键盘。  码位的这些前 128 相同的与 ASCII 字符集定义。  码位的第二个 128 \(128\-255\) 表示特殊字符，比如基于拉丁语字母表的字母、重音、、货币符号和部分。  使用 Unicode 其余的代码对各种符号点 \(256\-65535\)，包括成功率文本字符、差异和数学和技术符号。  
  
 可以象使用 <xref:System.Char.IsDigit%2A> 和 <xref:System.Char.IsPunctuation%2A> 的方法。 `Char` 变量确定其 Unicode 类别。  
  
## 类型转换  
 Visual Basic 不直接转换在 `Char` 和 numeric 类型之间。  可以使用 <xref:Microsoft.VisualBasic.Strings.Asc%2A> 或转换表示其代码的 `Char` 值的 <xref:Microsoft.VisualBasic.Strings.AscW%2A> 函数为 `Integer` 点。  可以使用 <xref:Microsoft.VisualBasic.Strings.Chr%2A> 或 <xref:Microsoft.VisualBasic.Strings.ChrW%2A> 功能将具有的 `Integer` 值转换为 `Char` 码位。  
  
 如果类型检查开关 \([Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)\) 打开，必须追加该文本类型字符单字符字符串标识，而 `Char` 数据类型。  下面的示例阐释了这一点。  
  
```  
Option Strict On  
Dim charVar As Char  
' The following statement attempts to convert a String literal to Char.  
' Because Option Strict is On, it generates a compiler error.  
charVar = "Z"  
' The following statement succeeds because it specifies a Char literal.  
charVar = "Z"C  
```  
  
## 编程提示  
  
-   **负数。** `Char` 是无符号类型，不能表示负值。  在任一情况下，您不应使用 `Char` 表示数值。  
  
-   **互操作注意事项。** 如果您使用 .NET framework 编写的组件的接口，如自动或 COM 对象，记得字符类型具有不同的数据宽度 \(8 位\) 在其他环境。  如果将 8 位参数传递给此类元素，则将其声明为 `Byte` 而不是在新的 Visual Basic 代码的 `Char` 。  
  
-   **扩大到。** `Char` 数据类型扩大到 `String`。  这意味着您可以将 `Char` 为 `String` ，并且不会遇到 <xref:System.OverflowException?displayProperty=fullName> 错误。  
  
-   **键入字符。** 追加该文本类型对于单字符字符串的字符 `C` 强制到 `Char` 数据类型。  `Char` 没有标识符类型字符。  
  
-   **结构类型。** 相应键入 .NET framework 是 <xref:System.Char?displayProperty=fullName> 结构。  
  
## 请参阅  
 <xref:System.Char?displayProperty=fullName>   
 <xref:Microsoft.VisualBasic.Strings.Asc%2A>   
 <xref:Microsoft.VisualBasic.Strings.AscW%2A>   
 <xref:Microsoft.VisualBasic.Strings.Chr%2A>   
 <xref:Microsoft.VisualBasic.Strings.ChrW%2A>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [String 数据类型](../../../visual-basic/language-reference/data-types/string-data-type.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [如何：调用采用无符号类型的 Windows 函数](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)