---
title: "如何︰ 修改表达式树 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: d1309fff-28bd-4d8e-a2cf-75725999e8f2
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
ms.openlocfilehash: fb4e818eed7d6547e091c914d40b3ce87af59512
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-modify-expression-trees-visual-basic"></a>如何︰ 修改表达式树 (Visual Basic)
本主题演示如何修改某个表达式树。 表达式树是不可变的这意味着它们不能直接修改。 若要更改表达式目录树，必须创建一份现有表达式树，并在创建该副本，进行必要的更改。 您可以使用<xref:System.Linq.Expressions.ExpressionVisitor>类遍历现有表达式树，并复制它访问的每个节点。</xref:System.Linq.Expressions.ExpressionVisitor>  
  
### <a name="to-modify-an-expression-tree"></a>若要修改某个表达式树  
  
1.  创建一个新**控制台应用程序**项目。  
  
2.  添加`Imports`语句的文件与`System.Linq.Expressions`命名空间。  
  
3.  添加`AndAlsoModifier`类传递给您的项目。  
  
    ```vb  
    Public Class AndAlsoModifier  
        Inherits ExpressionVisitor  
  
        Public Function Modify(ByVal expr As Expression) As Expression  
            Return Visit(expr)  
        End Function  
  
        Protected Overrides Function VisitBinary(ByVal b As BinaryExpression) As Expression  
            If b.NodeType = ExpressionType.AndAlso Then  
                Dim left = Me.Visit(b.Left)  
                Dim right = Me.Visit(b.Right)  
  
                ' Make this binary expression an OrElse operation instead   
                ' of an AndAlso operation.  
                Return Expression.MakeBinary(ExpressionType.OrElse, left, right, _  
                                             b.IsLiftedToNull, b.Method)  
            End If  
  
            Return MyBase.VisitBinary(b)  
        End Function  
    End Class  
    ```  
  
     此类继承<xref:System.Linq.Expressions.ExpressionVisitor>类，专用于修改表示条件的表达式`AND`operations。</xref:System.Linq.Expressions.ExpressionVisitor> 它将从条件更改这些操作`AND`为条件`OR`。 若要这样做，类将重写<xref:System.Linq.Expressions.ExpressionVisitor.VisitBinary%2A>方法是基类型，因为条件`AND`表达式表示为二进制表达式。</xref:System.Linq.Expressions.ExpressionVisitor.VisitBinary%2A> 在`VisitBinary`方法时，如果传递给它的表达式表示条件`AND`操作，该代码构造一个新的表达式包含条件`OR`运算符而不是在条件`AND`运算符。 如果传递给该表达式`VisitBinary`不表示条件`AND`操作，该方法交由基类实现。 就像在中，传递的表达式目录树的构造节点但这些节点将它们替换为表达式树的子树将基类方法生成以递归方式访问者。  
  
4.  添加`Imports`语句的文件与`System.Linq.Expressions`命名空间。  
  
5.  将代码添加到`Main`Module1.vb 文件创建一个表达式树并将其传递给该方法的方法中将对其进行修改。  
  
    ```vb  
    Dim expr As Expression(Of Func(Of String, Boolean)) = _  
        Function(name) name.Length > 10 AndAlso name.StartsWith("G")  
  
    Console.WriteLine(expr)  
  
    Dim modifier As New AndAlsoModifier()  
    Dim modifiedExpr = modifier.Modify(CType(expr, Expression))  
  
    Console.WriteLine(modifiedExpr)  
  
    ' This code produces the following output:  
    ' name => ((name.Length > 10) && name.StartsWith("G"))  
    ' name => ((name.Length > 10) || name.StartsWith("G"))  
    ```  
  
     该代码创建一个表达式，包含在条件`AND`操作。 然后，它创建的实例`AndAlsoModifier`类，并将表达式传递给`Modify`此类的方法。 输出的原始版本以及修改后的表达式树以显示更改。  
  
6.  编译并运行该应用程序。  
  
## <a name="see-also"></a>另请参阅  
 [如何︰ 执行表达式树 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md)   
 [表达式树 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/index.md)
