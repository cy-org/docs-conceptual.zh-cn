---
title: "While...End While 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.While"
  - "vb.While...EndWhile"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "While 语句"
  - "While 语句, While...End While"
  - "While...End While 语句"
ms.assetid: b931d1ce-e8ed-44d8-a13d-92a4f5458a1e
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# While...End While 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

只要给定条件为 `True` 就运行一系列语句。  
  
## 语法  
  
```  
While condition  
    [ statements ]  
    [ Continue While ]  
    [ statements ]  
    [ Exit While ]  
    [ statements ]  
End While  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`condition`|必需。  `Boolean` 表达式。  如果 `condition` 为 `Nothing`，Visual Basic 会将其视为 `False`。|  
|`statements`|可选。  跟在 `While` 后面的一个或多个语句，这些语句将在每次 `condition` 为 `True` 时运行。|  
|`Continue While`|可选。  为 `While` 的下一次迭代传输控件块。|  
|`Exit While`|可选。  将控制权传送到 `While` 块外部。|  
|`End While`|必需。  结束 `While` 块的定义。|  
  
## 备注  
 如果要重复一组语句无限次数，请使用 `While...End While` 结构，只要条件一直为 `True`。  如果想要更灵活地选择在何处测试条件以及针对什么结果进行测试，您可能宁愿使用 [Do...Loop 语句](../../../visual-basic/language-reference/statements/do-loop-statement.md)。  如果想要重复语句一定次数，则 [For...Next 语句](../../../visual-basic/language-reference/statements/for-next-statement.md) 通常是较好的选择。  
  
> [!NOTE]
>  `While` 关键字还在 [Do...Loop 语句](../../../visual-basic/language-reference/statements/do-loop-statement.md)、[Skip While 子句](../../../visual-basic/language-reference/queries/skip-while-clause.md) 和 [Take While 子句](../../../visual-basic/language-reference/queries/take-while-clause.md) 中使用。  
  
 如果 `condition` 为 `True`，则所有 `statements` 将运行，直至遇到 `End While` 语句。  然后控件回 `While` 语句，并且，`condition` 再次检查。  如果 `condition` 仍为 `True`，则重复上面的过程。  如果是 `False`，控件传递给遵循 `End While` 条语句。  
  
 在启动循环之前，`While` 语句始终检查该条件。  在条件一直为 `True` 时循环会继续下去。  如果 `condition` 是 `False`，在首次进入循环时，它甚至一次不会运行。  
  
 `condition` 通常由两个值的比较，但是，它可以是计算结果为 [Boolean 数据类型](../../../visual-basic/language-reference/data-types/boolean-data-type.md) 值的表达式\(`True` 或 `False`\)。  此表达式可以包含其他数据类型的值，如数值类型，被转换为 `Boolean`。  
  
 可以将一个循环放在另一个循环内以嵌套 `While` 循环。  您还可以将多个不同类型的控制结构嵌套在一个结构中。  有关更多信息，请参见 [嵌套的控件结构](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)。  
  
## 退出，while  
 [退出，while](../../../visual-basic/language-reference/statements/exit-statement.md) 语句可以提供了另一种 `While` 退出循环。  立即`Exit While` 到遵循 `End While` 条语句传输控件。  
  
 通常使用 `Exit While`，在某些条件计算后\(例如，在 `If...Then...Else` 结构\)。  如果检测到使继续迭代不必要或不可能的条件（如错误值或终止请求），则可能需要退出循环。  可以使用 `Exit While`，则测试可能会导致无限 *循环*，该循环可以运行非常甚至无限次数的条件时。  然后可以使用 `Exit While` 退出循环。  
  
 可以在 `While` 循环的任意位置放置任意数量的 `Exit While` 语句。  
  
 当在嵌套的 `While` 循环内使用时，`Exit While` 会将控制权转移出最内层的循环，并交给下一层级别较高的嵌套。  
  
 对于循环的下一次迭代的直接 `Continue While` 语句发送控件。  有关更多信息，请参见 [Continue 语句](../../../visual-basic/language-reference/statements/continue-statement.md)。  
  
## 示例  
 在下面的示例中，循环中的语句继续运行，直到 `index` 变量大于 10。  
  
 [!code-vb[VbVbalrStatements#171](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/while-end-while-statement_1.vb)]  
  
## 示例  
 下面的示例阐释了 `Continue While` and `Exit While` 语句的用法。  
  
 [!code-vb[VbVbalrStatements#172](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/while-end-while-statement_2.vb)]  
  
## 示例  
 下面的示例读取文本文件中的所有行。  <xref:System.IO.File.OpenText%2A> 方法打开文件，并返回读取字符的 <xref:System.IO.StreamReader>。  在 `While` 情况，`StreamReader` 的 <xref:System.IO.StreamReader.Peek%2A> 方法确定文件是否包含其他字符。  
  
 [!code-vb[VbVbalrStatements#173](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/while-end-while-statement_3.vb)]  
  
## 请参阅  
 [循环结构](../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [Do...Loop 语句](../../../visual-basic/language-reference/statements/do-loop-statement.md)   
 [For...Next 语句](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [Boolean 数据类型](../../../visual-basic/language-reference/data-types/boolean-data-type.md)   
 [嵌套的控件结构](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Exit 语句](../../../visual-basic/language-reference/statements/exit-statement.md)   
 [Continue 语句](../../../visual-basic/language-reference/statements/continue-statement.md)