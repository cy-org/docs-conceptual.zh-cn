---
title: "将 ByRef 参数的值复制 &quot;&lt;parametername&gt;返回到匹配的参数可以缩小范围从类型&lt;typename1，而&gt;为了 type&quot;&lt;typename2&gt;&quot; |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc32053
- vbc32053
dev_langs:
- VB
helpviewer_keywords:
- BC32053
ms.assetid: 281564b7-99f7-451f-b10d-f985e831bb25
caps.latest.revision: 8
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
ms.openlocfilehash: 84574006b2e2ccc669fdd83ebfb6eec06b00f041
ms.lasthandoff: 03/13/2017

---
# <a name="copying-the-value-of-39byref39-parameter-39ltparameternamegt39-back-to-the-matching-argument-narrows-from-type-39lttypename1gt39-to-type-39lttypename2gt39"></a>将 ByRef 参数的值复制 '&lt;parametername&gt;返回到匹配的参数可以缩小范围从类型&lt;typename1，而&gt;为了 type'&lt;typename2&gt;
调用过程时使用加宽到对应的参数类型的参数转换和收缩从参数到参数的转换。  
  
 在定义类或结构时，可以定义一个或多个转换运算符来将该类或结构类型转换为其他类型。 也可以定义反向转换运算符来将这些其他类型转换回类或结构类型。 当在过程调用中，使用您的类或结构类型[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]可以使用这些转换运算符将参数的类型转换为其对应的参数的类型。  
  
 如果传递参数[ByRef](../../../visual-basic/language-reference/modifiers/byref.md)，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]有时会将参数值复制到局部变量中而不是传递一个引用，该过程。 这种情况下，该过程返回时，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]然后必须将本地变量的值复制回调用代码中的参数。  
  
 如果将 `ByRef` 实参值复制到过程中，并且实参与形参为同一类型，则不必进行转换。 但是，如果类型不同，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]必须进行双向转换。 如果一种类型是类或结构类型，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]必须将其转换传入和传出另一种类型。 如果其中一个这些转换扩大转换，则可能会收缩反向转换。  
  
 **错误 ID:** BC32053  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   如果可能，请使用与过程参数的调用参数的类型相同，所以[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]不需要进行任何转换。  
  
-   如果您需要使用参数调用过程键入的参数类型不同，但不是需要将一个值返回到调用的参数，参数定义为[ByVal](../../../visual-basic/language-reference/modifiers/byval.md)而不是`ByRef`。  
  
-   如果您需要返回到调用变量的值，定义反向转换运算符用作[扩大](../../../visual-basic/language-reference/modifiers/widening.md)，如有可能。  
  
## <a name="see-also"></a>另请参阅  
 [过程](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和变量](../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [通过值和通过引用传递参数](../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md)   
 [如何︰ 定义运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [如何︰ 定义转换运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [在 Visual Basic 中的类型转换](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)
