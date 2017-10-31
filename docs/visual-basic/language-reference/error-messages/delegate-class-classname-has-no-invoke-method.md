---
title: "委托类&lt;classname&gt;有没有 Invoke 方法，因此这种类型的表达式不能是方法调用的目标 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30220
- bc30220
dev_langs:
- VB
helpviewer_keywords:
- BC30220
ms.assetid: 6be0d61c-f2f9-4f9b-ab90-8871a0d7206d
caps.latest.revision: 10
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
ms.openlocfilehash: ddc5ef0f0b3e9baa58f17dafb727e250c0fba9fd
ms.lasthandoff: 03/13/2017

---
# <a name="delegate-class-39ltclassnamegt39-has-no-invoke-method-so-an-expression-of-this-type-cannot-be-the-target-of-a-method-call"></a>委托类&lt;classname&gt;有没有 Invoke 方法，因此这种类型的表达式不能是方法调用的目标
调用`Invoke`通过委托已失败，因为`Invoke`上委托类未实现。  
  
 **错误 ID:** BC30220  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  确保委托类的实例已经用`Dim`到具有的委托实例分配了一个过程和语句`AddressOf`运算符。  
  
2.  找到实现委托类的代码中，确保它实现了`Invoke`过程。  
  
## <a name="see-also"></a>另请参阅  
 [委托](../../../visual-basic/programming-guide/language-features/delegates/index.md)   
 [Delegate 语句](../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [AddressOf 运算符](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)
