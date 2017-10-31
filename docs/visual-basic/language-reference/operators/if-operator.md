---
title: "If 运算符 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.IfOperator"
  - "IfOperator"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "有条件执行"
  - "条件运算符 [Visual Basic]"
  - "If 表达式 [Visual Basic]"
  - "If 运算符 [Visual Basic]"
  - "三元运算符"
ms.assetid: dd56c9df-7cd4-442c-9ba6-20c70ee44c8f
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# If 运算符 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

使用短路计算按条件返回两个值中的一个。  可以使用三个参数或两个参数调用 `If` 运算符。  
  
## 语法  
  
```  
If( [argument1,] argument2, argument3 )  
```  
  
## 使用三个参数调用 If 运算符  
 在使用三个参数调用 `If` 时，第一个参数的计算结果必须为一个可以强制转换为 `Boolean` 值的值。  该 `Boolean` 值将确定要计算并返回其他两个参数中的哪一个。  下面的列表仅当使用三个参数调用 `If` 运算符时适用。  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`argument1`|必选。  `Boolean`.  确定要计算并返回其他两个参数中的哪一个。|  
|`argument2`|必选。  `Object`.  在 `argument1` 的计算结果为 `True` 时计算并返回。|  
|`argument3`|必选。  `Object`.  计算并返回，如果 `argument1` 计算结果为 `False` ，或者 `argument1` 是计算结果为 [nothing](../../../visual-basic/language-reference/nothing.md)的 [Null](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)`Boolean` 变量。|  
  
 使用三个参数调用的 `If` 运算符的工作方式与 `IIf` 函数相似，只不过该运算符使用短路计算。  `IIf` 函数始终计算所有三个参数的结果，而具有三个参数的 `If` 运算符仅计算其中两个参数的结果。  第一个 `If` 参数将进行计算，并且结果被强制转换为 `Boolean` 值（`True` 或 `False`）。  如果该值为 `True`，则计算 `argument2` 并返回其值，但是不计算 `argument3`。  如果 `Boolean` 表达式的值为 `False`，则计算 `argument3` 并返回其值，但是不计算 `argument2`。  下面的示例演示在使用三个参数时 `If` 的用法：  
  
 [!code-vb[VbVbalrOperators#100](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/if-operator_1.vb)]  
  
 下面的示例演示短路计算的值。  示例演示将变量 `number` 除以变量 `divisor` 的两次尝试，其中 `divisor` 不为零。  在该值为零时，则应返回 0，并且不应尝试执行该除法运算，否则会导致运行时错误。  因为 `If` 表达式使用短路计算，所以该表达式会根据第一个参数的值来计算第二个参数或第三个参数。  如果第一个参数为 true，则 divisor 不为零，可以安全地计算第二个参数并执行除法。  如果第一个参数为 false，则仅计算第三个参数并返回 0。  因此，当 divisor 为 0 时，不会尝试执行除法，也不会产生错误。  但是，因为 `IIf` 不使用短路计算，所以即使第一个参数为 false，也会计算第二个参数。  这会导致运行时被零除错误。  
  
 [!code-vb[VbVbalrOperators#101](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/if-operator_2.vb)]  
  
## 使用两个参数调用 If 运算符  
 可以省略 `If` 的第一个参数。  这样便可以仅使用两个参数来调用该运算符。  下面的列表仅当使用两个参数调用 `If` 运算符时适用。  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`argument2`|必选。  `Object`.  必须是引用或可以为 null 的类型。  在其计算结果为除 `Nothing` 以外的任何值时计算并返回。|  
|`argument3`|必选。  `Object`.  在 `argument2` 的计算结果为 `Nothing` 时计算并返回。|  
  
 省略 `Boolean` 参数时，第一个参数必须是引用或可以为 null 的类型。  如果第一个参数的计算结果为 `Nothing`，则返回第二个参数的值。  在其他所有情况下，都返回第一个参数的值。  下面的示例演示如何进行此计算。  
  
 [!code-vb[VbVbalrOperators#102](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/if-operator_3.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Interaction.IIf%2A>   
 [可以为 Null 的值类型](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)   
 [Nothing](../../../visual-basic/language-reference/nothing.md)