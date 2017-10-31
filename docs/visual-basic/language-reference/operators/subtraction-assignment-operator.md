---
title: "-= 运算符 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.-=
dev_langs:
- VB
helpviewer_keywords:
- -= operator [Visual Basic]
- assignment statements, compound
- statements [Visual Basic], compound assignment
- operator -=
- compound assignment statements
ms.assetid: 5ead0c37-ae50-48f7-8435-8e341d81cae1
caps.latest.revision: 19
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
ms.openlocfilehash: f640bd288c677954bae189c2e86ef096e7a73a2b
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="--operator-visual-basic"></a>-= 运算符 (Visual Basic)
减去表达式的值的变量或属性的值并将结果赋给变量或属性。  
  
## <a name="syntax"></a>语法  
  
```  
variableorproperty -= expression  
```  
  
## <a name="parts"></a>部件  
 `variableorproperty`  
 必需。 任何数值变量或属性。  
  
 `expression`  
 必需。 任何数值表达式。  
  
## <a name="remarks"></a>备注  
 在左侧元素`-=`运算符可以是简单的标量变量、 属性或数组的元素。 该变量或属性不能为[ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)。  
  
 `-=`运算符第一次 （对该运算符的右侧） 的表达式的值将从中减去的值的变量或属性 （该运算符左侧）。 该运算符会将该操作的结果分配给变量或属性。  
  
## <a name="overloading"></a>重载  
 [-运算符 (Visual Basic)](../../../visual-basic/language-reference/operators/subtraction-operator.md)可以是*重载*，这意味着，某个类或结构可以重新定义其行为时，操作数的类或结构的类型。 重载`-`运算符影响的应用程序行为`-=`运算符。 如果您的代码使用`-=`对类或结构，它重载`-`，请确保您了解其重新定义的行为。 有关详细信息，请参阅[运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## <a name="example"></a>示例  
 下面的示例使用`-=`运算符中减去&1;`Integer`从另一个变量并将结果赋给前一个变量。  
  
 [!code-vb[VbVbalrOperators #&11;](codesnippet/VisualBasic/subtraction-assignment-operator_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [-运算符 (Visual Basic)](../../../visual-basic/language-reference/operators/subtraction-operator.md)   
 [赋值运算符](../../../visual-basic/language-reference/operators/assignment-operators.md)   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [在 Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)

