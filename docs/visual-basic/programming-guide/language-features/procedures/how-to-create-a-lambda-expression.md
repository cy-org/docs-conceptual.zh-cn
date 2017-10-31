---
title: "如何︰ 创建 Lambda 表达式 (Visual Basic 中) |Microsoft 文档"
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
- lambda expressions [Visual Basic]
- expressions [Visual Basic], lambda
ms.assetid: 3279bd5c-80f7-410a-a7ba-f7085ed36aa5
caps.latest.revision: 27
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
ms.openlocfilehash: 5e105e87b1e63218f2c3c2204350257c139b5837
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-a-lambda-expression-visual-basic"></a>如何：创建 Lambda 表达式 (Visual Basic)
一个*lambda 表达式*是函数或不具有名称的子例程。 委托类型有效的任何地方，则可以使用 lambda 表达式。  
  
### <a name="to-create-a-single-line-lambda-expression-function"></a>若要创建的单行 lambda 表达式函数  
  
1.  在任何情况下，可以使用一种委托类型的位置，键入关键字`Function`，下面的示例所示︰  
  
     `Dim add1 =`   `Function`  
  
2.  在括号内，紧靠`Function`，键入函数的参数。 请注意不指定后的名称`Function`。  
  
     `Dim add1 = Function`   `(num As Integer)`  
  
3.  以下参数列表中，作为该函数的正文中键入一个表达式。 表达式计算结果的值是由函数返回的值。 不使用`As`子句指定返回类型。  
  
     [!code-vb[VbVbalrLambdas #&1;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_1.vb)]  
  
     Lambda 表达式通过调用传入一个整数参数。  
  
     [!code-vb[VbVbalrLambdas #&2;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_2.vb)]  
  
4.  或者，相同的结果被通过下面的示例︰  
  
     [!code-vb[VbVbalrLambdas #&3;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_3.vb)]  
  
### <a name="to-create-a-single-line-lambda-expression-subroutine"></a>若要创建的单行 lambda 表达式子例程  
  
1.  在任何情况下，可以使用一种委托类型的位置，键入关键字`Sub`，如在下面的示例所示。  
  
     `Dim add1 =`   `Sub`  
  
2.  在括号内，紧靠`Sub`，键入该子例程的参数。 请注意不指定后的名称`Sub`。  
  
     `Dim add1 = Sub`   `(msg As String)`  
  
3.  以下参数列表中，键入作为该子例程的正文的单个语句。  
  
     [!code-vb[VbVbalrLambdas #&17;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_4.vb)]  
  
     Lambda 表达式通过调用传入一个字符串参数。  
  
     [!code-vb[VbVbalrLambdas #&18;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_5.vb)]  
  
### <a name="to-create-a-multiline-lambda-expression-function"></a>若要创建多行 lambda 表达式函数  
  
1.  在任何情况下，可以使用一种委托类型的位置，键入关键字`Function`，如在下面的示例所示。  
  
     `Dim add1 =`   `Function`  
  
2.  在括号内，紧靠`Function`，键入函数的参数。 请注意不指定后的名称`Function`。  
  
     `Dim add1 = Function`   `(index As Integer)`  
  
3.  按 Enter。 `End Function`语句会自动添加。  
  
4.  该函数体内，添加以下代码以创建一个表达式，返回的值。 不使用`As`子句指定返回类型。  
  
     [!code-vb[VbVbalrLambdas #&19;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_6.vb)]  
  
     Lambda 表达式通过调用传入一个整数参数。  
  
     [!code-vb[VbVbalrLambdas #&20;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_7.vb)]  
  
### <a name="to-create-a-multiline-lambda-expression-subroutine"></a>若要创建多行 lambda 表达式子例程  
  
1.  在任何情况下，可以使用一种委托类型的位置，键入关键字`Sub`，如在下面的示例所示︰  
  
     `Dim add1 =`   `Sub`  
  
2.  在括号内，紧靠`Sub`，键入该子例程的参数。 请注意不指定后的名称`Sub`。  
  
     `Dim add1 = Sub`  `(msg As String)`  
  
3.  按 Enter。 `End Sub`语句会自动添加。  
  
4.  该函数体内，添加以下代码以调用该子例程时应执行。  
  
     [!code-vb[VbVbalrLambdas #&21;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_8.vb)]  
  
     Lambda 表达式通过调用传入一个字符串参数。  
  
     [!code-vb[VbVbalrLambdas #&22;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_9.vb)]  
  
## <a name="example"></a>示例  
 Lambda 表达式的常见用途是定义一个函数，它可以作为参数的类型的参数中传递`Delegate`。 在下面的示例中，<xref:System.Diagnostics.Process.GetProcesses%2A>方法返回在本地计算机上运行的进程的数组。</xref:System.Diagnostics.Process.GetProcesses%2A> <xref:System.Linq.Enumerable.Where%2A>方法从<xref:System.Linq.Enumerable>类需要`Boolean`委托作为其参数。</xref:System.Linq.Enumerable> </xref:System.Linq.Enumerable.Where%2A> 该示例中的 lambda 表达式用于此目的。 它将返回`True`的每个进程，只有一个线程，并且初始屏幕中选择`filteredList`。  
  
 [!code-vb[VbVbalrLambdas #&10;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_10.vb)]  
  
 上一个示例是等效于下面的代码中编写[!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)]语法︰  
  
 [!code-vb[VbVbalrLambdas #&11;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-create-a-lambda-expression_11.vb)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Linq.Enumerable></xref:System.Linq.Enumerable>   
 [Lambda 表达式](./lambda-expressions.md)   
 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub 语句](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [委托](../../../../visual-basic/programming-guide/language-features/delegates/index.md)   
 [如何︰ 将过程传递给在 Visual Basic 中的另一个过程](../../../../visual-basic/programming-guide/language-features/delegates/how-to-pass-procedures-to-another-procedure.md)   
 [Delegate 语句](../../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [在 Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
