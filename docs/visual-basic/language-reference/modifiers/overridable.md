---
title: "Overridable (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "Overridable"
  - "vb.Overridable"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "具体元素"
  - "元素, 具体"
  - "元素, virtual"
  - "Overridable 关键字"
  - "重写, Overridable 关键字"
  - "过程, 重写"
  - "过程, 重新定义"
  - "属性 [Visual Basic], 重写"
  - "属性 [Visual Basic], 重新定义"
  - "虚拟元素"
ms.assetid: 612581e7-8a4c-4a5d-beff-3402fffa6f35
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Overridable (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定属性或过程可由派生类中同名的属性或过程进行重写。  
  
## 备注  
 `Overridable` 修饰符允许一个属性或方法在派生类中重写类。  [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md) 修饰符在派生类防止方法或属性重写。  有关更多信息，请参见 [继承的基础知识](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)。  
  
 如果 `Overridable` 或 `NotOverridable` 修饰符未指定，则的默认设置取决于属性或方法是否重写基类的属性或方法。  如果属性或方法重写基类的属性或方法，默认设置为 `Overridable`;否则，为 `NotOverridable`。  
  
 可以通过隐藏或重写来重新定义继承的元素，但是这两种方法之间存在重大差异。  有关更多信息，请参见 [Visual Basic 中的隐藏](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)。  
  
 可被重写的元素有时称为“虚拟”元素。  如果它可被重写，但是无需重写，有时又称为“具体”元素。  
  
 只能在属性和过程声明语句中使用 `Overridable`。  
  
## 合并修饰符  
 不能为 `Private` 方法指定 `Overridable` 或 `NotOverridable` 。  
  
 不能在同一个声明中同时指定 `Overridable` 与 `MustOverride`、`NotOverridable` 或 `Shared`。  
  
 因为重写元素隐式可重写，所以无法将 `Overridable` 与 `Overrides` 组合在一起。  
  
## 用法  
 `Overridable` 修饰符可用于下面的上下文中：  
  
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## 请参阅  
 [修饰符](../../../visual-basic/language-reference/modifiers/index.md)   
 [继承的基础知识](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)   
 [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)   
 [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)   
 [Overrides](../../../visual-basic/language-reference/modifiers/overrides.md)   
 [关键字](../../../visual-basic/language-reference/keywords/index.md)   
 [Visual Basic 中的隐藏](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)