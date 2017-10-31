---
title: "如何︰ 执行表达式树 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 9dfb5ab3-f48f-417e-975f-f8f6f1cdc18d
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e12c45b417310f097d597561b2652ee793a4b2c0
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-execute-expression-trees-visual-basic"></a>如何︰ 执行表达式树 (Visual Basic)
本主题演示如何执行表达式树。 执行表达式树可能会返回一个值，或者它可能只需执行的操作，例如调用方法。  
  
 可以执行仅表示 lambda 表达式的表达式树。 表示 lambda 表达式的表达式目录树是类型<xref:System.Linq.Expressions.LambdaExpression>或<xref:System.Linq.Expressions.Expression%601>.</xref:System.Linq.Expressions.Expression%601> </xref:System.Linq.Expressions.LambdaExpression> 若要执行这些表达式树，调用<xref:System.Linq.Expressions.LambdaExpression.Compile%2A>方法来创建一个可执行的委托，然后调用该委托。</xref:System.Linq.Expressions.LambdaExpression.Compile%2A>  
  
> [!NOTE]
>  如果不知道该委托的类型，即 lambda 表达式是类型<xref:System.Linq.Expressions.LambdaExpression>和 not <xref:System.Linq.Expressions.Expression%601>，必须调用<xref:System.Delegate.DynamicInvoke%2A>上而不是直接调用委托方法。</xref:System.Delegate.DynamicInvoke%2A> </xref:System.Linq.Expressions.Expression%601> </xref:System.Linq.Expressions.LambdaExpression>  
  
 如果表达式目录树不表示 lambda 表达式，可以创建一个新的 lambda 表达式作为其主体具有原始表达式目录树，通过调用<xref:System.Linq.Expressions.Expression.Lambda%60%601%28System.Linq.Expressions.Expression%2CSystem.Collections.Generic.IEnumerable%7BSystem.Linq.Expressions.ParameterExpression%7D%29>方法。</xref:System.Linq.Expressions.Expression.Lambda%60%601%28System.Linq.Expressions.Expression%2CSystem.Collections.Generic.IEnumerable%7BSystem.Linq.Expressions.ParameterExpression%7D%29> 然后，可以执行 lambda 表达式，如本节前面所述。  
  
## <a name="example"></a>示例  
 下面的代码示例演示如何执行表达式树表示数字的幂︰ 创建 lambda 表达式，然后执行它。 结果，它表示为数字幂的次幂，将显示。  
  
```vb  
' The expression tree to execute.  
Dim be As BinaryExpression = Expression.Power(Expression.Constant(2.0R), Expression.Constant(3.0R))  
  
' Create a lambda expression.  
Dim le As Expression(Of Func(Of Double)) = Expression.Lambda(Of Func(Of Double))(be)  
  
' Compile the lambda expression.  
Dim compiledExpression As Func(Of Double) = le.Compile()  
  
' Execute the lambda expression.  
Dim result As Double = compiledExpression()  
  
' Display the result.  
MsgBox(result)  
  
' This code produces the following output:  
' 8  
```  
  
## <a name="compiling-the-code"></a>编译代码  
  
-   如果未引用将添加对 System.Core.dll 的项目引用。  
  
-   包括 System.Linq.Expressions 命名空间。  
  
## <a name="see-also"></a>另请参阅  
 [表达式树 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/index.md)   
 [如何︰ 修改表达式树 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/how-to-modify-expression-trees.md)
