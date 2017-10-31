---
title: "For...Next 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Step"
  - "vb.Next"
  - "vb.To"
  - "vb.for"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "无限循环"
  - "Next 关键字, For...Next 语句"
  - "For 关键字 [Visual Basic], For...Next 语句"
  - "Step 关键字, For...Next 语句"
  - "运算符重载, For...Next 语句"
  - "To 关键字, For...Next 语句"
  - "无限循环"
  - "循环, 无限"
  - "指令, 重复"
  - "Next 语句, For...Next"
  - "For...Next 语句"
  - "循环结构, For...Next"
  - "循环, 无限"
  - "Exit 语句, For...Next 语句"
  - "For 语句"
ms.assetid: f5fc0d51-67ce-4c36-9f09-31c9a91c94e9
caps.latest.revision: 64
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 64
---
# For...Next 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

将一组语句重复执行指定的次数。  
  
## 语法  
  
```  
For counter [ As datatype ] = start To end [ Step step ]  
    [ statements ]  
    [ Continue For ]  
    [ statements ]  
    [ Exit For ]  
    [ statements ]  
Next [ counter ]  
```  
  
## 部件  
  
|组成部分|描述|  
|----------|--------|  
|`counter`|`For` 语句的必选项。  数值变量。  它是循环的控制变量。  有关更多信息，请参见本主题后面的[计数器参数](#BKMK_Counter)。|  
|`datatype`|可选。  `counter` 的数据类型。  有关更多信息，请参见本主题后面的[计数器参数](#BKMK_Counter)。|  
|`start`|必需。  数值表达式。  `counter` 的初始值。|  
|`end`|必需。  数值表达式。  `counter` 的最终值。|  
|`step`|可选。  数值表达式。  每次循环后 `counter` 的增量。|  
|`statements`|可选。  放在 `For` 和 `Next` 之间的一条或多条语句，它们将运行指定的次数。|  
|`Continue For`|可选。  将控制权交给下一轮循环迭代。|  
|`Exit For`|可选。  将控制转移到 `For` 循环外。|  
|`Next`|必需。  结束 `For` 循环的定义。|  
  
> [!NOTE]
>  `To` 关键字用于此语句。计数器指定大小。  还可以使用此关键字在 [Select...Case 语句](../../../visual-basic/language-reference/statements/select-case-statement.md) 和在数组声明。  有关数组声明的更多信息，请参见 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)。  
  
## 简单示例  
 如果要重复组语句设定的次数时，可以使用一 `For`…`Next` 结构。  
  
 在下面的示例中，`index` 变量从值为 1 开始并提高与循环的每次迭代，关闭，在 `index` 达到 5. 后的值。  
  
 [!code-vb[VbVbalrStatements#111](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-next-statement_1.vb)]  
  
 在下面的示例中，`number` 变量从 2 开始和减小 0.25 在每次循环迭代，关闭，在 `number` 达到 0 后的值。  `-.25` 的 `Step` 参数减少该值按 0.25 在每次循环迭代。  
  
 [!code-vb[VbVbalrStatements#112](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-next-statement_2.vb)]  
  
> [!TIP]
>  [While...End While 语句](../../../visual-basic/language-reference/statements/while-end-while-statement.md) 或 [Do...Loop 语句](../../../visual-basic/language-reference/statements/do-loop-statement.md) 适用，当您事先不知道多少次运行在循环中的语句。  但是，如果您希望让循环运行特定次数，则 `For`...`Next` 是较好的选择。  您需要在第一次输入循环时确定迭代次数。  
  
## 嵌套循环  
 可以将一个循环放在另一个循环内以嵌套 `For` 循环。  下面的示例演示了具有不同步长值的 `For`...`Next` 嵌套结构。  外部循环为每次循环迭代创建一个字符串。  内部循环减小每次循环迭代的循环计数器变量。  
  
 [!code-vb[VbVbalrStatements#113](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-next-statement_3.vb)]  
  
 如果嵌套循环时，每个循环必须具有唯一 `counter` 变量。  
  
 您还可以将多个不同类型的控制结构相互进行嵌套。  有关更多信息，请参见[嵌套的控件结构](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)。  
  
## 退出并继续为  
 `Exit For` 语句立即退出 `For`…`Next` 循环和将控件传输到遵循 `Next` 条语句。  
  
 `Continue For` 语句将控制权立即转移给下一轮循环。  有关更多信息，请参见[Continue 语句](../../../visual-basic/language-reference/statements/continue-statement.md)。  
  
 下面的示例阐释了 `Continue For` and `Exit For` 语句的用法。  
  
 [!code-vb[VbVbalrStatements#115](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-next-statement_4.vb)]  
  
 可以在 `For`…`Next` 循环中放置任意数量的 `Exit For` 语句。  当在嵌套的 `For`…`Next` 循环内使用时，`Exit For` 将退出最内层的循环，并将控制权交给下一层较高级别的嵌套。  
  
 `Exit For` 是通常，在计算某种情况后 \(例如，在 `If`…`Then`…`Else` 结构\)。  您可能希望针对下列条件使用 `Exit For`：  
  
-   继续循环不必要或不可能。  一个不正确的值或停止请求可创建此条件。  
  
-   `Try`…`Catch`…`Finally` 语句捕捉异常。  可以在 `Finally` 块的末尾使用 `Exit For`。  
  
-   有无限循环，该循环可以运行甚至不用次数。  如果检测到这样的条件，就可以使用 `Exit For` 退出循环。  有关更多信息，请参见[Do...Loop 语句](../../../visual-basic/language-reference/statements/do-loop-statement.md)。  
  
## 技术实现  
 当 `For`...`Next` 循环开始时，Visual Basic 将计算 `start`、`end` 和 `step`。  Visual Basic 目前仅计算这些值然后将 `start` 到 `counter`。  在语句块运行，Visual Basic 与 `end`之前比较 `counter`。  如果 `counter` 大于 `end` 值已为 \(或更小，如果 `step` 为负\)，`For` 循环结束，并且控制传递到遵循 `Next` 条语句。  否则，该语句块运行。  
  
 每次 Visual Basic 遇到 `Next` 语句时，都按 `step` 递增 `counter`，然后返回到 `For` 语句。  它再次将 `counter` 与 `end` 进行比较，并再次根据结果运行块或者退出循环。  这一过程将一直持续下去，直到 `counter` 传递 `end` 或者遇到 `Exit For` 语句为止。  
  
 循环不会停止，直到 `counter` 已通过 `end`。  如果 `counter` 等于 `end`，则循环继续。  如果 `step` 为正数，确定是否运行循环代码块的比较运算将为 `counter` \<\= `end`；如果 `step` 为负数，则为 `counter` \>\= `end`。  
  
 如果更改 `counter` 的值，在循环内时，您的代码可能会难以阅读和调试。  更改 `start`的值，`end`或 `step` 不影响确定的迭代值，当循环先输入了。  
  
 如果嵌套循环，编译器发出错误信号，如果它在内部级别的 `Next` 语句之前遇到了外部嵌套级别的 `Next` 语句。  不过，仅当在所有 `Next` 语句中都指定了 `counter` 时，编译器才能检测到这种重叠错误。  
  
### 步骤参数  
 `step` 的值可以是正数或负数。  此参数确定处理根据下表中的循环：  
  
|**Step 值**|**循环执行的条件**|  
|----------------|-----------------|  
|正数或零|`counter` \<\= `end`|  
|负数|`counter` \>\= `end`|  
  
 `step` 的默认值为 1。  
  
###  <a name="BKMK_Counter"></a> 计数器参数  
 下表指示 `counter` 是否定义了作用于整个 `For…Next` 循环的一个新的局部变量。  此确定依赖 `datatype` 是否存在，并 `counter` 是否已经定义。  
  
|`datatype` 是否存在？|`counter` 已定义？|结果 \( `counter` 是否定义了作用于整个 `For...Next` 循环\) 的新局部变量|  
|----------------------|--------------------|---------------------------------------------------------|  
|否|是|不，因为 `counter` 已定义。  如果范围 `counter` 不是本地传递给过程，编译时警告发生。|  
|否|否|是的。  数据类型。`start`、`end`和 `step` 表达式推断。  有关类型推断的信息，请参见 [Option Infer 语句](../../../visual-basic/language-reference/statements/option-infer-statement.md) 和 [局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)。|  
|是|是|是，但，只有 \+ 当现有 `counter` 变量在过程外定义。  该变量保留单独的。  如果现有 `counter` 变量的范围是本地传递给过程，将产生编译时错误。|  
|是|否|是的。|  
  
 `counter` 的数据类型确定迭代的类型，必须为下列类型之一：  
  
-   `Byte`、`SByte`、`UShort`、`Short`、`UInteger`、`Integer`、`ULong`、`Long`、`Decimal`、`Single` 或 `Double`。  
  
-   您使用 [Enum 语句](../../../visual-basic/language-reference/statements/enum-statement.md) 声明的枚举。  
  
-   一个 `Object`。  
  
-   具有下列运算符的 `T`，其中 `B` 是可以在 `Boolean` 表达式中使用的类型。  
  
     `Public Shared Operator >= (op1 As T, op2 As T) As B`  
  
     `Public Shared Operator <= (op1 As T, op2 As T) As B`  
  
     `Public Shared Operator - (op1 As T, op2 As T) As T`  
  
     `Public Shared Operator + (op1 As T, op2 As T) As T`  
  
 在 `Next` 语句可以选择指定 `counter` 变量。  尤其是如果嵌套 `For` 循环，此语法以提高程序的可读性。  您必须指定出现在相应的 `For` 语句中的变量。  
  
 `start`、`end` 和 `step` 表达式可以计算为拓宽到 `counter` 类型的任何数据类型。  如果为 `counter`使用用户定义的类型时，您可能必须定义 `CType` 转换运算符将 `start`、`end`或 `step` 的类型转换为 `counter`的类型。  
  
## 示例  
 下面的示例从泛型列表中删除所有元素。  而不是 [For Each...Next 语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md)，该示例显示按降序重复一个 `For`…`Next` 语句。  因为 `removeAt` 方法将移除的元素后面使元素具有较小索引值，该示例使用此方法。  
  
 [!code-vb[VbVbalrStatements#114](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-next-statement_5.vb)]  
  
## 示例  
 下面的示例通过使用 [Enum 语句](../../../visual-basic/language-reference/statements/enum-statement.md)，声明的循环访问枚举。  
  
 [!code-vb[VbVbalrStatements#116](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-next-statement_6.vb)]  
  
## 示例  
 在下面的示例中，语句参数使用了具有 `+`、 `-`、`>=` 和 `<=` 运算符的运算符重载的类。  
  
 [!code-vb[VbVbalrStatements#117](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-next-statement_7.vb)]  
  
## 请参阅  
 <xref:System.Collections.Generic.List%601>   
 [循环结构](../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [While...End While 语句](../../../visual-basic/language-reference/statements/while-end-while-statement.md)   
 [Do...Loop 语句](../../../visual-basic/language-reference/statements/do-loop-statement.md)   
 [嵌套的控件结构](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Exit 语句](../../../visual-basic/language-reference/statements/exit-statement.md)   
 [集合](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md)