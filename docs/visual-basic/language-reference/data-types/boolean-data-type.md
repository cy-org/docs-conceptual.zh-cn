---
title: "Boolean 数据类型 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.FALSE"
  - "vb.TRUE"
  - "vb.Boolean"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Boolean 数据类型"
  - "布尔值, False 关键字"
  - "布尔值, True 关键字"
  - "False 关键字 [Visual Basic]"
  - "True 关键字 [Visual Basic]"
ms.assetid: 4858e630-4813-4216-a55e-f4d0feb884e4
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Boolean 数据类型 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

存放只可能为 `True` 或 `False` 的值。  关键字 `True` 和 `False` 对应于 `Boolean` 变量的两种状态。  
  
## 备注  
 使用 [Boolean Data Type \(Visual Basic\)](../../../visual-basic/language-reference/data-types/boolean-data-type.md) 以包含双状态值（例如 true\/false、yes\/no 或 on\/off）。  
  
 `Boolean` 的默认值为 `False`。  
  
 `Boolean` 值不作为数字进行存储，存储的值也不用来与数字等效。  绝不应编写依赖于 `True` 和 `False` 的等效数值的代码。  只要有可能，就应当按照 `Boolean` 变量的设计意图，限制将其用于逻辑值。  
  
## 类型转换  
 当 Visual Basic 将数字数据类型值转换为 `Boolean` 时，0 变为 `False`，所有其他值变为 `True`。  当 Visual Basic 将 `Boolean` 值转换为数字类型时，`False` 变为 0，`True` 变为 \-1。  
  
 当在 `Boolean` 值和数字数据类型之间转换时，请注意，.NET Framework 转换方法不会总是产生与 Visual Basic 转换关键字相同的结果。  这是因为 Visual Basic 转换会保留与先前版本兼容的行为。  有关更多信息，请参见 [数据类型疑难解答](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md) 中的“Boolean 类型无法精确转换为 Numeric 类型”。  
  
## 编程提示  
  
-   **负数。** `Boolean` 不是数字类型，无法表示负值。  在任何情况下都不应使用 `Boolean` 存放数值。  
  
-   **类型字符。** `Boolean` 不包含文本类型字符或标识符类型字符。  
  
-   **Framework 类型。**.NET Framework 中的对应类型是 <xref:System.Boolean?displayProperty=fullName> 结构。  
  
## 示例  
 在下面的示例中，`runningVB` 是一个存储简单的是\/否设置的 `Boolean` 变量。  
  
```  
Dim runningVB As Boolean  
' Check to see if program is running on Visual Basic engine.  
If scriptEngine = "VB" Then  
    runningVB = True  
End If  
```  
  
## 请参阅  
 <xref:System.Boolean?displayProperty=fullName>   
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [转换摘要](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [有效使用数据类型](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)   
 [数据类型疑难解答](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [CType 函数](../../../visual-basic/language-reference/functions/ctype-function.md)