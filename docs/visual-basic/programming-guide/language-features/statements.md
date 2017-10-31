---
title: "在 Visual Basic 中的语句 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- variables [Visual Basic], declaring
- colons (:)
- constants, defining
- underlines
- constants, statements
- blue underline
- procedures, statements
- variables [Visual Basic], assigning
- line breaks, in code
- executable statements
- variables [Visual Basic], defining
- statements [Visual Basic], about statements
ms.assetid: fcfdee1a-82b7-4846-98f7-9ca3f5160089
caps.latest.revision: 30
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 001ea1cb5e651b95f808eefd47fd468f556550a1
ms.lasthandoff: 03/13/2017

---
# <a name="statements-in-visual-basic"></a>语句 (Visual Basic)
中的语句[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]是完整的指令。 它可以包含关键字、 运算符、 变量、 常量和表达式。 每个语句都属于以下类别之一︰  
  
-   **声明语句**，其中命名变量、 常量或过程中，并还可以指定一种数据类型。  
  
-   **可执行语句**，它启动操作。 这些语句可以调用方法或函数，并且它们可以循环或分支的代码块。 可执行语句包括**赋值语句**，它将一个值或表达式分配给变量或常数。  
  
 本主题介绍每个类别。 此外，本主题介绍如何结合使用多个语句在单独的行以及如何跨多行 continue 语句。  
  
## <a name="declaration-statements"></a>声明语句  
 使用声明语句命名和过程、 变量、 属性、 数组和常量定义。 在声明的编程元素时，您还可以定义其数据类型、 访问级别和作用域。 有关详细信息，请参阅[声明元素的特性](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)。  
  
 下面的示例包含三个声明。  
  
 [!code-vb[VbVbalrStatements #&80;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_1.vb)]  
  
 第一个声明是`Sub`语句。 以及与其匹配`End Sub`语句，它声明一个名为过程`applyFormat`。 它还指定`applyFormat`是`Public`，这意味着可以引用它的任何代码可以调用它。  
  
 第二个声明是`Const`语句，它声明了常量`limit`，并指定`Integer`数据类型和值为 33。  
  
 第三个声明是`Dim`语句声明变量`thisWidget`。 数据类型是否为特定对象，即从创建对象`Widget`类。 您可以声明一个变量以任何基本数据类型，或为在您使用的应用程序中公开任意对象类型。  
  
### <a name="initial-values"></a>初始值  
 包含声明语句的代码运行时，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]保留已声明的元素所需的内存。 如果该元素具有一个值，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]初始化为其数据类型的默认值。 详细信息，请参阅"行为"中[Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)。  
  
 您可以将初始值赋给一个变量，作为其声明的一部分，如下面的示例所示。  
  
 [!code-vb[VbVbalrStatements #&81;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_2.vb)]  
  
 如果某个变量为对象变量，您可以通过声明时地显式创建它的类的实例[New 运算符](../../../visual-basic/language-reference/operators/new-operator.md)关键字，如下面的示例阐释了。  
  
 [!code-vb[VbVbalrStatements #&82;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_3.vb)]  
  
 请注意直到执行变量的声明语句，在声明语句中指定的初始值未分配给一个变量。 到那时，该变量包含其数据类型的默认值。  
  
## <a name="executable-statements"></a>可执行语句  
 一个可执行语句执行的操作。 它可以调用的过程，在代码中，只需遍历多个语句的另一个位置的分支，或计算的表达式。 赋值语句是一种特殊情况的一个可执行语句。  
  
 下面的示例使用`If...Then...Else`控制结构来运行不同的变量的值所基于的代码块。 在代码中，每个块内`For...Next`循环运行指定的次数。  
  
 [!code-vb[VbVbalrStatements #&83;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_4.vb)]  
  
 `If`前面示例中的语句会检查参数值`clockwise`。 如果值为`True`，它将调用`spinClockwise`方法`aWidget`。 如果值为`False`，它将调用`spinCounterClockwise`方法`aWidget`。 `If...Then...Else`控制结构结尾`End If`。  
  
 `For...Next`循环内每个块将调用相应方法的次数的值相等`revolutions`参数。  
  
## <a name="assignment-statements"></a>赋值语句  
 赋值语句执行赋值操作，包括获取赋值运算符右侧的值 (`=`) 并将其存储在左侧，如以下示例所示的元素中。  
  
 [!code-vb[VbVbalrStatements #&73;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_5.vb)]  
  
 在前面的示例中，赋值语句将存储在变量中的文本值 42 `v`。  
  
### <a name="eligible-programming-elements"></a>合格的编程元素  
 赋值运算符左侧的编程元素必须能够接受和存储的值。 这意味着它必须是变量或属性不是[ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)，或者它必须是一个数组元素。 在赋值语句的上下文中，此类元素有时称为*左值*，为"左侧值"。  
  
 赋值运算符右侧的值生成的表达式，它可以由文本、 常量、 变量、 属性、 数组元素、 其他表达式或函数调用的任意组合组成。 下面的示例阐释了这一点。  
  
 [!code-vb[VbVbalrStatements #&74;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_6.vb)]  
  
 前面的示例将变量中保存的值`y`变量中保存的值为`z`，然后将添加对函数的调用返回的值`findResult`。 此表达式的总计值然后存储在变量`x`。  
  
### <a name="data-types-in-assignment-statements"></a>赋值语句中的数据类型  
 除了数值，赋值运算符还可以分配`String`值，如下面的示例所示。  
  
 [!code-vb[VbVbalrStatements #&75;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_7.vb)]  
  
 你还可以分配`Boolean`值，使用`Boolean`文字或`Boolean`表达式，如下面的示例将说明。  
  
 [!code-vb[VbVbalrStatements #&76;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_8.vb)]  
  
 同样，可以将适当的值分配给的编程元素`Char`， `Date`，或`Object`数据类型。 您还可以将对象实例分配给要从中创建该实例的类中声明的元素。  
  
### <a name="compound-assignment-statements"></a>复合赋值语句  
 *复合赋值语句*第一次对执行操作，然后再将它分配给编程元素的表达式。 下面的示例阐释了以下运算符之一`+=`，该运算符左侧变量的值由右侧表达式的值时都会增加。  
  
 [!code-vb[VbVbalrStatements #&77;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_9.vb)]  
  
 前面的示例中的值加上 1 `n`，然后将存储在该新值`n`。 它是一种速记等效的以下语句︰  
  
 [!code-vb[VbVbalrStatements #&78;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_10.vb)]  
  
 可以使用此类型的运算符执行多种不同的复合赋值操作。 这些运算符和有关它们的详细信息的列表，请参阅[赋值运算符](../../../visual-basic/language-reference/operators/assignment-operators.md)。  
  
 串联赋值运算符 (`&=`) 可用于将字符串添加到已存在的结束字符串，如下面的示例所示。  
  
 [!code-vb[VbVbalrStatements #&79;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_11.vb)]  
  
### <a name="type-conversions-in-assignment-statements"></a>赋值语句中的类型转换  
 将分配给变量、 属性或数组元素的值必须是相应于该目标元素的数据类型。 一般情况下，您应尝试生成相同的数据类型与目标元素的值。 但是，某些类型可以在分配过程转换为其他类型中。  
  
 有关数据类型之间进行转换的信息，请参阅[Visual Basic 中的类型转换](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)。 简单地说，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]会自动将给定类型的值转换为其扩大的任何其他类型。 一个*扩大转换*是一个中，始终在运行时成功，不会丢失任何数据。 例如，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将转换`Integer`值赋给`Double`在适当的时候，因为`Integer`加宽到`Double`。 有关详细信息，请参阅[扩大和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)。  
  
 *收缩转换*（那些不扩大） 执行的运行时，在发生故障或数据丢失的风险。 您可以通过使用类型转换函数，显式执行收缩转换，或者您可以直接将编译器能够通过设置隐式执行所有转换`Option Strict Off`。 有关详细信息，请参阅[隐式和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)。  
  
## <a name="putting-multiple-statements-on-one-line"></a>在一行上放置多个语句  
 在由冒号分隔的单个行中可以有多个语句 (`:`) 字符。 下面的示例阐释了这一点。  
  
 [!code-vb[VbVbalrStatements #&70;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_12.vb)]  
  
 虽然偶尔带来方便，因此这种形式的语法使代码更难以阅读和维护。 因此，建议您保留到行的一条语句。  
  
## <a name="continuing-a-statement-over-multiple-lines"></a>跨多行继续一条语句  
 语句通常会使在一行上，但太长时，您可以继续使用行继续符序列，其中包括空格后跟一个下划线字符在下一行 (`_`) 后跟回车符。 在下面的示例中，`MsgBox`可执行的语句将继续在两个行。  
  
 [!code-vb[VbVbalrStatements #&71;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_13.vb)]  
  
### <a name="implicit-line-continuation"></a>隐式行继续符  
 在许多情况下，可以在下一步的后续行继续一条语句，而无需使用下划线字符 (_)。 下表列出了隐式在下一行代码 continue 语句的语法元素。  
  
|语法元素|示例|  
|---|---|  
|在逗号之后 (`,`)。|[!code-vb[VbVbalrLineContinuation #&1;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_14.vb)]|  
|在左括号之后 (`(`) 或右括号之前 (`)`)。|[!code-vb[VbVbalrLineContinuation #&2;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_15.vb)]|  
|在左大括号之后 (`{`) 或右大括号之前 (`}`)。|[!code-vb[VbVbalrLineContinuation #&3;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_16.vb)]<br /><br /> 有关详细信息，请参阅[对象初始值设定项︰ 命名类型和匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)或[集合初始值设定项](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)。|  
|在打开后嵌入式表达式 (`<%=`) 或嵌入式表达式结束之前 (`%>`) 在 XML 文本内。|[!code-vb[VbVbalrLineContinuation #&4;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_17.vb)]<br /><br /> 有关详细信息，请参阅[XML 中的嵌入式表达式](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)。|  
|串联运算符之后 (`&`)。|[!code-vb[VbVbcnConventions #&9;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_18.vb)]<br /><br /> 有关详细信息，请参阅[按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)。|  
|After assignment operators (`=`, `&=`, `:=`, `+=`, `-=`, `*=`, `/=`, `\=`, `^=`, `<<=`, `>>=`).|[!code-vb[VbVbalrLineContinuation #&5;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_19.vb)]<br /><br /> 有关详细信息，请参阅[按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)。|  
|After binary operators (`+`, `-`, `/`, `*`, `Mod`, `<>`, `<`, `>`, `<=`, `>=`, `^`, `>>`, `<<`, `And`, `AndAlso`, `Or`, `OrElse`, `Like`, `Xor`) within an expression.|[!code-vb[VbVbalrLineContinuation #&7;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_20.vb)]<br /><br /> 有关详细信息，请参阅[按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)。|  
|之后`Is`和`IsNot`运算符。|[!code-vb[VbVbalrLineContinuation #&8;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_21.vb)]<br /><br /> 有关详细信息，请参阅[按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)。|  
|在成员限定符后 (`.`) 和成员名称的前面。 但是，您必须包含成员限定符字符后面的使用时的行继续符字符 (_)`With`语句或在一种类型的初始化列表中提供值。 请考虑使用赋值运算符之后换行 (例如， `=`) 正在使用时`With`语句或对象初始化列表。|[!code-vb[VbVbalrLineContinuation #&5;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_19.vb)]<br />[!code-vb[VbVbalrLineContinuation #&14;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_22.vb)]<br /><br /> 有关详细信息，请参阅[与...使用语句结束](../../../visual-basic/language-reference/statements/with-end-with-statement.md)或[对象初始值设定项︰ 命名类型和匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)。|  
|XML 轴属性限定符后 (`.`或`.@`或`...`)。 但是，必须包括行继续符字符 (_)，当您在使用时指定成员限定符`With`关键字。|[!code-vb[VbVbalrLineContinuation #&9;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_23.vb)]<br /><br /> 有关详细信息，请参阅[XML 轴属性](../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)。|  
|在小于-号 (<) or="" before="" a="" greater-than="" sign=""></)>`>`) 时指定的属性。 此外后大于-号 (`>`) 时指定的属性。 但是，您必须包含行继续符字符 (_) 时，可以指定程序集级别或模块级别的属性。|[!code-vb[VbVbalrLineContinuation #&10;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_24.vb)]<br /><br /> 有关详细信息，请参阅[属性概述](../../../visual-basic/programming-guide/concepts/attributes/index.md)。|  
|Before and after query operators (`Aggregate`, `Distinct`, `From`, `Group By`, `Group Join`, `Join`, `Let`, `Order By`, `Select`, `Skip`, `Skip While`, `Take`, `Take While`, `Where`, `In`, `Into`, `On`, `Ascending`, and `Descending`). 您不能之间换行组成的多个关键字的查询运算符的关键字 (`Order By`， `Group Join`， `Take While`，和`Skip While`)。|[!code-vb[VbVbalrLineContinuation #&11;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_25.vb)]<br /><br /> 有关详细信息，请参阅[查询](../../../visual-basic/language-reference/queries/queries.md)。|  
|之后`In`中的关键字`For Each`语句。|[!code-vb[VbVbalrLineContinuation #&12;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_26.vb)]<br /><br /> 有关详细信息，请参阅[为每个...下一条语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md)。|  
|之后`From`集合初始值设定项中的关键字。|[!code-vb[VbVbalrLineContinuation #&13;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/statements_27.vb)]<br /><br /> 有关详细信息，请参阅[集合初始值设定项](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)。|  
  
## <a name="adding-comments"></a>添加注释  
 源代码并不总是很容易理解，甚至对程序员而言。 为了帮助说明其代码，因此，大多数程序员请自由使用嵌入的注释。 一个过程或特定指令的读取或更高版本使用它的任何人都可以解释代码中的注释。 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]在编译期间，将忽略注释不会影响已编译的代码。  
  
 注释行开头的撇号 (`'`) 或`REM`跟一个空格。 可以将他们添加任何地方在代码中，除字符串中。 若要将注释附加到一条语句，插入一个撇号或`REM`之后的语句，后面添加注释。 注释还可以在自己单独的行上。 下面的示例演示这些可能性。  
  
 [!code-vb[VbVbalrStatements #&72;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/statements_28.vb)]  
  
## <a name="checking-compilation-errors"></a>检查编译错误  
 如果键入的代码行后，该行显示有蓝色波浪下划线 （也会出现一条错误消息），则语句中有语法错误。 您必须找出错误的语句 （通过查看在任务列表中，或将鼠标悬停在带有鼠标指针的错误以及阅读的错误消息） 并更正它。 直到已修复代码中的所有语法错误，程序将无法正确编译。  
  
## <a name="related-sections"></a>相关章节  
  
|术语|定义|  
|---|---|  
|[赋值运算符](../../../visual-basic/language-reference/operators/assignment-operators.md)|提供一些主题的链接，如涉及赋值运算符的语言参考页`=`， `*=`，和`&=`。|  
|[运算符和表达式](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)|演示如何组合元素和运算符以生成新值。|  
|[如何：在代码中拆分和合并语句](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)|演示如何拆分为多行的一条语句以及如何在同一行上放置多个语句。|  
|[如何：标记语句](../../../visual-basic/programming-guide/program-structure/how-to-label-statements.md)|演示如何标记代码行。|
