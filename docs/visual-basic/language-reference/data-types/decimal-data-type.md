---
title: "Decimal 数据类型 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Decimal"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "@ 标识符类型字符"
  - "0 个字符, 尾随"
  - "D 文本类型字符"
  - "数据类型 [Visual Basic], 分配"
  - "Decimal 数据类型"
  - "decimal 关键字"
  - "小数, Decimal 数据类型"
  - "标识符类型字符串, @"
  - "文本类型的字符, D"
  - "数字, 实数"
  - "实数"
  - "尾随 0 个字符"
  - "尾随零"
  - "可变精度数字"
  - "零, 尾随"
ms.assetid: 1d855b45-afe2-45b0-a623-96b6f63a43d5
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# Decimal 数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

存储 128 位（16 字节）的有符号值，它表示按 10 的可变幂进行缩放的 96 位（12 字节）整数。  缩放系数指定小数点右侧的数字数；范围为 0 到 28。  使用范围 0（无小数位），最大的可能值为 \+\/\-79,228,162,514,264,337,593,543,950,335 \(\+\/\-7.9228162514264337593543950335E\+28\)。  如果小数位数为 28，则最大值为 \+\/\-7.9228162514264337593543950335，且最小非零值为 \+\/\-0.0000000000000000000000000001 \(\+\/\-1E\-28\)。  
  
## 备注  
 `Decimal` 数据类型提供数字的最大数量的有效数位。  它最多支持 29 个有效数位，并可以表示超过 7.9228 x 10^28 的值。  它特别适用于需要使用大量数位但不能容忍舍入误差的计算，如金融方面的计算。  
  
 `Decimal` 的默认值为 0。  
  
## 编程提示  
  
-   **精度。** `Decimal` 不是浮点数据类型。  `Decimal` 结构存储二进制整数值，以及符号位和指定值中的哪部分为纯小数的整数比例因子。  因此，`Decimal` 数字在内存中的表示形式比浮点型（`Single` 和 `Double`）更精确。  
  
-   **性能。** `Decimal` 数据类型是所有 Numeric 类型中最慢的一种类型。  在选择数据类型之前，应权衡精度和性能之间的重要性。  
  
-   **扩大。** `Decimal` 数据类型扩大至 `Single` 或 `Double`。  这意味着您可以将 `Decimal` 转换为这些类型中的任何类型，而不会遇到 <xref:System.OverflowException?displayProperty=fullName> 错误。  
  
-   **尾随零。**Visual Basic 不会将尾随零存储在 `Decimal` 文本中。  但是，`Decimal` 变量将保留通过计算获得的任何尾随零。  下面的示例阐释了这一点。  
  
    ```  
    Dim d1, d2, d3, d4 As Decimal  
    d1 = 2.375D  
    d2 = 1.625D  
    d3 = d1 + d2  
    d4 = 4.000D  
    MsgBox("d1 = " & CStr(d1) & ", d2 = " & CStr(d2) &  
          ", d3 = " & CStr(d3) & ", d4 = " & CStr(d4))  
    ```  
  
     前面的示例中的 `MsgBox` 的输出如下所示：  
  
     d1 \= 2.375，d2 \= 1.625，d3 \= 4.000，d4 \= 4  
  
-   **类型字符。**将文本类型字符 `D` 追加到文本会将其强制转换成 `Decimal` 数据类型。  将标识符类型字符 `@` 追加到任何标识符会将其强制转换成 `Decimal`。  
  
-   **Framework 类型。**.NET Framework 中的对应类型是 <xref:System.Decimal?displayProperty=fullName> 结构。  
  
## 范围  
 可能需要使用 `D` 类型字符将较大的值分配到 `Decimal` 变量或常数。  此要求是，因为编译器解释一个文本作为 `Long`，除非一个文本类型字符之后，如下例所示。  
  
```  
Dim bigDec1 As Decimal = 9223372036854775807   ' No overflow.  
Dim bigDec2 As Decimal = 9223372036854775808   ' Overflow.  
Dim bigDec3 As Decimal = 9223372036854775808D  ' No overflow.  
```  
  
 `bigDec1` 的声明不会导致溢出，因为分配给它的值属于 `Long`的大小。  `Long` 值可以分配给 `Decimal` 变量。  
  
 `bigDec2` 的声明会产生一个溢出检查，因为分配给它的值。`Long`太大。  由于该数字字符串不会先被解释为 `Long`，它不能分配给 `Decimal` 变量。  
  
 为 `bigDec3`，文本类型字符 `D` 通过强制编译器解释该文本解决该问题作为 `Decimal` 而不是 `Long`。  
  
## 请参阅  
 <xref:System.Decimal?displayProperty=fullName>   
 <xref:System.Decimal.%23ctor%2A?displayProperty=fullName>   
 <xref:System.Math.Round%2A?displayProperty=fullName>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Single 数据类型](../../../visual-basic/language-reference/data-types/single-data-type.md)   
 [Double 数据类型](../../../visual-basic/language-reference/data-types/double-data-type.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)