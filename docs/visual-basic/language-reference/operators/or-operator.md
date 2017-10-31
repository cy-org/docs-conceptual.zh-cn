---
title: "Or 运算符 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Or
dev_langs:
- VB
helpviewer_keywords:
- Or operator
- operators [Visual Basic], bitwise
- inclusive Or operator
- bitwise operators, OR operator
- Or keyword
- operators [Visual Basic], inclusive or
- operators [Visual Basic], disjunction
- bitwise comparison
- logical disjunction
- disjunction operator
ms.assetid: 41ed6905-bf3d-468a-9e3b-03c10d461891
caps.latest.revision: 12
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
ms.openlocfilehash: f3f6c013df6cd5c3b99e465bdc8bb0b4ead6bdf4
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="or-operator-visual-basic"></a>Or 运算符 (Visual Basic)
对两个执行逻辑析取`Boolean`表达式或两个数值表达式按位或运算。  
  
## <a name="syntax"></a>语法  
  
```  
result = expression1 Or expression2  
```  
  
## <a name="parts"></a>部件  
 `result`  
 必需。 任何`Boolean`或数值表达式。 有关`Boolean`比较，`result`是两个包含的逻辑析取`Boolean`值。 对于按位运算`result`是表示两个数字组合模式的包含按位析取的数值。  
  
 `expression1`  
 必需。 任何`Boolean`或数值表达式。  
  
 `expression2`  
 必需。 任何`Boolean`或数值表达式。  
  
## <a name="remarks"></a>备注  
 有关`Boolean`比较，`result`是`False`当且仅当`expression1`和`expression2`的计算结果为`False`。 下表说明了如何`result`确定的。  
  
|If `expression1` is|和`expression2`是|值`result`是|  
|-------------------------|--------------------------|------------------------------|  
|`True`|`True`|`True`|  
|`True`|`False`|`True`|  
|`False`|`True`|`True`|  
|`False`|`False`|`False`|  
  
> [!NOTE]
>  在`Boolean`比较，`Or`运算符始终计算两个表达式，它可能包含调用过程。 [OrElse 运算符](../../../visual-basic/language-reference/operators/orelse-operator.md)执行*短路*，这意味着，如果`expression1`是`True`，然后`expression2`则不会评估。  
  
 对于按位运算`Or`运算符在两个数值表达式执行按位比较位置相同的位并设置相应的位在`result`根据下表。  
  
|如果中位`expression1`是|和在位`expression2`是|中的位`result`是|  
|--------------------------------|---------------------------------|----------------------------|  
|1|1|1|  
|1|0|1|  
|0|1|1|  
|0|0|0|  
  
> [!NOTE]
>  因为逻辑和按位运算符的优先级低于其他算术和关系运算符，所以应将任何按位运算括在圆括号中以确保准确的执行。  
  
## <a name="data-types"></a>数据类型  
 如果其中一个的操作数包括`Boolean`Visual Basic 表达式和一个数值表达式，将转换`Boolean`为数字值的表达式 (– 1 表示`True`，0 表示`False`)，并执行按位运算。  
  
 有关`Boolean`比较，结果的数据类型是`Boolean`。 有关的按位比较，结果数据类型为数值类型适用于数据类型的`expression1`和`expression2`。 请参阅中的"关系与按位比较"表[运算符结果的数据类型的](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md)。  
  
## <a name="overloading"></a>重载  
 `Or`运算符可以被*重载*，这意味着，某个类或结构可以重新定义其行为时，操作数的类或结构的类型。 如果您的代码对这样的类或结构中使用此运算符，请确保您了解其被重新定义的行为。 有关详细信息，请参阅[运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)。  
  
## <a name="example"></a>示例  
 下面的示例使用`Or`运算符对两个表达式执行包含的逻辑析取。 结果是`Boolean`值，该值表示两个表达式之一是否`True`。  
  
 [!code-vb[VbVbalrOperators #&35;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/or-operator_1.vb)]  
  
 前面的示例将生成的结果`True`， `True`，和`False`分别。  
  
## <a name="example"></a>示例  
 下面的示例使用`Or`运算符对两个数值表达式的各个位执行包含逻辑析取。 如果任一操作数中的对应位将设置为 1，则结果模式中的位将设置。  
  
 [!code-vb[VbVbalrOperators #&36;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/or-operator_2.vb)]  
  
 前面的示例分别产生 10、 14 和 14 的结果。  
  
## <a name="see-also"></a>另请参阅  
 [逻辑/按位运算符 (Visual Basic)](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)   
 [在 Visual Basic 中的运算符优先级](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [按功能列出的运算符](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [OrElse 运算符](../../../visual-basic/language-reference/operators/orelse-operator.md)   
 [在 Visual Basic 中的逻辑和按位运算符](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)

