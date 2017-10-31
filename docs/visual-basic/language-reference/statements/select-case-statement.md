---
title: "Select...Case 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Select"
  - "vb.Case"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "分支, conditional"
  - "Case Else 语句, Select...Case"
  - "Case 语句"
  - "Case 语句, Select...Case"
  - "条件语句, Select Case"
  - "控制流, 分支"
  - "Else 关键字 [Visual Basic], 在 Select...Case 语句中"
  - "End 关键字, Select Case 语句"
  - "执行, conditional"
  - "Is 运算符 [Visual Basic], 在 Select...Case 语句中"
  - "Select Case 语句, Select...Case"
  - "Select 语句"
  - "Select 语句, Select...Case"
  - "Select...Case 语句"
  - "To 关键字, 在 Select...Case 语句中"
ms.assetid: 68877b65-5419-4bf0-a465-20cd0e4c7d44
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Select...Case 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

根据表达式的值，运行若干组语句中的某一组。  
  
## 语法  
  
```  
Select [ Case ] testexpression  
    [ Case expressionlist  
        [ statements ] ]  
    [ Case Else  
        [ elsestatements ] ]  
End Select  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`testexpression`|必选。  表达式。  计算结果必须为某个基本数据类型（`Boolean`、`Byte`、`Char`、`Date`、`Double`、`Decimal`、`Integer`、`Long`、`Object`、`SByte`、`Short`、`Single`、`String`、`UInteger`、`ULong` 和 `UShort`）。|  
|`expressionlist`|在 `Case` 语句中是必选项。  代表 `testexpression` 匹配值的表达式子句的列表。  多个表达式子句以逗号隔开。  每个子句可以采取下面的某一种形式：<br /><br /> -   *表达式 1* `To` *表达式 2*<br />-   \[ `Is` \] *比较运算符**表达式*<br />-   *表达式*<br /><br /> 使用 `To` 关键字指定 `testexpression` 匹配值范围的边界。  `expression1` 的值必须小于或等于 `expression2` 的值。<br /><br /> 使用带比较运算符（`=`、`<>`、`<`、`<=`、`>` 或 `>=`）的 `Is` 关键字来指定对 `testexpression` 匹配值的限制。  如果没有提供 `Is` 关键字，则会自动将其插入到 *比较运算符* 之前。<br /><br /> 仅指定 `expression` 的格式将被视为 `Is` 格式的一种特殊情况，在此情况下，*比较运算符* 为等号 \(`=`\)。  此格式的计算方式为 `testexpression` \= `expression`。<br /><br /> `expressionlist` 中的表达式可以是任何数据类型，只要它们可被隐式地转换为 `testexpression` 的类型，而且适当的 `comparisonoperator` 对于与它一起使用的这两种类型均有效。|  
|`statements`|可选。  跟在 `Case` 后面的一个或多个语句，在以下情况下运行：`testexpression` 与 `expressionlist` 中的任何子句匹配。|  
|`elsestatements`|可选。  跟在 `Case Else` 后面的一个或多个语句，在以下情况下运行：`testexpression` 与任何 `Case` 语句的 `expressionlist` 中的任何子句不匹配。|  
|`End Select`|结束 `Select`...`Case` 构造的定义。|  
  
## 备注  
 如果 `testexpression` 与任何 `Case` `expressionlist` 子句匹配，跟在该 `Case` 语句后面的语句将运行，直至遇到下一个 `Case`、`Case Else` 或 `End Select` 语句。  然后将控制传递到 `End Select` 后面的语句。  如果 `testexpression` 与多个 `Case` 子句中的某个 `expressionlist` 子句匹配，则只有跟在第一个匹配子句后的语句才会运行。  
  
 `Case Else` 语句用于引入 `elsestatements`，以便在任何其他 `Case` 语句中的 `testexpression` 和 `expressionlist` 子句之间没有匹配项时运行。  最好让 `Select Case` 构造中的 `Case Else` 语句来处理无法预料的 `testexpression` 值，尽管这样做并不是必需的。  如果没有 `Case` `expressionlist` 子句与 `testexpression` 匹配，并且没有 `Case Else` 语句，控制权将会传递到跟在 `End Select` 后面的语句。  
  
 可以在每个 `Case` 子句中使用多个表达式或范围。  例如，下面的行是有效的。  
  
 `Case 1 To 4, 7 To 9, 11, 13, Is > maxNumber`  
  
> [!NOTE]
>  `Case` 和 `Case Else` 语句中使用的 `Is` 关键字与 [Is 运算符](../../../visual-basic/language-reference/operators/is-operator.md) 不同，后者用于对象引用比较。  
  
 可以针对字符串指定范围和多个表达式。  在下面的示例中，`Case` 匹配与“apples”完全相同的任何字符串，它有一个介于“nuts”和“soup”之间的值（按字母顺序），或包含与 `testItem` 的当前值完全相同的值。  
  
 `Case "apples", "nuts" To "soup", testItem`  
  
 `Option Compare` 的设置可能会影响字符串比较。  依据 `Option Compare Text` 进行比较，字符串“Apples”和“apples”相同，但依据 `Option Compare Binary` 进行比较，它们则不同。  
  
> [!NOTE]
>  具有多个子句的 `Case` 语句可能会表现出称为“短路”的行为。  Visual Basic 从左到右计算各个子句的值，如果某个子句生成了与 `testexpression` 匹配的值，则不会计算其余子句。  “短路”可以提高性能，但是，如果您希望计算 `expressionlist` 中每个表达式的值，可能会产生意外结果。  有关“短路”的更多信息，请参见 [布尔表达式](../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md)。  
  
 如果 `Case` 或 `Case Else` 语句块内的代码无需再运行该块中的任何其他语句，可以使用 `Exit Select` 语句退出该块。  这会将控制立即转交给 `End Select` 后面的语句。  
  
 `Select Case` 构造可相互嵌套。  每个嵌套的 `Select Case` 构造必须有匹配的 `End Select` 语句，并且完整包含在外部 `Select Case` 构造（它嵌套于其中）的单个 `Case` 或 `Case Else` 语句块内。  
  
## 示例  
 下面的示例使用 `Select Case` 构造写入与变量 `number` 的值相对应的行。  第二个 `Case` 语句包含与 `number` 的当前值匹配的值，因此，写入“Between 6 and 8, inclusive”的语句将运行。  
  
 [!code-vb[VbVbalrStatements#54](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/select-case-statement_1.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Interaction.Choose%2A>   
 [End 语句](../../../visual-basic/language-reference/statements/end-statement.md)   
 [If...Then...Else 语句](../../../visual-basic/language-reference/statements/if-then-else-statement.md)   
 [Option Compare 语句](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [Exit 语句](../../../visual-basic/language-reference/statements/exit-statement.md)