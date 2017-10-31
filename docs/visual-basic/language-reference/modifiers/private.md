---
title: "Private (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Private"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Private 关键字"
  - "Private 关键字, 语法"
ms.assetid: aba74a2e-5824-4613-bf63-b9ec7787f4e6
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# Private (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定一个或多个已声明的编程元素只能从其声明上下文中进行访问（包括从所包含的任何类型中进行访问）。  
  
## 备注  
 如果编程元素表示专有功能或包含机密数据，则通常需要尽最大可能严格限制对它的访问。  最严格的限制是仅允许定义该编程元素的模块、类或结构对其进行访问。  若要依此方法限制对某个元素的访问，可以使用 `Private` 声明此元素。  
  
## 规则  
  
-   **声明上下文。**仅可以在模块级别使用 `Private`。  这意味着 `Private` 元素的声明上下文必须为模块、类或结构，而不能是源文件、命名空间、接口或过程。  
  
## 行为  
  
-   **访问级别。**声明上下文中的所有代码均可访问声明上下文中的 `Private` 元素。  这些代码包括所包含的类型中的代码，如嵌套类或枚举中的赋值表达式。  声明上下文之外的代码不能访问声明上下文中的 `Private` 元素。  
  
-   **访问修饰符。**指定访问级别的关键字称为*“访问修饰符”*。  有关访问修饰符的比较，请参见 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
 `Private` 修饰符可用于下面的上下文中：  
  
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
 [Protected](../../../visual-basic/language-reference/modifiers/protected.md)   
 [Friend](../../../visual-basic/language-reference/modifiers/friend.md)   
 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [过程](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [结构](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)