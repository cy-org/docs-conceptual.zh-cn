---
title: "With...End With 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.With"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "End 关键字, With...End With 语句"
  - "执行, 在对象上"
  - "指令, 重复"
  - "循环结构, 和 With...End With 语句"
  - "对象 [Visual Basic], 访问"
  - "With 块"
  - "With 关键字"
  - "With 语句"
  - "With 语句, 嵌套"
  - "With...End With 语句"
ms.assetid: 340d5fbb-4f43-48ec-a024-80843c137817
caps.latest.revision: 34
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 34
---
# With...End With 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

执行一系列反复引用单个对象或结构的语句，以便这些语句可在访问对象或结构的成员时使用简化语法。使用结构时，你只能读取成员或调用的方法的值，如果你尝试为 `With...End With` 语句中使用的结构的成员赋值，则将收到错误。  
  
## 语法  
  
```  
With objectExpression  
    [ statements ]  
End With  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`objectExpression`|必选。  计算结果为对象的表达式。  表达式可能是任意复杂的，并且只能计算一次。  表达式可以计算为任何数据类型，包括基本类型。|  
|`statements`|可选。  `With` 和 `End With` 之间的一个或多个语句，这些语句可能引用通过计算 `objectExpression` 生成的对象的成员。|  
|`End With`|必选。  终止 `With` 块的定义。|  
  
## 备注  
 通过使用 `With...End With`，你可对指定对象执行一系列语句，而无需多次指定对象名称。  在 `With` 语句块内，你可指定以句点开头的对象的成员，就像它前面有 `With` 语句对象一样。  
  
 例如，若要更改单个对象的多个属性，请将属性分配语句放在 `With...End With` 块中，这样只需引用一次对象，而不是为每个属性分配都引用一次对象。  
  
 如果代码访问多个语句中的同一个对象，则使用 `With` 语句将获得下列好处：  
  
-   你不必多次计算复杂的表达式，或者多次将结果分配给临时变量来引用其成员。  
  
-   通过消除反复限定表达式，你提高了代码的可读取性。  
  
 `objectExpression` 的数据类型可以是任何类或结构类型，甚至可以是 Visual Basic 基础类型（如 `Integer`）。如果 `objectExpression` 生成对象之外的任何内容，则你只能读取其成员或调用的方法的值，如果你尝试为 `With...End With` 语句中使用的结构的成员赋值，则将收到错误。此错误与你在调用返回一个结构的方法并立即访问函数结果（如 `GetAPoint().x = 1`）的成员并为其赋值时收到的错误一样。这两种情况的问题是，结构仅存在于调用堆栈上，并且已修改的结构成员在这些情况下无法写入到一个位置以使程序中的所有其他代码可以观察到更改。  
  
 在进入块时仅计算 `objectExpression` 一次。  你无法从 `With` 块中重新分配 `objectExpression`。  
  
 在 `With` 块中，你可访问仅指定对象的方法和属性，而不必限定它们。  你可以使用其他对象的方法和属性，但是必须用其对象名限定它们。  
  
 你可以将一个 `With...End With` 语句放置在另一个语句中。  如果未从上下文中清除引用的对象，则嵌套的 `With...End With` 语句可能产生混乱。  从内部的 `With` 块内引用外部的 `With` 块中的某个对象时，你必须提供对该对象的完全限定的引用。  
  
 你不能从 `With` 语句块的外部分支到此语句块。  
  
 除非此语句块包含循环，否则这些语句只运行一次。  你可嵌套不同类型的控制结构。  有关详细信息，请参阅[嵌套的控件结构](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)。  
  
> [!NOTE]
>  你还可在对象初始值设定项中使用 `With` 关键字。  有关更多信息和示例，请参见[对象初始值设定项：命名类型和匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)和[匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
>   
>  如果你使用 `With` 块只是为了初始化已实例化的对象的属性或字段，请考虑改用对象初始值设定项。  
  
## 示例  
 在下面的示例中，每个 `With` 块将对单个对象执行一系列语句。  
  
 [!code-vb[VbVbalrWithStatement#2](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/with-end-with-statement_1.vb)]  
  
## 示例  
 下面的示例嵌套 `With…End With` 语句。  在嵌套的 `With` 语句中，语法引用内部对象。  
  
 [!code-vb[VbVbalrWithStatement#1](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/with-end-with-statement_2.vb)]  
  
## 请参阅  
 <xref:System.Collections.Generic.List%601>   
 [嵌套的控件结构](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [对象初始值设定项：命名类型和匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)