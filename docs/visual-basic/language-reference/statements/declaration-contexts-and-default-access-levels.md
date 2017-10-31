---
title: "声明上下文和默认访问级别 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "访问级别, 默认级别"
  - "访问级别, Visual Basic"
  - "声明上下文, Visual Basic"
  - "模块级别, 已定义"
  - "命名空间级别, 已定义"
  - "过程级别, 已定义"
ms.assetid: bf63b96e-e825-4745-88c8-5dae222728db
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 声明上下文和默认访问级别 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

此主题介绍哪些 Visual Basic 类型可以在其他类型内进行声明，以及在未指定访问级别时各自的默认访问级别如何。  
  
## 声明上下文级别  
 编程元素的声明上下文是指声明编程元素的代码区域。  声明上下文在很多时候也是另一个编程元素，这样的编程元素称为“包含元素”。  
  
 声明上下文的级别包括：  
  
-   命名空间级 \- 在源文件或命名空间内，但不在类、结构、模块或接口内  
  
-   模块级 \- 在类、结构、模块或接口内，但不在过程或块内  
  
-   过程级 \- 在过程或块（如 `If` 或 `For`）内  
  
 下表显示各种已声明的编程元素的默认访问级别（取决于其声明上下文）。  
  
|已声明元素|命名空间级|模块级|过程级|  
|-----------|-----------|---------|---------|  
|变量 \([Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)\)|不允许|`Private`（在 `Structure` 中为 `Public`；在 `Interface` 中不允许）|`Public`|  
|常数 \([Const 语句](../../../visual-basic/language-reference/statements/const-statement.md)\)|不允许|`Private`（在 `Structure` 中为 `Public`；在 `Interface` 中不允许）|`Public`|  
|枚举 \([Enum 语句](../../../visual-basic/language-reference/statements/enum-statement.md)\)|`Friend`|`Public`|不允许|  
|类 \([Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)\)|`Friend`|`Public`|不允许|  
|结构 \([Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md)\)|`Friend`|`Public`|不允许|  
|模块 \([Module 语句](../../../visual-basic/language-reference/statements/module-statement.md)\)|`Friend`|不允许|不允许|  
|接口 \([Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)\)|`Friend`|`Public`|不允许|  
|过程 \([Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)、[Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)\)|不允许|`Public`|不允许|  
|外部接口 \([Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)\)|不允许|`Public`（在 `Interface` 中不允许）|不允许|  
|运算符 \([Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md)\)|不允许|`Public`（在 `Interface` 或 `Module` 中不允许）|不允许|  
|属性 \([Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)\)|不允许|`Public`|不允许|  
|默认属性 \([Default](../../../visual-basic/language-reference/modifiers/default.md)\)|不允许|`Public`（在 `Module` 中不允许）|不允许|  
|事件 \([Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)\)|不允许|`Public`|不允许|  
|委托 \([Delegate 语句](../../../visual-basic/language-reference/statements/delegate-statement.md)\)|`Friend`|`Public`|不允许|  
  
 有关更多信息，请参见 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
## 请参阅  
 [Friend](../../../visual-basic/language-reference/modifiers/friend.md)   
 [Private](../../../visual-basic/language-reference/modifiers/private.md)   
 [Public](../../../visual-basic/language-reference/modifiers/public.md)