---
title: "Sub 表达式 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
helpviewer_keywords: 
  - "lambda 表达式 [Visual Basic], 子表达式"
  - "子表达式 [Visual Basic]"
  - "子例程 [Visual Basic], 子表达式"
ms.assetid: 36b6bfd1-6539-4d8f-a5eb-6541a745ffde
caps.latest.revision: 6
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 6
---
# Sub 表达式 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

声明定义子例程 lambda 表达式的参数和代码。  
  
## 语法  
  
```  
Sub ( [ parameterlist ] ) statement  
- or -  
Sub ( [ parameterlist ] )  
  [ statements ]  
End Sub  
  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`parameterlist`|可选。  表示过程的参数的局部变量名称的列表。  即使该列表为空，也必须使用括号。  有关更多信息，请参见 [参数列表](../../../visual-basic/language-reference/statements/parameter-list.md)。|  
|`statement`|必选。  一条语句。|  
|`statements`|必选。  语句的列表。|  
  
## 备注  
 “lambda 表达式”是没有名称且执行一条或多条语句的子例程。  可在您可以使用委托类型的任何位置（除了作为 `RemoveHandler` 的参数）使用 lambda 表达式。  有关委托以及通过委托使用 lambda 表达式的更多信息，请参见 [Delegate 语句](../../../visual-basic/language-reference/statements/delegate-statement.md)和[宽松委托转换](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)。  
  
## Lambda 表达式语法  
 Lambda 表达式的语法类似于标准子例程的语法。  区别如下：  
  
-   lambda 表达式没有名称。  
  
-   Lambda 表达式不能有修饰符，例如 `Overloads` 或 `Overrides`。  
  
-   单行 lambda 表达式的主体必须是语句，而不是表达式。  函数体可以包含对子过程的调用，但不能包含对函数过程的调用。  
  
-   在 lambda 表达式中，要么所有参数都必须具有指定的数据类型，要么所有参数都必须推断得出。  
  
-   Lambda 表达式中不允许使用可选和 `ParamArray` 参数。  
  
-   Lambda 表达式中不允许使用泛型参数。  
  
## 示例  
 下面是将值写入控制台的 Lambda 表达式的示例。  该示例同时显示了一个子例程的单行和多行 Lambda 表达式语法。  有关更多示例，请参见[lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)。  
  
 [!code-vb[VbVbalrLambdas#15](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/sub-expression_1.vb)]  
  
## 请参阅  
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [运算符和表达式](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)   
 [宽松委托转换](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)