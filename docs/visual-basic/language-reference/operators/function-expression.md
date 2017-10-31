---
title: "函数表达式 (Visual Basic 中) |Microsoft 文档"
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
- Function expression [Visual Basic]
- functions [Visual Basic], function expressions
- lambda expressions [Visual Basic], function expression
ms.assetid: e8a47a45-4b8a-4f45-a623-7653625dffbc
caps.latest.revision: 18
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
ms.openlocfilehash: 9b181b18a28a8b92a392fffdc10e08690d54f545
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="function-expression-visual-basic"></a>函数表达式 (Visual Basic)
声明的参数和函数的 lambda 表达式定义的代码。  
  
## <a name="syntax"></a>语法  
  
```  
Function ( [ parameterlist ] ) expression  
- or -  
Function ( [ parameterlist ] )  
  [ statements ]  
End Function  
```  
  
## <a name="parts"></a>部件  
  
|术语|定义|  
|---|---|  
|`parameterlist`|可选。 本地变量的名称，表示此过程的参数的列表。 括号必须存在，即使该列表为空。 请参阅[参数列表](../../../visual-basic/language-reference/statements/parameter-list.md)。|  
|`expression`|必需。 单个表达式。 表达式的类型是该函数的返回类型。|  
|`statements`|必需。 返回一个值，通过使用语句的列表`Return`语句。 (请参阅[Return 语句](../../../visual-basic/language-reference/statements/return-statement.md)。)返回的值的类型为该函数的返回类型。|  
  
## <a name="remarks"></a>备注  
 一个*lambda 表达式*是没有名称，用于计算并返回一个值的函数。 您可以使用 lambda 表达式任意位置可用作委托类型，除参数`RemoveHandler`。 有关委托和使用委托的 lambda 表达式的用法的详细信息，请参阅[委托语句](../../../visual-basic/language-reference/statements/delegate-statement.md)和[宽松委托转换](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)。  
  
## <a name="lambda-expression-syntax"></a>Lambda 表达式语法  
 Lambda 表达式的语法类似于标准函数。 区别，如下所示如下︰  
  
-   Lambda 表达式不具有一个名称。  
  
-   Lambda 表达式不能具有修饰符，如`Overloads`或`Overrides`。  
  
-   不使用 lambda 表达式`As`子句来指定该函数的返回类型。 相反，该类型被推断从单行 lambda 表达式的主体，计算得出的值或多行 lambda 表达式的返回值。 例如，如果单行 lambda 表达式的主体是`Where cust.City = "London"`，其返回类型是`Boolean`。  
  
-   单行 lambda 表达式的主体必须是一个表达式，而不是语句。 主体可以包含的调用函数的过程，但未对一个 sub 过程的调用。  
  
-   必须必须推断数据类型或所有已经指定所有参数。  
  
-   不允许使用可选和 Paramarray 参数。  
  
-   不允许泛型参数。  
  
## <a name="example"></a>示例  
 下面的示例演示两种方法可以创建简单的 lambda 表达式。 第一个使用`Dim`提供该函数的名称。 若要调用函数时，您传递参数的值。  
  
 [!code-vb[VbVbalrLambdas #&1;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/function-expression_1.vb)]  
  
 [!code-vb[VbVbalrLambdas #&2;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/function-expression_2.vb)]  
  
## <a name="example"></a>示例  
 或者，可以声明并在同一时间运行该函数。  
  
 [!code-vb[VbVbalrLambdas #&3;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/function-expression_3.vb)]  
  
## <a name="example"></a>示例  
 下面是递增其参数并返回的值的 lambda 表达式的示例。 该示例同时显示的单行和多行 lambda 表达式语法的函数。 有关更多示例，请参阅[Lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)。  
  
 [!code-vb[VbVbalrLambdas #&14;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/function-expression_4.vb)]  
  
## <a name="example"></a>示例  
 Lambda 表达式是基础中的查询运算符的许多[!INCLUDE[vbteclinqext](../../../csharp/getting-started/includes/vbteclinqext_md.md)]，并可以在基于方法的查询中显式使用。 下面的示例显示了典型[!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq_md.md)]查询，然后再查询的平移到方法格式。  
  
```vb  
Dim londonCusts = From cust In db.Customers  
                       Where cust.City = "London"  
                       Select cust  
  
' This query is compiled to the following code:  
Dim londonCusts = db.Customers.  
                  Where(Function(cust) cust.City = "London").  
                  Select(Function(cust) cust)  
```  
  
 有关查询方法的详细信息，请参阅[查询](../../../visual-basic/language-reference/queries/queries.md)。 有关标准查询运算符的详细信息，请参阅[标准查询运算符概述](http://msdn.microsoft.com/library/24cda21e-8af8-4632-b519-c404a839b9b2)。  
  
## <a name="see-also"></a>另请参阅  
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [运算符和表达式](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)   
 [值的比较](../../../visual-basic/programming-guide/language-features/operators-and-expressions/value-comparisons.md)   
 [布尔表达式](../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md)   
 [如果运算符](../../../visual-basic/language-reference/operators/if-operator.md)   
 [宽松委托转换](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)

