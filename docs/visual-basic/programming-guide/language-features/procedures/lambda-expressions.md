---
title: "Lambda 表达式 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.LambdaFunction
dev_langs:
- VB
helpviewer_keywords:
- functions [Visual Basic], lambda expressions
- lambda expressions [Visual Basic]
- expressions [Visual Basic], lambda
- inline functions [Visual Basic]
ms.assetid: 137064b0-3928-4bfa-ba71-c3f9cbd951e2
caps.latest.revision: 52
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
ms.openlocfilehash: e50593e76afecfe8807c3cb5bac479245d2feaef
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="lambda-expressions-visual-basic"></a>Lambda 表达式 (Visual Basic)
一个*lambda 表达式*是没有程序可以委托有效的任何地方使用的名称的函数或子例程。 Lambda 表达式可以是函数或子例程，可以为单行或多行。 可以将值从当前作用域传递到 lambda 表达式中。  
  
> [!NOTE]
>  `RemoveHandler`语句是一个例外。 不能将传递的委托参数的 lambda 表达式中`RemoveHandler`。  
  
 使用创建 lambda 表达式`Function`或`Sub`关键字，就像创建标准函数或子例程。 但是，lambda 表达式包含在一个语句。  
  
 下面的示例是递增其参数并返回的值的 lambda 表达式。 该示例同时显示的单行和多行 lambda 表达式语法的函数。  
  
 [!code-vb[VbVbalrLambdas #&14;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_1.vb)]  
  
 下面的示例是一个向控制台写入一个值的 lambda 表达式。 该示例显示一个子例程这两个单行和多行 lambda 表达式语法。  
  
 [!code-vb[VbVbalrLambdas #&15;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_2.vb)]  
  
 请注意，前面示例中的 lambda 表达式分配给变量的名称。 只要您引用该变量，则调用 lambda 表达式。 您还可以声明并调用 lambda 表达式在同一时间，如下面的示例中所示。  
  
 [!code-vb[VbVbalrLambdas #&3;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_3.vb)]  
  
 Lambda 表达式可以返回作为函数调用的值 (如示例中所示[上下文](#context)在本主题后面的部分)，或作为参数传递给参数接受一个委托类型，如下面的示例中所示。  
  
 [!code-vb[VbVbalrLambdas #&8;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_4.vb)]  
  
## <a name="lambda-expression-syntax"></a>Lambda 表达式语法  
 Lambda 表达式的语法类似于标准函数或子例程。 区别，如下所示如下︰  
  
-   Lambda 表达式不具有一个名称。  
  
-   Lambda 表达式不能具有修饰符，如`Overloads`或`Overrides`。  
  
-   单行 lambda 函数不使用`As`子句指定返回类型。 相反，该类型是从推断 lambda 表达式的主体的计算结果为的值。 例如，如果 lambda 表达式的主体是`cust.City = "London"`，其返回类型是`Boolean`。  
  
-   在多行 lambda 函数中，您可以指定返回类型使用`As`子句，或忽略`As`子句以便推断返回类型。 当`As`子句被省略对于多行 lambda 函数、 返回类型推断为从所有的主要类型`Return`多行 lambda 函数中的语句。 *主导类型*是所有其他类型都可以扩大到的唯一类型。 如果无法确定此唯一类型，主导类型是数组中的所有其他类型可以收缩到的唯一类型。 如果无法确定为这两种唯一类型之一，则基准类型是 `Object`。 在这种情况下，如果`Option Strict`设置为`On`，会发生编译错误。  
  
     例如，如果表达式提供给`Return`语句包含类型的值`Integer`， `Long`，和`Double`，得到的数组的类型是`Double`。 同时`Integer`和`Long`扩大到`Double`和仅`Double`。 因此， `Double` 是基准类型。 有关详细信息，请参阅[扩大和收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)。  
  
-   单行函数的主体必须是一个表达式，返回一个值，而不是语句。 有没有`Return`单行函数的语句。 单行函数返回的值是表达式的函数的正文中的值。  
  
-   单行子例程的主体必须是单行语句。  
  
-   不包括的单行函数和子例程`End Function`或`End Sub`语句。  
  
-   可以通过指定 lambda 表达式参数的数据类型`As`可以推断关键字或该参数的数据类型。 必须必须推断数据类型或所有已经指定所有参数。  
  
-   `Optional`和`Paramarray`不允许使用参数。  
  
-   不允许泛型参数。  
  
## <a name="async-lambdas"></a>异步 lambda  
 您可以轻松创建 lambda 表达式和语句通过使用包含异步处理[异步](../../../../visual-basic/language-reference/modifiers/async.md)和[Await 运算符](../../../../visual-basic/language-reference/operators/await-operator.md)关键字。 例如，下面的 Windows 窗体示例包含一个调用和等待异步方法 `ExampleMethodAsync`的事件处理程序。  
  
```vb  
Public Class Form1  
  
    Async Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click  
        ' ExampleMethodAsync returns a Task.  
        Await ExampleMethodAsync()  
        TextBox1.Text = vbCrLf & "Control returned to button1_Click."  
    End Sub  
  
    Async Function ExampleMethodAsync() As Task  
        ' The following line simulates a task-returning asynchronous process.  
        Await Task.Delay(1000)  
    End Function  
  
End Class  
```  
  
 可以通过使用在异步 lambda 添加同一事件处理程序[AddHandler 语句](../../../../visual-basic/language-reference/statements/addhandler-statement.md)。 若要添加此处理程序，请在 lambda 参数列表前添加一个 `Async` 修饰符，如下例所示。  
  
```vb  
Public Class Form1  
  
    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load  
        AddHandler Button1.Click,   
            Async Sub(sender1, e1)  
                ' ExampleMethodAsync returns a Task.  
                Await ExampleMethodAsync()  
                TextBox1.Text = vbCrLf & "Control returned to Button1_ Click."  
            End Sub  
    End Sub  
  
    Async Function ExampleMethodAsync() As Task  
        ' The following line simulates a task-returning asynchronous process.  
        Await Task.Delay(1000)  
    End Function  
  
End Class  
```  
  
 有关如何创建和使用异步方法的详细信息，请参阅[使用 Async 和 Await 的异步编程](../../../../visual-basic/programming-guide/concepts/async/index.md)。  
  
##  <a name="context"></a>上下文  
 Lambda 表达式与在其中定义的范围共享其上下文。 它具有相同的访问权限，在编写包含作用域中的任何代码。 这包括对成员变量、 函数和子例程，访问`Me`，以及参数和包含作用域中的局部变量。  
  
 包含作用域中的局部变量和参数的访问可以超出该范围的生存期。 只要引用 lambda 表达式的委托不能进行垃圾回收，就将保留与原始环境中的变量的访问。 在以下示例中，变量`target`本地`makeTheGame`的方法的 lambda 表达式`playTheGame`定义。 请注意，返回的 lambda 表达式中，分配给`takeAGuess`中`Main`，仍有权访问本地变量`target`。  
  
 [!code-vb[VbVbalrLambdas #&12;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_5.vb)]  
  
 下面的示例演示了广泛的嵌套的 lambda 表达式的访问权限。 返回的 lambda 表达式中的执行时`Main`作为`aDel`，它能够访问下列元素︰  
  
-   在其中定义的类的字段︰`aField`  
  
-   在其中定义的类的属性︰`aProp`  
  
-   方法的一个参数`functionWithNestedLambda`，在其中定义︰`level1`  
  
-   本地变量`functionWithNestedLambda`:`localVar`  
  
-   在其中嵌套 lambda 表达式的参数︰`level2`  
  
 [!code-vb[VbVbalrLambdas #&9;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_6.vb)]  
  
## <a name="converting-to-a-delegate-type"></a>将转换为委托类型  
 Lambda 表达式可以隐式转换为兼容的委托类型。 有关兼容性的常规要求的信息，请参阅[宽松委托转换](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)。 例如，下面的代码示例显示了 lambda 表达式隐式转换为`Func(Of Integer, Boolean)`或匹配委托签名。  
  
 [!code-vb[VbVbalrLambdas #&16;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_7.vb)]  
  
 下面的代码示例显示了 lambda 表达式隐式转换为`Sub(Of Double, String, Double)`或匹配委托签名。  
  
 [!code-vb[VbVbalrLambdas 第&23;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_8.vb)]  
  
 当将 lambda 表达式分配给的代理，或将它们作为参数传递给过程时，您可以指定参数名称，但省略其数据类型，以便从委托中获取的类型。  
  
## <a name="examples"></a>示例  
  
-   下面的示例定义返回的 lambda 表达式`True`如果可以为 null 的参数已被赋值，和`False`如果其值为`Nothing`。  
  
     [!code-vb[VbVbalrLambdas #&4;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_9.vb)]  
  
-   下面的示例定义返回数组中的最后一个元素的索引的 lambda 表达式。  
  
     [!code-vb[VbVbalrLambdas #&5;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/lambda-expressions_10.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [在 Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [委托](../../../../visual-basic/programming-guide/language-features/delegates/index.md)   
 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [可以为 null 的值类型](../../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)   
 [如何︰ 将过程传递给在 Visual Basic 中的另一个过程](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)   
 [如何︰ 创建 Lambda 表达式](./how-to-create-a-lambda-expression.md)   
 [宽松委托转换](../../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)

