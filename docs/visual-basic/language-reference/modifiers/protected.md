---
title: "Protected (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Protected"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Protected 访问修饰符"
  - "Protected Friend 关键字组合"
  - "Protected 关键字"
  - "Protected 关键字, 和 Friend"
  - "Protected 关键字, 语法"
ms.assetid: 74ad3d56-309f-49d2-b60c-1d0157d010e8
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Protected (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定一个或多个已声明的编程元素只能从其自身的类或派生类访问。  
  
## 备注  
 有时在某个类中声明的编程元素包含敏感数据或受限制的代码，因而您想要限制对该元素的访问。  但是，如果此类是可继承的，且之前已经有派生类的层次结构，则这些派生类可能需要访问此数据或代码。  在这种情况下，您希望可从基类和从所有派生类均可访问该元素。  若要依此方法限制对某个元素的访问，可以使用 `Protected` 声明此元素。  
  
## 规则  
  
-   **声明上下文。**只能在类级使用 `Protected`。  这意味着 `Protected` 元素的声明上下文必须是类，不能是源文件、命名空间、接口、模块、结构或过程。  
  
-   **组合修饰符。**您可以将 `Protected` 修饰符与同一个声明中的 [Friend](../../../visual-basic/language-reference/modifiers/friend.md) 修饰符结合起来使用。  使用此组合，可以从已声明元素的相同程序集的任何地方、其自身的类以及派生类访问这些元素。  只能对类的成员指定 `Protected Friend`。  
  
## 行为  
  
-   **访问级别。**类中的所有代码均可以访问该类的元素。  派生自基类的任何类中的代码可以访问此基类的所有 `Protected` 元素。  对每一代的派生均如此。  这意味着某个类可以访问其基类的基类的（依此类推）`Protected` 元素。  
  
     受保护访问不是友元访问的超集或子集。  
  
-   **访问修饰符。**指定访问级别的关键字称为*“访问修饰符”*。  有关访问修饰符的比较，请参见 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
 `Protected` 修饰符可用于下面的上下文中：  
  
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
 [Public](../../../visual-basic/language-reference/modifiers/public.md)   
 [Friend](../../../visual-basic/language-reference/modifiers/friend.md)   
 [Private](../../../visual-basic/language-reference/modifiers/private.md)   
 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [过程](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [结构](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)