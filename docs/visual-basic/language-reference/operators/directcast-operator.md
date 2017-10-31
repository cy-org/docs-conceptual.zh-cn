---
title: "DirectCast 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.directCast"
  - "directCast"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "DirectCast 关键字"
ms.assetid: 63e5a1d0-4d9e-4732-bf8f-e90c0c8784b8
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# DirectCast 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

介绍基于继承或实现的类型转换操作。  
  
## 备注  
 在 `Object` 数据类型之间来回转换时，`DirectCast` 不使用 Visual Basic 运行时帮助器例程进行转换，因此它可以提供比 `CType` 更好一些的性能。  
  
 使用 `DirectCast` 关键字的方法与使用 [CType 函数](../../../visual-basic/language-reference/functions/ctype-function.md) 和 [TryCast 运算符](../../../visual-basic/language-reference/operators/trycast-operator.md) 关键字相同。  提供一个表达式作为第一个参数，并提供要将该表达式转化为的类型作为第二个参数。  `DirectCast` 需要两个参数的数据类型之间的继承或实现关系。  这意味着一个类型必须继承自或实现另一个类型。  
  
## 错误和失败  
 如果 `DirectCast` 检测到不存在继承或实现关系，则生成一个编译器错误。  但是不出现编译器错误并不能保证转换成功。  如果需要的转换为收缩转换，它可能在运行时失败。  如果发生这种状况，运行时会引发一个 <xref:System.InvalidCastException> 错误。  
  
## 转换关键字  
 以下是类型转换关键字的对比。  
  
|||||  
|-|-|-|-|  
|关键字|数据类型|参数关系|运行时失败|  
|[CType 函数](../../../visual-basic/language-reference/functions/ctype-function.md)|任何数据类型|必须在两种数据类型之间定义扩大转换或收缩转换|引发 <xref:System.InvalidCastException>|  
|`DirectCast`|任何数据类型|一个类型必须继承自或者实现另一个类型|引发 <xref:System.InvalidCastException>|  
|[TryCast 运算符](../../../visual-basic/language-reference/operators/trycast-operator.md)|仅引用类型|一个类型必须继承自或者实现另一个类型|返回 [Nothing](../../../visual-basic/language-reference/nothing.md)|  
  
## 示例  
 下面的示例演示 `DirectCast` 的两种用法，一种在运行时发生失败，另一种取得成功。  
  
 [!code-vb[VbVbalrKeywords#1](../../../visual-basic/language-reference/codesnippet/VisualBasic/directcast-operator_1.vb)]  
  
 在前面的示例中，`q` 的运行时类型为 `Double`。  `CType` 能够成功是因为 `Double` 可转换为 `Integer`。  但是，第一个 `DirectCast` 在运行时失败是因为 `Double` 的运行时类型与 `Integer` 没有继承关系，即使是可以进行转换。  第二个 `DirectCast` 成功是因为它从 <xref:System.Windows.Forms.Form> 类型转换为 <xref:System.Windows.Forms.Control> 类型，而 <xref:System.Windows.Forms.Form> 继承自该类型。  
  
## 请参阅  
 <xref:System.Convert.ChangeType%2A?displayProperty=fullName>   
 [扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [隐式转换和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)