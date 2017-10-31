---
title: "如何：在 Visual Basic 中将一个对象转换为其他类型 | Microsoft Docs"
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
  - "对象 [Visual Basic], 转换"
ms.assetid: 60cb5fc7-7ba4-4ab5-9c24-480fa12ddcdc
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# 如何：在 Visual Basic 中将一个对象转换为其他类型
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

通过使用像 [CType 函数](../../../../visual-basic/language-reference/functions/ctype-function.md) 这样的转换关键字，可将 `Object` 变量转换为其他数据类型。  
  
## 示例  
 下面的示例将 `Object` 变量转换为 `Integer` 和 `String`。  
  
```  
Public Sub objectConversion(ByVal anObject As Object)  
    Dim anInteger As Integer  
    Dim aString As String  
    anInteger = CType(anObject, Integer)  
    aString = CType(anObject, String)  
End Sub  
```  
  
 如果知道 `Object` 变量的内容为某个特定的数据类型，最好将该变量转换为那个数据类型。  如果继续使用 `Object` 变量，则会引发*“装箱”*和*“取消装箱”*操作（对于值类型）或*“后期绑定”*操作（对于引用类型）。  这些操作都会需要额外的执行时间，从而导致性能降低。  
  
## 编译代码  
 此示例需要：  
  
-   对 <xref:System?displayProperty=fullName> 命名空间的引用。  
  
## 请参阅  
 <xref:System.Object>   
 [Visual Basic 中的类型转换](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [扩大转换和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [隐式转换和显式转换](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [字符串和其他类型之间的转换](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)   
 [数组转换](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)   
 [结构](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)