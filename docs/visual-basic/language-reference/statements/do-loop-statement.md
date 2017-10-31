---
title: "Do...Loop 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Do"
  - "vb.Loop"
  - "vb.Until"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "条件语句, Do...Loop"
  - "Do 循环"
  - "Do 语句"
  - "Do...Loop 语句"
  - "do-while 语句"
  - "执行, 条件"
  - "Exit 语句, 在 Do...Loop 语句中"
  - "指令, 重复"
  - "Loop 关键字, Do...Loop 语句"
  - "循环结构, Do...Loop 语句"
  - "循环, 退出"
  - "Until 关键字, Do...Loop 语句"
  - "while 语句, Do...Loop"
ms.assetid: 892f9096-b3e2-4aee-834d-83bc4e2c379d
caps.latest.revision: 37
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 37
---
# Do...Loop 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

当某个 `Boolean` 条件为 `True` 时，或在该条件变为 `True` 之前，重复执行某个语句块。  
  
## 语法  
  
```  
Do { While | Until } condition  
    [ statements ]  
    [ Continue Do ]  
    [ statements ]  
    [ Exit Do ]  
    [ statements ]  
Loop  
-or-  
Do  
    [ statements ]  
    [ Continue Do ]  
    [ statements ]  
    [ Exit Do ]  
    [ statements ]  
Loop { While | Until } condition  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`Do`|必需。  开始 `Do` 循环的定义。|  
|`While`|必选项（除非使用了 `Until`）。  重复执行循环，直到 `condition` 为 `False`。|  
|`Until`|必选项（除非使用了 `While`）。  重复执行循环，直到 `condition` 为 `True`。|  
|`condition`|可选。  `Boolean` 表达式。  如果 `condition` 为 `Nothing`，Visual Basic 会将其视为 `False`。|  
|`statements`|可选。  一条或多条语句，它们在 `condition` 为 `True` 时或变为 True 之前重复执行。|  
|`Continue Do`|可选。  为 `Do` 循环的下一次迭代传输控件。|  
|`Exit Do`|可选。  将控制传送到 `Do` 循环外。|  
|`Loop`|必需。  终止 `Do` 循环的定义。|  
  
## 备注  
 如果想重复执行一组语句不定的次数，直到满足了某个条件为止，则可使用 `Do...Loop` 结构。  如果想重复执行语句既定的次数，则 [For...Next 语句](../../../visual-basic/language-reference/statements/for-next-statement.md)通常是更好的选择。  
  
 可以使用 `While` 或 `Until` 来指定 `condition`，但不能同时使用两个。  
  
 只能在循环的开头或结尾测试一次 `condition`。  如果在循环的开头（在 `Do` 语句中）测试 `condition`，则循环可能从不会运行一次。  如果在循环的结尾（在 `Loop` 语句中）进行测试，则循环总会至少运行一次。  
  
 条件通常通过两个值的比较得到，但也可以是任何计算为 [Boolean 数据类型](../../../visual-basic/language-reference/data-types/boolean-data-type.md) 值（`True` 或 `False`）的表达式。  这包括已转换为 `Boolean` 的其他数据类型（如数字类型）的值。  
  
 可以将一个循环放在另一个循环内以嵌套 `Do` 循环。  您还可以将多个不同类型的控制结构相互进行嵌套。  有关更多信息，请参见 [嵌套的控件结构](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)。  
  
> [!NOTE]
>  `Do...Loop` 结构在灵活性上比 [While...End While 语句](../../../visual-basic/language-reference/statements/while-end-while-statement.md) 更强，这是因为，它可让您在 `condition` 停止为 `True` 或初次变为 `True` 时决定是否结束循环。  它还可让您在循环的开头或结尾测试 `condition`。  
  
## Exit Do  
 [Exit Do](../../../visual-basic/language-reference/statements/exit-statement.md) 语句可以提供退出 `Do…Loop` 的备选方式。  `Exit Do` 将控制立即转移到 `Loop` 语句后面的语句。  
  
 `Exit Do` 通常在计算特定条件后使用，例如在 `If...Then...Else` 结构中。  如果检测到使继续迭代不必要或不可能的条件（如错误值或终止请求），则可能需要退出循环。  `Exit Do` 的一种用途是测试能够导致无限循环（即运行次数多甚至无限的循环）的条件。  可以使用 `Exit Do` 来退出循环。  
  
 可以在 `Do…Loop` 的任意位置包括任意数量的 `Exit Do` 语句。  
  
 当在嵌套的 `Do` 循环内使用时，`Exit Do` 会将控制权转移出最内层的循环，并交给下一层级别较高的嵌套。  
  
## 示例  
 在下面的示例中，循环中的语句继续运行，直到 `index` 变量大于 10。  `Until` 子句在循环的末尾。  
  
 [!code-vb[VbVbalrStatements#131](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/do-loop-statement_1.vb)]  
  
## 示例  
 下面的示例使用 `While` 子句，而不是 `Until` 子句，并在循环开始处（而非结束处）测试 `condition`。  
  
 [!code-vb[VbVbalrStatements#132](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/do-loop-statement_2.vb)]  
  
## 示例  
 在下面的示例中，当 `index` 变量大于100 时，`condition` 将停止循环。  但是，循环中的 `If` 语句在索引变量大于 10 时将导致 `Exit Do` 语句停止循环。  
  
 [!code-vb[VbVbalrStatements#133](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/do-loop-statement_3.vb)]  
  
## 示例  
 下面的示例读取文本文件中的所有行。  <xref:System.IO.File.OpenText%2A> 方法打开文件，并返回读取字符的 <xref:System.IO.StreamReader>。  在 `Do...Loop` 条件中，`StreamReader` 的 <xref:System.IO.StreamReader.Peek%2A> 方法确定是否存在任何额外的字符。  
  
 [!code-vb[VbVbalrStatements#134](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/do-loop-statement_4.vb)]  
  
## 请参阅  
 [循环结构](../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [For...Next 语句](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [Boolean 数据类型](../../../visual-basic/language-reference/data-types/boolean-data-type.md)   
 [嵌套的控件结构](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Exit 语句](../../../visual-basic/language-reference/statements/exit-statement.md)   
 [While...End While 语句](../../../visual-basic/language-reference/statements/while-end-while-statement.md)