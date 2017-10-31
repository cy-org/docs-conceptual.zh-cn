---
title: "可修改和不可修改参数之间的差异 (Visual Basic) | Microsoft Docs"
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
  - "变量 [Visual Basic], 可修改的"
  - "变量 [Visual Basic], 不可修改的"
  - "过程参数"
  - "过程, 参数"
  - "Visual Basic 代码, 过程"
ms.assetid: 87b2df69-e1f7-4657-9caf-b3f48d693428
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# 可修改和不可修改参数之间的差异 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

当调用过程时，通常要将一个或多个参数传递给它。  每个参数对应于一个基础编程元素。  基础元素和参数可更改还是不可更改。  
  
## 可更改和不可更改元素  
 一个编程元素可以是 " *可更改元素*，可以有它的已更改值， *不可更改*元素，一次具有固定值它已创建。  
  
 下表列出了可更改和不可更改的编程元素。  
  
|可更改元素|不可更改元素|  
|-----------|------------|  
|局部变量 \(在过程内声明\)，包括对象变量，不包括只读|只读变量、字段和属性|  
|字段 \(模块、类和结构的成员变量\)，不包括只读|常数和文本|  
|属性，不包括只读|枚举成员|  
|数组元素|表达式 \(即使元素可更改\)|  
  
## 可更改和不可更改参数  
 *可修改的参数* 是一个带有可更改基础元素。  调用代码可以随时存储一个新值，，并且，如果您传递参数， [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)过程中的代码还可以更改调用代码中的基础元素。  
  
 *不可更改参数* 具有不可更改的基础元素或者传递 [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)。  该过程不能更改调用代码中的基础元素，因此，即使它是一个可修改的元素。  如果是不可更改元素，调用代码不能修改它。  
  
 被调用过程可以更改它的不可更改参数的本地副本，，但更改不会影响调用代码中的基础元素。  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [如何：将参数传递给过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-pass-arguments-to-a-procedure.md)   
 [通过值和通过引用传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [通过值传递参数和通过引用传递参数之间的差异](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md)   
 [如何：更改过程参数的值](../../../../visual-basic/programming-guide/language-features/procedures/how-to-change-the-value-of-a-procedure-argument.md)   
 [如何：防止过程参数的值被更改](../../../../visual-basic/programming-guide/language-features/procedures/how-to-protect-a-procedure-argument-against-value-changes.md)   
 [如何：强制通过值传递参数](../../../../visual-basic/programming-guide/language-features/procedures/how-to-force-an-argument-to-be-passed-by-value.md)   
 [按位置和按名称传递参数](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-position-and-by-name.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)