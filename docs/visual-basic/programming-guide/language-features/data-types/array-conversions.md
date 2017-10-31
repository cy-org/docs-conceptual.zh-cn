---
title: "数组转换 (Visual Basic) | Microsoft Docs"
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
  - "数组 [Visual Basic], 转换类型"
  - "数组 [Visual Basic], 数据类型"
  - "转换, 数组类型"
  - "转换, 数据类型"
  - "转换, 类型"
  - "数据类型转换, 数组转换"
  - "对象数组"
  - "对象数组, 转换类型"
  - "类型转换, 数组"
ms.assetid: fceff7d2-a1b7-44c7-b9aa-8bd831d8a444
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# 数组转换 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

您可以将一种数组类型转换为另一种数组类型，但必须满足以下条件：  
  
-   **秩相等。**两个数组的秩必须相同，即它们必须具有相同的维数。  但是，它们各自的维度长度不必相同。  
  
-   **元素数据类型。**两个数组的元素数据类型必须都是引用类型。  不能将 `Integer` 数组转换为 `Long` 数组，或者甚至转换为 `Object` 数组，因为将至少涉及一种值类型。  有关更多信息，请参见 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)。  
  
-   **可转换性。**必须可以在两个数组的元素类型间进行转换（扩大转换或收缩转换）。  不符合此要求的一个例子是，尝试在 `String` 数组和从 <xref:System.Attribute?displayProperty=fullName> 派生的类的数组之间进行转换。  这两种类型迥然不同，它们之间不存在任何性质的转换。  
  
 一种数组类型到另一种数组类型的转换是扩展转换还是双字节到单字节转换，取决于各自元素的转换是扩展转换还是双字节到单字节转换。  有关更多信息，请参见[扩大转换和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)。  
  
## 到对象数组的转换  
 声明 `Object` 数组但没有将其初始化时，只要它保持未初始化，其元素类型便是 `Object`。  将其设置为属于特定类的数组时，它将采用那个类的类型。  但其基本类型仍然是 `Object`，而且之后可以将其设置为另一个属于无关类的数组。  由于所有类都派生自 `Object`，因此可以将数组的元素类型从任何类更改为任何其他类。  
  
 在下面的示例中，虽然类型 `student` 和 `String` 之间不存在转换的可能，但由于两者都是从 `Object` 派生的，因此所有赋值操作均有效。  
  
```  
' Assume student has already been defined as a class.  
Dim testArray() As Object  
' testArray is still an Object array at this point.  
Dim names() As String = New String(3) {"Name0", "Name1", "Name2", "Name3"}  
testArray = New student(3) {}  
' testArray is now of type student().  
testArray = names  
' testArray is now a String array.  
```  
  
### 数组的基础类型  
 如果最初用特定的类声明数组，其基本元素类型就是那个类。  如果之后要将其设置为属于另一个类的数组，则必须在两个类之间进行转换。  
  
 在下面的示例中，`students` 是一个 `student` 数组。  由于在 `String` 和 `student` 之间不存在转换的可能，因此最后一条语句失败。  
  
```  
Dim students() As student  
Dim names() As String = New String(3) {"Name0", "Name1", "Name2", "Name3"}  
students = New Student(3) {}  
' The following statement fails at compile time.  
students = names  
```  
  
## 请参阅  
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [隐式转换和显式转换](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [字符串和其他类型之间的转换](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)   
 [如何：在 Visual Basic 中将一个对象转换为其他类型](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md)