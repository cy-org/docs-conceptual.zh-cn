---
title: "Friend (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Friend"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Friend 关键字"
  - "Friend 访问修饰符"
  - "Friend 关键字, 语法"
  - "Protected Friend 关键字组合"
  - "Friend 关键字和 Protected"
ms.assetid: b664605e-1c79-4728-b996-aa59c50846bc
caps.latest.revision: 25
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 25
---
# Friend (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定只能从包含其声明的程序集内部来访问一个或多个所声明的编程元素。  
  
## 备注  
 许多情况下，需要让整个程序集使用某些编程元素（如类或结构），而不是只是让声明它们的组件使用。  但是，您可能不希望将其进行访问由程序集外部的代码 \(例如，因此，如果应用程序是专有技术\)。  如果要这样的限制对组件的访问，使用 `Friend` 修饰符，可以将其声明为。  
  
 编译到同一程序集的其他类、结构和模块中的代码可以访问该程序集中的所有 `Friend` 元素。  
  
 `Friend` 访问通常是应用程序的编程元素的优先级别，因此，`Friend` 是接口、模块、选件类或结构的默认值访问级别。  
  
 仅可以 `Friend` 在模块、接口或命名空间级别。  因此，`Friend` 元素的声明上下文必须是源文件、命名空间、接口、模块、选件类或结构；它不能为程序。  
  
 您可以将 `Friend` 修饰符与同一个声明中的 [Protected](../../../visual-basic/language-reference/modifiers/protected.md) 修饰符结合起来使用。  此组合在声明元素商谈 `Friend` 访问和受保护的访问，因此，它们是可访问的中的任何位置相同程序集，从其选件类和派生类。  只能对类的成员指定 `Protected Friend`。  
  
 有关 `Friend` 和其他访问修饰符的比较，请参见 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
> [!NOTE]
>  可以指定另一个程序集是友元程序集，提供它访问所有类型和成员标记为 `Friend`。  有关更多信息，请参见[友元程序集](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)。  
  
## 示例  
 下面的类使用 `Friend` 修饰符来允许同一程序集内的其他编程元素访问某些成员。  
  
 [!code-vb[VbVbalrAccessModifiers#1](../../../visual-basic/language-reference/modifiers/codesnippet/VisualBasic/friend_1.vb)]  
  
## 用法  
 可以在下列上下文使用 `Friend` 修饰符：  
  
 [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)  
  
 [Const 语句](../../../visual-basic/language-reference/statements/const-statement.md)  
  
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
 [Delegate 语句](../../../visual-basic/language-reference/statements/delegate-statement.md)  
  
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Enum 语句](../../../visual-basic/language-reference/statements/enum-statement.md)  
  
 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 [Module 语句](../../../visual-basic/language-reference/statements/module-statement.md)  
  
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## 请参阅  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>   
 [Public](../../../visual-basic/language-reference/modifiers/public.md)   
 [Protected](../../../visual-basic/language-reference/modifiers/protected.md)   
 [Private](../../../visual-basic/language-reference/modifiers/private.md)   
 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [过程](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [结构](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)