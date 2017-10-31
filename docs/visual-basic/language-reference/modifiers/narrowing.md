---
title: "Narrowing (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.narrowing"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "转换, 数据类型"
  - "转换, 类型"
  - "数据类型转换"
  - "Narrowing 关键字"
  - "类型转换"
ms.assetid: a207ee91-aca4-4771-b4e2-713f029bf2bb
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# Narrowing (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指示转换运算符 \(`CType`\) 将一个类或结构转换为某种类型，该类型可能无法保存原始类或结构的某些可能值。  
  
## 使用 Narrowing 关键字转换  
 转换过程除了指定 `Narrowing` 之外，还必须指定 `Public Shared`。  
  
 收缩转换在运行时并不总会成功，可能会失败或导致数据丢失。  示例为从 `Long` 转换至 `Integer`、从 `String` 转换至 `Date`，以及从基类型转换至派生类型。  最后一个转换为收缩转换，因为基类型可能不包含派生类型的所有成员，这样基类型就不是派生类型的一个实例。  
  
 如果 `Option Strict` 为 `On`，所使用的代码必须对所有收缩转换使用 `CType`。  
  
 `Narrowing` 关键字可用于下面的上下文中：  
  
 [Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
## 请参阅  
 [Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md)   
 [Widening](../../../visual-basic/language-reference/modifiers/widening.md)   
 [扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [如何：定义运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [CType 函数](../../../visual-basic/language-reference/functions/ctype-function.md)   
 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)