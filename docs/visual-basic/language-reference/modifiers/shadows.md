---
title: "Shadows (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Shadows"
  - "shadows"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "重复的名称"
  - "名称, 阴影操作"
  - "范围, 阴影操作"
  - "阴影操作"
  - "Shadows 关键字"
ms.assetid: 6bf687cd-0544-4797-b51b-911125ec57c6
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Shadows (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定已声明的编程元素重新声明并隐藏基类中的同名元素或重载元素集。  
  
## 备注  
 隐藏（又称为*按名称隐藏*）的主要目的是保护类成员的定义。  基类可能会经历这样的变化：用您已经定义的相同名称创建元素。  如果发生这种变化，`Shadows` 修饰符就会通过您的类强制引用被解析为您定义的成员，而不是解析为新的基类元素。  
  
 隐藏和重写均重新定义继承的元素，但是两种方法之间存在重大差异。  有关更多信息，请参见 [Visual Basic 中的隐藏](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)。  
  
## 规则  
  
-   **声明上下文。**只能在类级使用 `Shadows`。  这意味着 `Shadows` 元素的声明上下文必须是类，不能是源文件、命名空间、接口、模块、结构或过程。  
  
     在单个声明语句中只能声明一个隐藏元素。  
  
-   **组合修饰符。**不能在同一个声明中同时指定 `Shadows` 与 `Overloads`、`Overrides` 或 `Static`。  
  
-   **元素类型。**可以用其他任何类型的元素来隐藏任何类型的被声明元素。  如果用其他过程或属性隐藏某个属性或过程，则参数和返回类型不必非要与基类属性或过程中的参数和返回类型匹配。  
  
-   **访问。**基类中隐藏的元素在隐藏它的派生类中通常不可用。  但是，以下注意事项仍是适用的：  
  
    -   如果从引用隐藏元素的代码无法访问该元素，则引用被解析为被隐藏的元素。  例如，如果 `Private` 元素隐藏一个基类元素，则无权访问 `Private` 元素的代码会改为访问基类元素。  
  
    -   如果您隐藏某个元素，仍然可以通过用基类的类型所声明的对象来访问被隐藏的元素。  也可以通过 `MyBase` 访问它。  
  
 `Shadows` 修饰符可用于下面的上下文中：  
  
 [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)  
  
 [Const 语句](../../../visual-basic/language-reference/statements/const-statement.md)  
  
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 [Delegate 语句](../../../visual-basic/language-reference/statements/delegate-statement.md)  
  
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Enum 语句](../../../visual-basic/language-reference/statements/enum-statement.md)  
  
 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## 请参阅  
 [Shared](../../../visual-basic/language-reference/modifiers/shared.md)   
 [Static](../../../visual-basic/language-reference/modifiers/static.md)   
 [Private](../../../visual-basic/language-reference/modifiers/private.md)   
 [Me、My、MyBase 和 MyClass](../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)   
 [继承的基础知识](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)   
 [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)   
 [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)   
 [Overloads](../../../visual-basic/language-reference/modifiers/overloads.md)   
 [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)   
 [Overrides](../../../visual-basic/language-reference/modifiers/overrides.md)   
 [Visual Basic 中的隐藏](../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)