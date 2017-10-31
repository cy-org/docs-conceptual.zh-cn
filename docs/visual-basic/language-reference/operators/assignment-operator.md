---
title: "= 运算符 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Assign
- vb.=
dev_langs:
- VB
helpviewer_keywords:
- = operator [Visual Basic]
- = assignment statements [Visual Basic]
ms.assetid: 2dac2e49-86c8-42f8-80c1-458452fb5e29
caps.latest.revision: 16
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
ms.openlocfilehash: 47b69a908f12ec36daf2848da6ee4b04895fd3a4
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="-operator-visual-basic"></a>= 运算符 (Visual Basic)
将值分配给变量或属性。  
  
## <a name="syntax"></a>语法  
  
```  
variableorproperty = value  
```  
  
## <a name="parts"></a>部件  
 `variableorproperty`  
 任何可写的变量或任何属性。  
  
 `value`  
 任何文本、 常量或表达式。  
  
## <a name="remarks"></a>备注  
 等号左侧元素 (`=`) 可以是简单的标量变量、 属性或数组的元素。 该变量或属性不能为[ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)。 `=`运算符将值赋给变量右侧的值或在其左侧的属性。  
  
> [!NOTE]
>  `=`运算符也用作比较运算符。 有关详细信息，请参阅[比较运算符](../../../visual-basic/language-reference/operators/comparison-operators.md)。  
  
## <a name="overloading"></a>重载  
 `=`只能作为关系比较运算符，而不是赋值运算符可以重载运算符。 有关详细信息，请参阅[运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## <a name="example"></a>示例  
 下面的示例演示使用赋值运算符。 在右侧的值分配给左侧变量。  
  
 [!code-vb[VbVbalrOperators #&9;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/assignment-operator_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [< = 运算符](../../../visual-basic/language-reference/operators/and-assignment-operator.md)   
 [* = 运算符](../../../visual-basic/language-reference/operators/multiplication-assignment-operator.md)   
 [+ = 运算符](../../../visual-basic/language-reference/operators/addition-assignment-operator.md)   
 [-= 运算符 (Visual Basic)](../../../visual-basic/language-reference/operators/subtraction-assignment-operator.md)   
 [/ = 运算符 (Visual Basic)](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)   
 [\\= 运算符](../../../visual-basic/language-reference/operators/integer-division-assignment-operator.md)   
 [^ = 运算符](../../../visual-basic/language-reference/operators/exponentiation-assignment-operator.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)   
 [比较运算符](../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)   
 [局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)

