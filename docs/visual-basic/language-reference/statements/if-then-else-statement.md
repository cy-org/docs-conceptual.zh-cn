---
title: "If...Then...Else 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.ElseIf"
  - "vb.Then"
  - "vb.If"
  - "vb.EndIf"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "分支, 条件"
  - "控制流, 分支"
  - "Else 语句 [Visual Basic]"
  - "ElseIf 语句, If...Then...Else"
  - "执行, 条件"
  - "If 运算符 [Visual Basic]"
  - "If 语句"
  - "If 语句, If...Then...Else"
  - "If...Then...Else 语句"
  - "IIf 函数, 和 If...Then...Else 语句"
  - "Is 运算符 [Visual Basic], 在 If...Then...Else 语句中"
  - "Then 语句, If...Then...Else"
  - "TypeOf...Is 表达式, 和 If...Then...Else 语句"
ms.assetid: 790068a2-1307-4e28-8a72-be5ebda099e9
caps.latest.revision: 29
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 29
---
# If...Then...Else 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

根据表达式的值有条件地执行一组语句。  
  
## 语法  
  
```  
' Multiple-line syntax:  
If condition [ Then ]  
    [ statements ]  
[ ElseIf elseifcondition [ Then ]  
    [ elseifstatements ] ]  
[ Else  
    [ elsestatements ] ]  
End If  
  
' Single-line syntax:  
If condition Then [ statements ] [ Else [ elsestatements ] ]  
```  
  
## 部件  
 `condition`  
 必需。  表达式。  计算结果必须为 `True` 或 `False` 或者可隐式转换为 `Boolean` 的数据类型。  
  
 如果表达式是计算结果为 [nothing](../../../visual-basic/language-reference/nothing.md)的 [可以为 Null](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)`Boolean` 变量，条件处理，就好像该表达式不 `True`，并且，`Else` 块中执行。  
  
 `Then`  
 在单行语法中为必选项，在多行语法中为可选。  
  
 `statements`  
 可选。  跟在 `If`...`Then` 后面的一条或多条语句，如果 `condition` 的计算结果为 `True`，则执行这些语句。  
  
 `elseifcondition`  
 如果存在 `ElseIf`，则为必选。  表达式。  计算结果必须为 `True` 或 `False` 或者可隐式转换为 `Boolean` 的数据类型。  
  
 `elseifstatements`  
 可选。  跟在 `ElseIf`...`Then` 后面的一条或多条语句，如果 `elseifcondition` 的计算结果为 `True`，则执行这些语句。  
  
 `elsestatements`  
 可选。  一条或多条语句，如果前面的 `condition` 或 `elseifcondition` 表达式的计算结果都不是 `True`，则会执行这些语句。  
  
 `End If`  
 终止 `If`...`Then`...`Else` 块。  
  
## 备注  
  
## 多行语法  
 当遇到 `If`...`Then`...`Else` 语句时，`condition` 将被测试。  如果 `condition` 为 `True`，则会执行 `Then` 之后的语句。  如果 `condition` 为 `False`，则按顺序计算每个 `ElseIf` 语句（如果有）。  如果找到某个值为 `True` 的 `elseifcondition`，则会执行紧跟在关联的 `ElseIf` 之后的语句。  如果没有任何 `elseifcondition` 的计算结果为 `True`，或者没有 `ElseIf` 语句，则会执行 `Else` 之后的语句。  执行了 `Then`、`ElseIf` 或 `Else` 后面的语句之后，将继续执行 `End If` 之后的语句。  
  
 `ElseIf` 和 `Else` 子句都是可选。  可以根据需要在 `If`...`Then`...`Else` 语句中放置任意多个 `ElseIf` 子句，但 `ElseIf` 子句不能出现在 `Else` 子句后面。  `If`...`Then`...`Else` 语句可以相互嵌套。  
  
 在多行语法中，第一行只能是 `If` 语句。  `ElseIf`、`Else` 和 `End If` 语句的前面只能有行标签。  `If`...`Then`...`Else` 块必须以 `End If` 语句结尾。  
  
> [!TIP]
>  当计算具有若干可能值的单个表达式时，[Select...Case 语句](../../../visual-basic/language-reference/statements/select-case-statement.md) 可能会更有用。  
  
## 单行语法  
 可以将单行语法用于简短的测试。  但是，多行语法提供更多的结构和灵活性，并且通常更易于阅读、维护和调试。  
  
 `Then` 关键字后面是进行检查，以确定语句是否为单行 `If`。  如果同一行中的 `Then` 后面出现注释以外的任何其他内容，则该语句将被视为单行 `If` 语句。  如果 `Then` 不存在，则它必须是多行 `If`...`Then`...`Else` 的开头。  
  
 在单行语法中，可以作为 `If`...`Then` 判定的结果执行多条语句。  所有语句必须位于同一行上，并且由逗号分隔。  
  
## 示例  
 下面的示例阐释了 `If`...`Then`...`Else` 语句中多行语法的用法。  
  
 [!code-vb[VbVbalrStatements#101](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/if-then-else-statement_1.vb)]  
  
## 示例  
 下面的示例包含嵌套 `If`...`Then`...`Else` 语句。  
  
 [!code-vb[VbVbalrStatements#102](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/if-then-else-statement_2.vb)]  
  
## 示例  
 下面的示例阐述了单行语法的用法：  
  
 [!code-vb[VbVbalrStatements#103](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/if-then-else-statement_3.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Interaction.Choose%2A>   
 <xref:Microsoft.VisualBasic.Interaction.Switch%2A>   
 [\#If...Then...\#Else 指令](../../../visual-basic/language-reference/directives/if-then-else-directives.md)   
 [Select...Case 语句](../../../visual-basic/language-reference/statements/select-case-statement.md)   
 [嵌套的控件结构](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [决策结构](../../../visual-basic/programming-guide/language-features/control-flow/decision-structures.md)   
 [Visual Basic 中的逻辑运算符和位运算符](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)   
 [If 运算符](../../../visual-basic/language-reference/operators/if-operator.md)