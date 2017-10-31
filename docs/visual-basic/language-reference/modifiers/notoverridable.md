---
title: "NotOverridable (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.NotOverridable"
  - "NotOverridable"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "元素, sealed"
  - "方法 [Visual Basic], sealed"
  - "NotOverridable 关键字"
  - "重写"
  - "过程, 重写"
  - "过程, 重新定义"
  - "属性 [Visual Basic], 重写"
  - "属性 [Visual Basic], 重新定义"
  - "密封元素"
  - "密封的方法"
ms.assetid: 66ec6984-f5f5-4857-b362-6a3907aaf9e0
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# NotOverridable (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定不能在派生类中重写属性或过程。  
  
## 备注  
 `NotOverridable` 修饰符在派生类防止方法或属性重写。  [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md) 修饰符允许一个属性或方法在派生类中重写类。  有关更多信息，请参见 [继承的基础知识](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)。  
  
 如果 `Overridable` 或 `NotOverridable` 修饰符未指定，则的默认设置取决于属性或方法是否重写基类的属性或方法。  如果属性或方法重写基类的属性或方法，默认设置为 `Overridable`;否则，为 `NotOverridable`。  
  
 不能被重写的元素有时称为*密封*元素。  
  
 只能在属性和过程声明语句中使用 `NotOverridable`。  您可以仅在重写其他属性或过程的属性或过程上指定 `NotOverridable`，即只与 `Overrides` 组合。  
  
## 合并修饰符  
 不能为 `Private` 方法指定 `Overridable` 或 `NotOverridable` 。  
  
 不能在同一个声明中同时指定 `NotOverridable` 与 `MustOverride`、`Overridable` 或 `Shared`。  
  
## 用法  
 `NotOverridable` 修饰符可用于下面的上下文中：  
  
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## 请参阅  
 [修饰符](../../../visual-basic/language-reference/modifiers/index.md)   
 [继承的基础知识](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)   
 [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)   
 [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)   
 [Overrides](../../../visual-basic/language-reference/modifiers/overrides.md)   
 [关键字](../../../visual-basic/language-reference/keywords/index.md)   
 [Visual Basic 中的隐藏](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)