---
title: "Default (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Default"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Default 关键字 [Visual Basic]"
  - "默认属性"
  - "默认属性, Visual Basic 中"
  - "默认值, 属性"
  - "属性 [Visual Basic], default"
ms.assetid: 45fce9b9-d212-4b2d-ab86-6e359b8b57af
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Default (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

将一个属性标识为类、结构或接口的默认属性。  
  
## 备注  
 类、结构或接口最多可以将其一个属性指定为“默认属性”，前提是该属性至少带有一个参数。  如果代码引用某个类或结构，而没有指定成员，Visual Basic 将该引用解析到默认属性。  
  
 默认属性可以稍微减少源代码字符数，但是会使代码更难阅读。  如果调用代码不熟悉您的类或结构，当它引用类或结构名称时，它就不能肯定该引用是访问该类或结构本身，还是访问默认属性。  这可能导致编译器错误或细小的运行时逻辑错误。  
  
 通过始终使用 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md) 将编译器类型检查设置为 `On`，可以在某种程度上降低默认属性错误的机会。  
  
 如果您计划在代码中使用预定义类或结构，则必须确定它是否具有默认属性；如果有，还必须确定其名称。  
  
 由于存在这些缺点，您应该考虑不定义默认属性。  为了代码的可读性，您还应考虑始终显式引用所有属性，包括默认属性。  
  
 `Default` 修饰符可用于下面的上下文中：  
  
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
## 请参阅  
 [如何：在 Visual Basic 中声明和调用默认属性](../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [关键字](../../../visual-basic/language-reference/keywords/index.md)