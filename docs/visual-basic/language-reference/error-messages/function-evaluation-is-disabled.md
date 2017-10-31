---
title: "已禁用函数求值，因为前一个函数求值超时 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc30957
- vbc30957
dev_langs:
- VB
helpviewer_keywords:
- BC30957
ms.assetid: 561e593a-f50a-4b72-a708-4cab60ec7b28
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
ms.openlocfilehash: b861b5c6c151c5d3aeec2810c7f2a228f22fdf6e
ms.lasthandoff: 03/13/2017

---
# <a name="function-evaluation-is-disabled-because-a-previous-function-evaluation-timed-out"></a>已禁用函数求值，因为前一个函数求值超时
由于上一个函数求值超时，已禁用函数求值。 若要重新启用函数求值，请再次单步执行或重新启动调试。  
  
 在 Visual Studio 调试器中，表达式可以指定过程调用，但另一个计算已超时。  
  
 超时时间的过程调用的可能原因包括无限循环或*无穷循环*。 有关详细信息，请参阅[为...下一条语句](../../../visual-basic/language-reference/statements/for-next-statement.md)。  
  
 无限循环的一种特殊情况是*递归*。 有关详细信息，请参阅[递归过程](../../../visual-basic/programming-guide/language-features/procedures/recursive-procedures.md)。  
  
 **错误 ID:** BC30957  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  如果可能，请确定前一个函数求值是什么以及引起超时。 否则，可能会再次遇到此错误。  
  
2.  请再次，调试器单步执行或终止并重新启动调试。  
  
## <a name="see-also"></a>另请参阅  
 [在 Visual Studio 中进行调试](https://docs.microsoft.com/visualstudio/debugger/debugging-in-visual-studio)   
 [使用调试器浏览代码](https://docs.microsoft.com/visualstudio/debugger/navigating-through-code-with-the-debugger)
