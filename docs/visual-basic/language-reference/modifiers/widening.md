---
title: "Widening (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.widening"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "转换, 数据类型"
  - "转换, 类型"
  - "数据类型转换"
  - "类型转换"
  - "Widening 关键字"
ms.assetid: 646ae263-94d3-40a2-b0cc-64f619292f56
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Widening (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指示转换运算符 \(`CType`\) 将一个类或结构转换为类型，该类型可保存原始类或结构的所有可能值。  
  
## 用 Widening 关键字转换  
 转换过程除了指定 `Widening` 之外，还必须指定 `Public Shared`。  
  
 扩大转换在运行时始终是成功的，且从不会导致数据丢失。  示例为从 `Single` 转换至 `Double`、从 `Char` 转换至 `String` 以及从派生类型返回至其基类型。  最后一个转换为扩大转换，因为派生类型包含基类型的所有成员，于是为基类型的一个实例。  
  
 使用代码无需利用 `CType` 进行扩大转换，即使 `Option Strict` 为 `On`。  
  
 `Widening` 关键字可用于下面的上下文中：  
  
 [Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
 有关扩大转换和收缩转换运算符的示例定义，请参见[如何：定义转换运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)。  
  
## 请参阅  
 [Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md)   
 [Narrowing](../../../visual-basic/language-reference/modifiers/narrowing.md)   
 [扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [如何：定义运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [CType 函数](../../../visual-basic/language-reference/functions/ctype-function.md)   
 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [如何：定义转换运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)