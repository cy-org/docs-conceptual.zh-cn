---
title: "Operator 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.operator"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "CType 函数, Operator 语句"
  - "Narrowing 关键字, 转换运算符"
  - "运算符重载"
  - "运算符过程"
  - "Operator 语句"
  - "运算符 [Visual Basic]"
  - "运算符 [Visual Basic], 重载"
  - "重载运算符"
  - "过程, operator"
  - "语法, 运算符过程"
  - "Visual Basic 代码, 运算符"
  - "Widening 关键字, 转换运算符"
ms.assetid: b12ec4af-1ad7-4a17-865b-c5ee96320ae5
caps.latest.revision: 28
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 28
---
# Operator 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

声明在类或结构上定义运算符过程的运算符符号、操作数和代码。  
  
## 语法  
  
```  
[ <attrlist> ] Public [ Overloads ] Shared [ Shadows ] [ Widening | Narrowing ]   
Operator operatorsymbol ( operand1 [, operand2 ]) [ As [ <attrlist> ] type ]  
    [ statements ]  
    [ statements ]  
    Return returnvalue  
    [ statements ]  
End Operator  
```  
  
## 部件  
 `attrlist`  
 可选。  请参见[特性列表](../../../visual-basic/language-reference/statements/attribute-list.md)。  
  
 `Public`  
 必选。  指明此运算符过程具有 [Public](../../../visual-basic/language-reference/modifiers/public.md) 访问权。  
  
 `Overloads`  
 可选。  请参见 [Overloads](../../../visual-basic/language-reference/modifiers/overloads.md)。  
  
 `Shared`  
 必选。  指明此运算符过程是 [Shared](../../../visual-basic/language-reference/modifiers/shared.md) 过程。  
  
 `Shadows`  
 可选。  请参见 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)。  
  
 `Widening`  
 除非指定 `Narrowing`，否则对于转换运算符是必需的。  指明此运算符过程定义 [Widening](../../../visual-basic/language-reference/modifiers/widening.md) 转换。  请参见此“帮助”页上的“扩大转换和收缩转换”。  
  
 `Narrowing`  
 除非指定 `Widening`，否则对于转换运算符是必需的。  指明此运算符过程定义 [Narrowing](../../../visual-basic/language-reference/modifiers/narrowing.md) 转换。  请参见此“帮助”页上的“扩大转换和收缩转换”。  
  
 `operatorsymbol`  
 必选。  此运算符过程所定义运算符的符号或标识符。  
  
 `operand1`  
 必选。  一元运算符（包括转换运算符）的单一操作数或者二元运算符的左操作数的名称和类型。  
  
 `operand2`  
 对于二元运算符是必需的。  二元运算符的右操作数的名称和类型。  
  
 `operand1` 和 `operand2` 具有以下语法和部分：  
  
 `[ ByVal ] operandname [ As operandtype ]`  
  
|组成部分|说明|  
|----------|--------|  
|`ByVal`|可选项，但传递机制必须为 [ByVal](../../../visual-basic/language-reference/modifiers/byval.md)。|  
|`operandname`|必选。  表示此操作数的变量的名称。  请参见 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。|  
|`operandtype`|除非 `Option Strict` 设置为 `On`，否则是可选项。  此操作数的数据类型。|  
  
 `type`  
 除非 `Option Strict` 设置为 `On`，否则是可选项。  运算符过程所返回值的数据类型。  
  
 `statements`  
 可选。  运算符过程运行的语句块。  
  
 `returnvalue`  
 必选。  运算符过程返回到调用代码的值。  
  
 `End` `Operator`  
 必选。  结束此运算符过程的定义。  
  
## 备注  
 只能在类或结构中使用 `Operator`。  这意味着，运算符的声明上下文不能是源文件、命名空间、模块、接口、过程或块。  有关更多信息，请参见[声明上下文和默认访问级别](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)。  
  
 所有运算符均必须为 `Public Shared`。  不能为任何一个操作数指定 `ByRef`、`Optional` 或 `ParamArray`。  
  
 不能使用运算符符号或标识符来保存返回值。  必须使用 `Return` 语句，并且它必须指定一个值。  在过程内的任何位置都可以出现任意数目的 `Return` 语句。  
  
 通过这种方式定义运算符的过程称为运算符重载，不管您是否使用了 `Overloads` 关键字。  下表列出了您可以定义的运算符。  
  
|类型|运算符|  
|--------|---------|  
|一元|`+`, `-`, `IsFalse`, `IsTrue`, `Not`|  
|Binary|`+`, `-`, `*`, `/`, `\`, `&`, `^`, `>>`, `<<`, `=`, `<>`, `>`, `>=`, `<`, `<=`, `And`, `Like`, `Mod`, `Or`, `Xor`|  
|转换（一元）|`CType`|  
  
 请注意，二元列表中的 `=` 运算符是比较运算符，而不是赋值运算符。  
  
 在定义 `CType` 时，必须指定 `Widening` 或 `Narrowing`。  
  
## 匹配对  
 必须将某些运算符定义为匹配对。  如果定义了此类匹配对的任一个运算符，就必须同时定义另一个。  匹配对如下所示：  
  
-   `=` 和 `<>`  
  
-   `>` 和 `<`  
  
-   `>=` 和 `<=`  
  
-   `IsTrue` 和 `IsFalse`  
  
## 数据类型限制  
 您定义的每个运算符都必须与您在其上定义该运算符的类或结构密切相关。  这意味着，该类或结构必须作为以下各项的数据类型出现：  
  
-   一元运算符的操作数。  
  
-   二元运算符的至少一个操作数。  
  
-   转换运算符的操作数或返回类型。  
  
 某些运算符还有额外的数据类型限制，如下所示：  
  
-   如果定义 `IsTrue` 和 `IsFalse` 运算符，它们必须都返回 `Boolean` 类型。  
  
-   如果定义 `<<` 和 `>>` 运算符，它们必须都为 `operand2` 的 `operandtype` 指定 `Integer` 类型。  
  
 返回类型不必与任何一个操作数的类型对应。  例如，即使两个操作数都不是 `Boolean`，`=` 或 `<>` 等比较运算符也可能返回 `Boolean`。  
  
## 逻辑运算符和位运算符  
 `And`、`Or`、`Not` 和 `Xor` 运算符可在 Visual Basic 中执行逻辑运算或按位运算。  但是，如果在类或结构上定义这些运算符之一，则只能定义它的按位运算。  
  
 不能使用 `Operator` 语句直接定义 `AndAlso` 运算符。  但是，如果满足了以下条件，则可以使用 `AndAlso`：  
  
-   您已在想要用于 `AndAlso` 的同一操作数类型上定义了 `And`。  
  
-   `And` 的定义返回的类型与您已在其上定义了该运算符的类或结构的类型相同。  
  
-   在已在其上定义了 `And` 的类或结构上，您已定义了 `IsFalse` 运算符。  
  
 同样，如果您已使用类或结构的返回类型在相同操作数上定义了 `Or`，并且已在类或结构上定义了 `IsTrue`，则可以使用 `OrElse`。  
  
## 扩大转换和收缩转换  
 扩大转换在运行时总是会成功，而收缩转换在运行时则可能会失败。  有关更多信息，请参见[扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)。  
  
 如果将转换过程声明为 `Widening`，则过程代码一定不会产生任何错误。  这意味着：  
  
-   它必须始终返回类型为 `type` 的有效值。  
  
-   它必须处理所有可能的异常及其他错误条件。  
  
-   它必须处理从它调用的任何过程中返回的任何错误。  
  
 只要有任何可能转换过程也许会不成功，或者它可能会导致未经处理的异常，您就必须将其声明为 `Narrowing`。  
  
## 示例  
 下面的代码示例使用 `Operator` 语句定义一个结构大纲，其中包括 `And`、`Or`、`IsFalse` 和 `IsTrue` 运算符的运算符过程。  `And` 和 `Or` 每个都采用两个类型为 `abc` 的操作数，并返回类型 `abc`。  `IsFalse` 和 `IsTrue` 每个都采用类型为 `abc` 的单一操作数，并返回 `Boolean`。  这些定义允许调用代码通过 `abc` 类型的操作数来使用 `And`、`AndAlso`、`Or` 和 `OrElse`。  
  
 [!code-vb[VbVbalrStatements#44](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/operator-statement_1.vb)]  
  
## 请参阅  
 [IsFalse 运算符](../../../visual-basic/language-reference/operators/isfalse-operator.md)   
 [IsTrue 运算符](../../../visual-basic/language-reference/operators/istrue-operator.md)   
 [Widening](../../../visual-basic/language-reference/modifiers/widening.md)   
 [Narrowing](../../../visual-basic/language-reference/modifiers/narrowing.md)   
 [扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [如何：定义运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [如何：定义转换运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [如何：调用运算符过程](../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-operator-procedure.md)   
 [如何：使用定义运算符的类](../../../visual-basic/programming-guide/language-features/procedures/how-to-use-a-class-that-defines-operators.md)