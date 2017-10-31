---
title: "堆栈空间 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrID28
dev_langs:
- VB
ms.assetid: bfcd792b-ac29-4158-81fc-ea0c13f4ffa2
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
ms.openlocfilehash: 6343767da28ea4e02f9443006b222640755f7882
ms.lasthandoff: 03/13/2017

---
# <a name="out-of-stack-space-visual-basic"></a>堆栈空间不足 (Visual Basic)
堆栈是内存的执行程序的要求使用动态增长和收缩的工作区域。 已超出其限制。  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  检查不太深嵌套的过程。  
  
2.  请确保正确终止递归过程。  
  
3.  如果本地变量所需的本地变量空间大于可用空间，请尝试在模块级别声明一些变量。 您也可以声明该过程中的所有变量静态通过在其前面`Property`， `Sub`，或`Function`关键字与`Static`。 也可以使用`Static`语句来声明过程中的单个静态变量。  
  
4.  重新定义一些您固定长度的字符串为可变长度字符串，作为固定长度的字符串使用更多堆栈空间比可变长度字符串。 您还可以定义在模块级别，它不需要堆栈空间的字符串。  
  
5.  检查数嵌套`DoEvents`函数调用，通过使用`Calls`对话框查看哪些过程是否在堆栈上处于活动状态。  
  
6.  请确保没有导致通过触发调用事件过程已在堆栈的事件"事件级联"。 级联事件相似的终止的递归过程调用，但它是不太明显的因为默认情况下，调用通过[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]而不是在代码中显式调用。 使用`Calls`对话框查看哪些过程是否在堆栈上处于活动状态。  
  
## <a name="see-also"></a>另请参阅  
 [“内存”窗口](https://docs.microsoft.com/visualstudio/debugger/memory-windows)
