---
title: "如何︰ 声明自定义事件以避免阻止 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
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
- declaring events, custom
- events [Visual Basic], custom
- custom events
ms.assetid: 998b6a90-67c5-4d2c-8b11-366d3e355505
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 34b222bdbfdae0673b7150c220ca477b7e286dda
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-declare-custom-events-to-avoid-blocking-visual-basic"></a>如何：声明自定义事件以避免阻止 (Visual Basic)
有几种情况下很重要的一个事件处理程序不会阻止后续事件处理程序时。 自定义事件允许事件以异步方式调用其事件处理程序。  
  
 默认情况下，在事件声明的后备存储字段是一个按顺序组合所有事件处理程序的多路广播的委托。 这意味着，如果一个处理程序采用较长时间才能完成，它将阻止其他处理程序直到它完成。 （功能良好的事件处理程序应永远不会执行耗时较长或可能起阻止作用的操作。）  
  
 而不是使用 Visual Basic 提供的事件的默认实现，您可以使用自定义事件以异步方式执行的事件处理程序。  
  
## <a name="example"></a>示例  
 在此示例中，`AddHandler`取值函数添加的每个处理程序委托`Click`事件到<xref:System.Collections.ArrayList>存储在`EventHandlerList`字段。</xref:System.Collections.ArrayList>  
  
 在代码引发`Click`事件，`RaiseEvent`取值函数时，将调用以异步方式使用的所有事件处理程序委托<xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A>方法。</xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A> 该方法调用每个工作线程上的处理程序，并立即返回，这样处理程序无法阻止的另一个。  
  
 [!code-vb[VbVbalrEvents #&27;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-custom-events-to-avoid-blocking_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Collections.ArrayList></xref:System.Collections.ArrayList>   
 <xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A></xref:System.Web.Services.Protocols.LogicalMethodInfo.BeginInvoke%2A>   
 [事件](../../../../visual-basic/programming-guide/language-features/events/index.md)   
 [如何：声明自定义事件以节省内存](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-conserve-memory.md)
