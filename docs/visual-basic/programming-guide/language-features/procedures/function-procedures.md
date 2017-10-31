---
title: "函数过程 (Visual Basic 中) |Microsoft 文档"
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
- Function procedures
- return values, function procedures
- Visual Basic code, procedures
- procedures, calling
- procedures, Function procedures
- syntax, function procedures
ms.assetid: 1b9f632c-553b-4cb6-920a-ded117ead8c0
caps.latest.revision: 27
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 11baaa6985f0681aa9c67c4f2470fb9917db5b78
ms.lasthandoff: 03/13/2017

---
# <a name="function-procedures-visual-basic"></a>Function 过程 (Visual Basic)
一个`Function`过程是一系列[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]语句括`Function`和`End Function`语句。 `Function`过程执行一项任务，再将控制权返回给调用代码。 当此方法返回控制时，它还向调用代码返回一个值。  
  
 每次调用该过程时，运行时，其语句开头的第一个可执行语句后`Function`语句，并与第一个结束`End Function`， `Exit Function`，或`Return`遇到的语句。  
  
 您可以定义`Function`模块、 类或结构中的过程。 它是`Public`默认情况下，这意味着可以从任何位置调用在有权访问模块、 类或结构定义它的应用程序中。  
  
 一个`Function`过程可以采用参数，如常量、 变量或表达式，通过调用代码传递给它。  
  
## <a name="declaration-syntax"></a>声明语法  
 声明的语法`Function`过程是，如下所示︰  
  
```vb  
[Modifiers] Function FunctionName [(ParameterList)] As ReturnType  
    [Statements]  
End Function  
```  
  
 *修饰符*可以指定访问级别和重载、 重写、 共享和隐藏有关的信息。 有关详细信息，请参阅[Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)。  
  
 声明每个参数相同的方式相似， [Sub 过程](./sub-procedures.md)。  
  
### <a name="data-type"></a>数据类型  
 每个`Function`过程具有一种数据类型，只需为每个变量一样。 此数据类型由指定`As`中的子句`Function`语句，并且它确定该函数将返回到调用代码的值的数据类型。 下面的示例声明说明这一点。  
  
```vb  
Function yesterday() As Date  
End Function  
  
Function findSqrt(ByVal radicand As Single) As Single  
End Function  
```  
  
 有关详细信息，请参阅"部件" [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)。  
  
## <a name="returning-values"></a>返回值  
 值`Function`过程将发送回调用代码调用它的返回值。 此过程返回此值在两种方式之一︰  
  
-   它使用`Return`语句来指定返回值，并返回给调用程序立即控制。 下面的示例阐释了这一点。  
  
```vb  
Function FunctionName [(ParameterList)] As ReturnType  
    ' The following statement immediately transfers control back  
    ' to the calling code and returns the value of Expression.  
    Return Expression  
End Function  
```  
  
-   它将值分配给其自己的函数名称在一个或多个语句中的过程。 控制不返回给调用程序直到`Exit Function`或`End Function`执行语句。 下面的示例阐释了这一点。  
  
```vb  
Function FunctionName [(ParameterList)] As ReturnType  
    ' The following statement does not transfer control back to the calling code.  
    FunctionName = Expression  
    ' When control returns to the calling code, Expression is the return value.  
End Function  
```  
  
 返回值分配给函数名的优点是，控件才会返回过程中遇到`Exit Function`或`End Function`语句。 这样，您可以分配一个初步的值和更高版本调整，如有必要。  
  
 有关返回值的详细信息，请参阅[Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)。 有关返回数组的信息，请参阅[数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md)。  
  
## <a name="calling-syntax"></a>调用语法  
 您可以调用`Function`过程的方法是将其名称和参数放在赋值语句或表达式中的右侧。 您必须提供值的所有参数，不是可选的并且必须将参数列表括在括号中。 如果未不提供任何参数，可以选择省略括号。  
  
 对的调用语法`Function`过程是，如下所示︰  
  
 *左值*`=`*functionname* `[(` *argumentlist*    `)]`  
  
 `If ((`*functionname* `[(` *argumentlist* `)] / 3) <=`*表达式*  `) Then`  
  
 当您调用`Function`的过程中，您无需使用其返回值。 如果不这样做，将执行的函数的所有操作，但将忽略返回值。 <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>通常会调用这种方式。</xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>  
  
### <a name="illustration-of-declaration-and-call"></a>声明和调用的插图  
 以下`Function`过程计算的最长边或斜边直角三角形而言，给定的其他两个方面。  
  
 [!code-vb[VbVbcnProcedures #&1;](./codesnippet/VisualBasic/function-procedures_1.vb)]  
  
 下面的示例演示如何调用典型`hypotenuse`。  
  
 [!code-vb[VbVbcnProcedures #&6;](./codesnippet/VisualBasic/function-procedures_2.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [Sub 过程](./sub-procedures.md)   
 [属性过程](./property-procedures.md)   
 [运算符过程](./operator-procedures.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [如何︰ 创建返回一个值的过程](./how-to-create-a-procedure-that-returns-a-value.md)   
 [如何︰ 从过程返回值](./how-to-return-a-value-from-a-procedure.md)   
 [如何：调用返回值的过程](./how-to-call-a-procedure-that-returns-a-value.md)
