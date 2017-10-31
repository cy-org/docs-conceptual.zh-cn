---
title: "如何：将一个数组赋给另一个数组 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数组 [Visual Basic], 分配"
  - "数组 [Visual Basic], 协变"
  - "协变, 数组"
ms.assetid: 1ae89ea5-f292-4282-bcfc-e9b06b37fbd5
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# 如何：将一个数组赋给另一个数组 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

由于数组是对象，因此它和其他对象类型一样，可以用在赋值语句中。  数组变量持有一个指针，它指向构成数组元素的数据及秩和长度信息，赋值语句仅复制此指针。  
  
### 将一个数组赋给另一个数组  
  
1.  请确保两个数组具有相同的秩（维数）和兼容的元素数据类型。  
  
2.  使用标准赋值语句将源数组赋给目标数组。  数组名后不要跟括号。  
  
    ```  
    Dim formArray() As System.Windows.Forms.Form  
    Dim controlArray() As System.Windows.Forms.Control  
    controlArray = formArray  
    ```  
  
 将一个数组赋给另一个数组时，必须遵守以下规则：  
  
-   **相等的秩。**目标数组的秩（维数）必须与源数组的秩相同。  
  
     如果两个数组的秩相同，它们的维数不必相同。  给定维中的元素数目在赋值时可以更改。  
  
-   **元素类型。**要么两个数组的元素都是引用类型元素，要么都是值类型元素。  有关更多信息，请参见 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)。  
  
    -   如果两个数组的元素都是值类型元素，则元素的数据类型必须完全相同。  唯一的例外是，可以将 `Enum` 元素的数组赋给该 `Enum` 的基类型的数组。  
  
    -   如果两个数组都含有引用类型元素，则源元素类型必须是从目标元素类型派生的。  在这种情况下，两个数组具有与其元素相同的继承关系。  这称为“数组协方差”。  
  
 如果违反了上述规则，如当数据类型不兼容或者秩不相等时，编译器会报错。  可以在程序中添加错误处理代码，来确保数组在赋值前是相容的。  如果希望避免引发异常，也可以使用 [TryCast 运算符](../../../../visual-basic/language-reference/operators/trycast-operator.md) 关键字。  
  
## 请参阅  
 [数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [数组疑难解答](../../../../visual-basic/programming-guide/language-features/arrays/troubleshooting-arrays.md)   
 [Enum 语句](../../../../visual-basic/language-reference/statements/enum-statement.md)   
 [数组转换](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)