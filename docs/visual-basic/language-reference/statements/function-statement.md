---
title: "函数语句 (Visual Basic) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Function
dev_langs:
- VB
helpviewer_keywords:
- procedures, creating
- Function procedures, Function statement syntax
- functions [Visual Basic], function procedures
- ParamArray keyword, Function statements
- Private keyword, Function statements
- declarations, procedures
- procedures, declaration
- Public keyword, in Function statement
- ByVal keyword, Function statements
- procedures, recursive
- Implements keyword, Function statements
- procedures, returning values
- Exit statement, in Function procedures
- recursive procedures
- As keyword, in Function statement
- Optional keyword, Function statements
- Function statement
- Visual Basic code, Function procedures
- procedures, function
- ByRef keyword, Function statements
- Friend keyword, Function statements
- End keyword, Function statements
- Handles keyword, Function statements
ms.assetid: a4497077-0f46-4ede-a27f-9e8670df52b9
caps.latest.revision: 62
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: af87477f81fab8406d726ebc8c81260b371d71c8
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="function-statement-visual-basic"></a>Function 语句 (Visual Basic)
声明名称、 参数和定义的代码`Function`过程。  
  
## <a name="syntax"></a>语法  
  
```  
[ <attributelist> ] [ accessmodifier ] [ proceduremodifiers ] [ Shared ] [ Shadows ] [ Async | Iterator ]  
Function name [ (Of typeparamlist) ] [ (parameterlist) ] [ As returntype ] [ Implements implementslist | Handles eventlist ]  
    [ statements ]  
    [ Exit Function ]  
    [ statements ]  
End Function  
```  
  
## <a name="parts"></a>部件  
  
-   `attributelist`  
  
     可选。 请参阅[属性列表](attribute-list.md)。  
  
-   `accessmodifier`  
  
     可选。 可以是以下各项之一：  
  
    -   [Public](../../../visual-basic/language-reference/modifiers/public.md)  
  
    -   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)  
  
    -   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)  
  
    -   [Private](../../../visual-basic/language-reference/modifiers/private.md)  
  
    -   `Protected Friend`  
  
     请参阅[访问 Visual Basic 中的级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
-   `proceduremodifiers`  
  
     可选。 可以是以下各项之一：  
  
    -   [重载](../../../visual-basic/language-reference/modifiers/overloads.md)  
  
    -   [Overrides](../../../visual-basic/language-reference/modifiers/overrides.md)  
  
    -   [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)  
  
    -   [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)  
  
    -   [MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)  
  
    -   `MustOverride Overrides`  
  
    -   `NotOverridable Overrides`  
  
-   `Shared`  
  
     可选。 请参阅[共享](../../../visual-basic/language-reference/modifiers/shared.md)。  
  
-   `Shadows`  
  
     可选。 请参阅[阴影](../../../visual-basic/language-reference/modifiers/shadows.md)。  
  
-   `Async`  
  
     可选。 请参阅[异步](../../../visual-basic/language-reference/modifiers/async.md)。  
  
-   `Iterator`  
  
     可选。 请参阅[迭代器](../../../visual-basic/language-reference/modifiers/iterator.md)。  
  
-   `name`  
  
     必需。 该过程的名称。 请参阅[声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
-   `typeparamlist`  
  
     可选。 针对泛型过程的类型参数的列表。 请参阅[键入列表](type-list.md)。  
  
-   `parameterlist`  
  
     可选。 表示此过程的参数的本地变量名称的列表。 请参阅[参数列表](parameter-list.md)。  
  
-   `returntype`  
  
     如果使用`Option Strict`是`On`。 此过程所返回的值的数据类型。  
  
-   `Implements`  
  
     可选。 指示此过程实现一个或多个`Function`过程，此过程包含类或结构实现的接口中定义每个组。 请参阅[实现语句](implements-statement.md)。  
  
-   `implementslist`  
  
     如果提供 `Implements`，则是必需的。 所实现的 `Function` 过程的列表。  
  
     `implementedprocedure [ , implementedprocedure ... ]`  
  
     每个 `implementedprocedure` 都具有以下语法和部件：  
  
     `interface.definedname`  
  
    |部件|说明|  
    |---|---|  
    |`interface`|必需。 此过程所实现的接口名称的包含类或结构。|  
    |`definedname`|必需。 在 `interface` 中用于定义过程的名称。|  
  
-   `Handles`  
  
     可选。 指示此过程可以处理一个或多个特定事件。 请参阅[处理](handles-clause.md)。  
  
-   `eventlist`  
  
     如果提供 `Handles`，则是必需的。 此过程处理的事件的列表。  
  
     `eventspecifier [ , eventspecifier ... ]`  
  
     每个 `eventspecifier` 都具有以下语法和部件：  
  
     `eventvariable.event`  
  
    |部件|说明|  
    |---|---|  
    |`eventvariable`|必需。 声明的类或结构，它将引发事件的数据类型的对象变量。|  
    |`event`|必需。 此过程处理的事件的名称。|  
  
-   `statements`  
  
     可选。 此过程中执行的语句块。  
  
-   `End Function`  
  
     终止此过程的定义。  
  
## <a name="remarks"></a>备注  
 在过程内必须是所有可执行代码。 反过来，每个过程，一个类、 结构或包含的类、 结构或模块称为一个模块中声明。  
  
 若要将值返回给调用代码，使用`Function`过程; 否则，请使用`Sub`过程。  
  
## <a name="defining-a-function"></a>定义函数  
 您可以定义`Function`仅在模块级别的过程。 因此，对于函数的声明上下文必须是一个类、 结构、 模块或接口，且不能为源文件、 命名空间、 过程或块。 有关详细信息，请参阅[声明上下文和默认访问级别](declaration-contexts-and-default-access-levels.md)。  
  
 `Function`过程默认为公共访问。 您可以调整它们的访问级别使用的访问修饰符。  
  
 一个`Function`过程可以声明该过程返回的值的数据类型。 您可以指定任何数据类型或枚举、 结构、 类或接口的名称。 如果没有指定`returntype`参数，则该过程返回`Object`。  
  
 如果此过程使用`Implements`关键字、 包含的类或结构还必须具有`Implements`紧跟在后面的语句及其`Class`或`Structure`语句。 `Implements`语句必须包含在指定的每个接口`implementslist`。 但是，通过该接口定义的名称`Function`(在`definedname`) 不需要此过程的名称匹配 (在`name`)。  
  
> [!NOTE]
>  可以使用 lambda 表达式来定义内联函数的表达式。 有关详细信息，请参阅[函数表达式](../../../visual-basic/language-reference/operators/function-expression.md)和[Lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)。  
  
## <a name="returning-from-a-function"></a>从函数返回  
 当`Function`过程返回到调用代码时，继续执行调用该过程的语句后面的语句。  
  
 若要从函数返回一个值，可以将该值赋给出函数名称，或将其包含在`Return`语句。  
  
 `Return`语句同时分配返回值，并退出函数，如以下示例所示。  
  
 [!code-vb[VbVbalrStatements #&24;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/function-statement_1.vb)]  
  
 下面的示例将返回值分配给函数名`myFunction`，然后使用`Exit Function`语句返回。  
  
 [!code-vb[VbVbalrStatements 第&23;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/function-statement_2.vb)]  
  
 `Exit Function`和`Return`语句会导致立即退出`Function`过程。 任意数量的`Exit Function`和`Return`语句可以在过程中，任何位置出现，并可混合`Exit Function`和`Return`语句。  
  
 如果您使用`Exit Function`而无需将值分配给`name`，该过程返回在指定的数据类型的默认值`returntype`。 如果`returntype`未指定，则该过程返回`Nothing`，这是默认值为`Object`。  
  
## <a name="calling-a-function"></a>调用函数  
 您调用`Function`过程的方法是使用过程名，跟在括号内，在表达式中的参数列表。 只有在不提供任何参数，可以省略括号。 但是，您的代码是始终包含括号更具可读性。  
  
 您调用`Function`过程相同的方式调用的任何库函数如`Sqrt`， `Cos`，或`ChrW`。  
  
 您还可以通过调用一个函数`Call`关键字。 在这种情况下，将忽略返回值。 利用`Call`关键字，则不建议在大多数情况下。 有关详细信息，请参阅[Call 语句](call-statement.md)。  
  
 Visual Basic 有时可以重新排列算术表达式来提高内部工作效率。 由于这个原因，不应使用`Function`算术表达式时该函数更改同一表达式中的变量的值中的过程。  
  
## <a name="async-functions"></a>异步函数  
 *异步*功能可用于调用异步函数而无需使用显式回调或手动将您的代码分拆跨多个函数或 lambda 表达式。  
  
 如果将标记与函数[异步](../../../visual-basic/language-reference/modifiers/async.md)修饰符，您可以使用[Await](../../../visual-basic/language-reference/operators/await-operator.md)函数中的运算符。 当控制达到`Await`中的表达式`Async`函数，控制权将返回给调用方，并且等待的任务完成之前一直于挂起在函数中的进度。 当任务完成后时，可在函数中恢复执行。  
  
> [!NOTE]
>  `Async`过程将返回给调用方时也遇到尚未完成，第一个 awaited 的对象或到达末尾`Async`过程中，无论哪个操作发生第一次。  
  
 `Async`函数可以具有返回类型为<xref:System.Threading.Tasks.Task%601>或<xref:System.Threading.Tasks.Task>.</xref:System.Threading.Tasks.Task> </xref:System.Threading.Tasks.Task%601> 举例说明如何`Async`函数的返回类型为<xref:System.Threading.Tasks.Task%601>下面提供了。</xref:System.Threading.Tasks.Task%601>  
  
 `Async`函数不能声明任何[ByRef](../../../visual-basic/language-reference/modifiers/byref.md)参数。  
  
 一个[Sub 语句](sub-statement.md)还可以使用标记`Async`修饰符。 这主要用于事件处理程序，不能返回一个值的位置。 `Async``Sub`过程不能处于等待状态，并且调用方的`Async``Sub`过程不能捕获所引发异常的`Sub`过程。  
  
 有关详细信息`Async`函数，请参见[使用 Async 和 Await 的异步编程](../../../visual-basic/programming-guide/concepts/async/index.md)，[异步程序中的控制流](../../../visual-basic/programming-guide/concepts/async/control-flow-in-async-programs.md)，和[异步返回类型](../../../visual-basic/programming-guide/concepts/async/async-return-types.md)。  
  
## <a name="iterator-functions"></a>迭代器函数  
 *迭代器*函数执行自定义迭代访问集合，如列表或数组。 迭代器函数使用[生成](yield-statement.md)语句可一次返回每个元素。 当[产生](yield-statement.md)到达语句，记住代码中的当前位置。 在下次调用迭代器函数将从该位置重新开始执行。  
  
 通过使用从客户端代码调用迭代器[为每个...下一步](for-each-next-statement.md)语句。  
  
 迭代器函数的返回类型可以是<xref:System.Collections.IEnumerable>， <xref:System.Collections.Generic.IEnumerable%601>， <xref:System.Collections.IEnumerator>，或<xref:System.Collections.Generic.IEnumerator%601>.</xref:System.Collections.Generic.IEnumerator%601> </xref:System.Collections.IEnumerator> </xref:System.Collections.Generic.IEnumerable%601> </xref:System.Collections.IEnumerable>  
  
 有关详细信息，请参阅[迭代器](http://msdn.microsoft.com/library/f45331db-d595-46ec-9142-551d3d1eb1a7)。  
  
## <a name="example"></a>示例  
 下面的示例使用`Function`语句来声明名称、 参数和窗体的主体的代码`Function`过程。 `ParamArray`修饰符将启用用于接受可变数量的参数的函数。  
  
 [!code-vb[VbVbalrStatements #&25;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/function-statement_3.vb)]  
  
## <a name="example"></a>示例  
 下面的示例调用在前面的示例声明的函数。  
  
 [!code-vb[VbVbalrStatements #&26;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/function-statement_4.vb)]  
  
## <a name="example"></a>示例  
 在下面的示例中，`DelayAsync`是`Async``Function`，其返回类型为<xref:System.Threading.Tasks.Task%601>。</xref:System.Threading.Tasks.Task%601> `DelayAsync` 具有返回整数的 `Return` 语句。 因此的函数声明`DelayAsync`需要具有返回类型的`Task(Of Integer)`。 因为返回类型为`Task(Of Integer)`，计算`Await`中的表达式`DoSomethingAsync`产生一个整数。 在此语句中对此进行了演示︰ `Dim result As Integer = Await delayTask`。  
  
 `startButton_Click`过程是一种`Async Sub`过程。 因为`DoSomethingAsync`是`Async`函数，以调用任务`DoSomethingAsync`必须等待，如下面的语句所示︰ `Await DoSomethingAsync()`。 `startButton_Click``Sub`过程必须定义与`Async`修饰符，因此`Await`表达式。  
  
 [!code-vb[csAsyncMethod&#1;](../../../csharp/programming-guide/classes-and-structs/codesnippet/VisualBasic/function-statement_5.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [Sub 语句](sub-statement.md)   
 [Function 过程](../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [参数列表](parameter-list.md)   
 [Dim 语句](dim-statement.md)   
 [Call 语句](call-statement.md)   
 [Of](of-clause.md)   
 [参数数组](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md)   
 [如何︰ 使用泛型类](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)   
 [故障排除过程](../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [Lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [函数表达式](../../../visual-basic/language-reference/operators/function-expression.md)

