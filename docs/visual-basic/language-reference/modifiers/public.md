---
title: "Public (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Public"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "公共访问修饰符"
  - "Public 关键字"
  - "Public 关键字, 语法"
ms.assetid: 284c9e1b-ed23-499b-9bc9-ad87c11485a5
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# Public (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定一个或多个声明的编程元素没有访问限制。  
  
## 备注  
 如果正在发布一个组件或一组组件（例如类库），通常会想要编程元素可以被与程序集互操作的任何代码访问。  若要授予这种对元素的无限制访问，可以用 `Public` 声明该元素。  
  
 公共访问是在不需要限制对编程元素的访问时的正常级别。  请注意，如果不另行声明，在接口、模块、类或结构内声明的元素的访问级别默认为 `Public`。  
  
## 规则  
  
-   **声明上下文。**仅可以在模块、接口或命名空间级别使用 `Public`。  这意味着 `Public` 元素的声明上下文必须是源文件、命名空间、接口、模块、类或结构，而不能是过程。  
  
## 行为  
  
-   **访问级别。**可以访问模块、类或结构的所有代码都可以访问其 `Public` 元素。  
  
-   **默认访问。**过程内的局部变量默认为公共访问，您不能对它们使用任何访问修饰符。  
  
-   **访问修饰符。**指定访问级别的关键字称为*“访问修饰符”*。  有关访问修饰符的比较，请参见 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
 `Public` 修饰符可用于下面的上下文中：  
  
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
  
 [Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md)  
  
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## 请参阅  
 [Protected](../../../visual-basic/language-reference/modifiers/protected.md)   
 [Friend](../../../visual-basic/language-reference/modifiers/friend.md)   
 [Private](../../../visual-basic/language-reference/modifiers/private.md)   
 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [过程](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [结构](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)