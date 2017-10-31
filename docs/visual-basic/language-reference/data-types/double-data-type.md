---
title: "Double 数据类型 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Double"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "# 标识符类型字符"
  - "0 个字符, 尾随"
  - "数据类型 [Visual Basic], 分配"
  - "Double 数据类型"
  - "Double 数据类型 [Visual Basic]"
  - "双精度数字"
  - "浮点数字, Double 数据类型"
  - "标识符类型字符串, #"
  - "文本类型的字符, R"
  - "R 文本类型字符"
  - "实数"
  - "尾随 0 个字符"
  - "尾随零"
  - "零, 尾随"
ms.assetid: 0c5670f7-fcb1-453a-bef1-374730cd38fd
caps.latest.revision: 25
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 25
---
# Double 数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

存储带符号的 IEEE 64 位（8 个字节）双精度浮点数，负值取值范围为 \-1.79769313486231570E\+308 到 \-4.94065645841246544E\-324，正值取值范围为 4.94065645841246544E\-324 到 1.79769313486231570E\+308。  双精度数值存储实数数值的近似值。  
  
## 备注  
 `Double` 数据类型提供数字可能的最大和最小量值。  
  
 `Double` 的默认值为 0。  
  
## 编程提示  
  
-   **精度。**在处理浮点数字时，请记住浮点数在内存中并不总是有精确的表示形式。  对于某些操作（例如值比较和 `Mod` 运算符），这可能导致意外的结果。  有关更多信息，请参见 [数据类型疑难解答](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)。  
  
-   **尾随零。**浮点数据类型没有尾随零字符的任何内部表示形式。  例如，它们不能区别 4.2000 和 4.2。  因此，在显示或输出浮点值时，尾随零字符不会出现。  
  
-   **类型字符。**将文本类型字符 `R` 追加到文本会将其强制转换成 `Double` 数据类型。  例如，如果一个整数值后跟 `R`，则该值会更改为 `Double`。  
  
    ```  
    ' Visual Basic expands the 4 in the statement Dim dub As Double = 4R to 4.0:  
    Dim dub As Double = 4.0R  
    ```  
  
     将标识符类型字符 `#` 追加到任何标识符会将其强制转换成 `Double`。  在下面的示例中，变量 `num` 类型化为 `Double`。  
  
    ```  
    Dim num# = 3  
    ```  
  
-   **Framework 类型。**.NET Framework 中的对应类型是 <xref:System.Double?displayProperty=fullName> 结构。  
  
## 请参阅  
 <xref:System.Double?displayProperty=fullName>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Decimal 数据类型](../../../visual-basic/language-reference/data-types/decimal-data-type.md)   
 [Single 数据类型](../../../visual-basic/language-reference/data-types/single-data-type.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)   
 [数据类型疑难解答](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [类型字符](../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)