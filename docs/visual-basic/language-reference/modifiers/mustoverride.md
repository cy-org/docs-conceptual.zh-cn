---
title: "MustOverride (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.MustOverride"
  - "MustOverride"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "元素, 纯虚拟"
  - "MustOverride 关键字"
  - "重写, MustOverride 关键字"
  - "过程, 重写"
  - "过程, 重新定义"
  - "属性 [Visual Basic], 重写"
  - "属性 [Visual Basic], 重新定义"
  - "纯虚拟元素"
  - "虚拟元素, 纯"
ms.assetid: 6e9d9ad6-bb64-433f-b32b-3ef84293bf96
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# MustOverride (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定在这个类中没有实现的属性或过程，且必须在派生类中重写属性或过程后才可以使用。  
  
## 备注  
 只能在属性和过程声明语句中使用 `MustOverride`。  指定 `MustOverride` 的属性或过程必须是类的成员，并且该类必须标记为 [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md)。  
  
## 规则  
  
-   **不完整的声明。**在指定 `MustOverride` 时，请勿为属性或过程提供任何其他代码行，即使 `End Function`、`End Property` 或 `End Sub` 语句也不提供。  
  
-   **组合修饰符。**不能在同一个声明中同时指定 `MustOverride` 与 `NotOverridable`、`Overridable` 或 `Shared`。  
  
-   **隐藏与重写。**隐藏和重写均重新定义继承的元素，但是两种方法之间存在重大差异。  有关更多信息，请参见 [Visual Basic 中的隐藏](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)。  
  
-   **替换术语。**除用在重写中之外，不能再在其他地方使用的元素有时称为“纯虚拟”元素。  
  
 `MustOverride` 修饰符可用于下面的上下文中：  
  
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## 请参阅  
 [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)   
 [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)   
 [Overrides](../../../visual-basic/language-reference/modifiers/overrides.md)   
 [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md)   
 [关键字](../../../visual-basic/language-reference/keywords/index.md)   
 [Visual Basic 中的隐藏](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)