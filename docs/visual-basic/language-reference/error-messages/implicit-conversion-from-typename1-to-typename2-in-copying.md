---
title: "从隐式转换&lt;typename1，而&gt;&quot;to&quot;&lt;typename2&gt;in ByRef 参数的值复制&quot;&lt;parametername&gt;返回到匹配的参数。 | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc41999
- bc41999
dev_langs:
- VB
helpviewer_keywords:
- BC41999
ms.assetid: ae48c738-dff8-4c0f-8931-bbb70b2c8b03
caps.latest.revision: 7
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
ms.openlocfilehash: e397241aab78e17ea4efde0ea682d0e237fb8f8a
ms.lasthandoff: 03/13/2017

---
# <a name="implicit-conversion-from-39lttypename1gt39-to-39lttypename2gt39-in-copying-the-value-of-39byref39-parameter-39ltparameternamegt39-back-to-the-matching-argument"></a>从隐式转换&lt;typename1，而&gt;'to'&lt;typename2&gt;in ByRef 参数的值复制'&lt;parametername&gt;返回到匹配的参数。
与调用了过程[ByRef](../../../visual-basic/language-reference/modifiers/byref.md)相比，其对应的参数不同类型的参数。  
  
 如果传递了参数`ByRef`，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]有时会将参数值复制到局部变量中而不是传递一个引用，该过程。 这种情况下，该过程返回时，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]然后必须将本地变量的值复制回调用代码中的参数。  
  
 如果将 `ByRef` 实参值复制到过程中，并且实参与形参为同一类型，则不必进行转换。 但是，如果类型不同，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]必须进行双向转换。 由于不能使用`CType`或任何其他转换关键字上过程参数或参数，此类转换始终是隐式。  
  
 默认情况下，此消息是一个警告。 有关隐藏警告或将警告视为错误的信息，请参见 [Configuring Warnings in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID:** BC41999  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   如果可能，请使用与过程参数的调用参数的类型相同，所以[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]不需要进行任何转换。  
  
-   如果您需要使用参数调用过程键入的参数类型不同，但不是需要将一个值返回到调用的参数，参数定义为[ByVal](../../../visual-basic/language-reference/modifiers/byval.md)而不是`ByRef`。  
  
## <a name="see-also"></a>另请参阅  
 [过程](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [过程参数和变量](../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [通过值和通过引用传递参数](../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [隐式转换和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
