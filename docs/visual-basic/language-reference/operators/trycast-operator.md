---
title: "TryCast 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.trycast"
  - "trycast"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "TryCast 关键字"
ms.assetid: d1ef5d47-fef4-491e-b014-1d910628f65c
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# TryCast 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

引入不引发异常的类型转换操作。  
  
## 备注  
 如果尝试转换失败，则 `CType` 和 `DirectCast` 都会引发 <xref:System.InvalidCastException> 错误。  这将给应用程序的性能造成负面影响。  `TryCast` 返回 [Nothing](../../../visual-basic/language-reference/nothing.md)，因此只需测试返回的结果是否为 `Nothing`，而无需处理可能产生的异常。  
  
 使用 `TryCast` 关键字的方法与使用 [CType 函数](../../../visual-basic/language-reference/functions/ctype-function.md) 和 [DirectCast 运算符](../../../visual-basic/language-reference/operators/directcast-operator.md) 关键字的方法相同。  提供一个表达式作为第一个参数，并提供要将该表达式转化为的类型作为第二个参数。  `TryCast` 只处理引用类型，如类和接口。  它要求这两种类型之间的关系为继承或实现。  这意味着一个类型必须继承自或实现另一个类型。  
  
## 错误和失败  
 如果 `TryCast` 检测到不存在任何继承或实现关系，它将生成一个编译器错误。  但是不出现编译器错误并不能保证转换成功。  如果需要的转换为收缩转换，它可能在运行时失败。  如果发生这种情况，`TryCast` 返回 [Nothing](../../../visual-basic/language-reference/nothing.md)。  
  
## 转换关键字  
 以下是类型转换关键字的对比。  
  
|||||  
|-|-|-|-|  
|关键字|数据类型|参数关系|运行时失败|  
|[CType 函数](../../../visual-basic/language-reference/functions/ctype-function.md)|任何数据类型|必须在两种数据类型之间定义扩大转换或收缩转换|引发 <xref:System.InvalidCastException>|  
|[DirectCast 运算符](../../../visual-basic/language-reference/operators/directcast-operator.md)|任何数据类型|一个类型必须继承自或者实现另一个类型|引发 <xref:System.InvalidCastException>|  
|`TryCast`|仅引用类型|一个类型必须继承自或者实现另一个类型|返回 [Nothing](../../../visual-basic/language-reference/nothing.md)|  
  
## 示例  
 下面的示例显示如何使用 `TryCast`。  
  
 [!code-vb[VbVbalrKeywords#6](../../../visual-basic/language-reference/codesnippet/VisualBasic/trycast-operator_1.vb)]  
  
## 请参阅  
 [扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [隐式转换和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)