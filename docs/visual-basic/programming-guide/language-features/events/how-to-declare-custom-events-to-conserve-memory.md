---
title: "如何︰ 声明自定义事件以节省内存 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 87ebee87-260c-462f-979c-407874debd19
caps.latest.revision: 11
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
ms.openlocfilehash: 4f8ce32a3b4da411a73010119283ce9661b82a6c
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-declare-custom-events-to-conserve-memory-visual-basic"></a>如何：声明自定义事件以节省内存 (Visual Basic)
重要应用程序保持其内存使用量较低时，有几种情况。 自定义事件允许应用程序内存仅用于其处理的事件。  
  
 默认情况下，当一个类声明事件时，编译器将内存分配给一个字段来存储事件信息。 如果类具有许多未使用的事件，它们将不必要地占用内存。  
  
 而不是使用 Visual Basic 提供的事件的默认实现，您可以使用自定义事件以更加仔细地管理内存使用情况。  
  
## <a name="example"></a>示例  
 在此示例中，类使用的一个实例<xref:System.ComponentModel.EventHandlerList>类中，存储在`Events`字段中，在使用中存储有关的事件的信息。</xref:System.ComponentModel.EventHandlerList> <xref:System.ComponentModel.EventHandlerList>类是经过优化的列表类，用于保存委托。</xref:System.ComponentModel.EventHandlerList>  
  
 类使用中的所有事件`Events`字段来跟踪哪些方法正处理的每个事件。  
  
 [!code-vb[VbVbalrEvents #&22;](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-declare-custom-events-to-conserve-memory_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.ComponentModel.EventHandlerList></xref:System.ComponentModel.EventHandlerList>   
 [事件](../../../../visual-basic/programming-guide/language-features/events/index.md)   
 [如何：声明自定义事件以避免阻止](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-avoid-blocking.md)
