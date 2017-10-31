---
title: "事件 (Visual Basic)"
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
- events [Visual Basic], about events
- events [Visual Basic]
ms.assetid: 8fb0353a-e41b-4e23-b78f-da65db832f70
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 84f8385e1b2f16c4bcfa53ef2c77e1f0cf61e5e3
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="events-visual-basic"></a>事件 (Visual Basic)
虽然可以将 [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] 项目可视化为按序列执行的一系列过程，但实际上大多数程序都是事件驱动型。也就是说，外部发生的*事件*决定了执行流。  
  
 事件是一种信号，可指示应用程序某重要事件已发生。 例如，当用户单击窗体控件时，窗体会引发 `Click` 事件，并调用可处理此事件的过程。 借助事件，各个不同的任务还可以相互通信。 例如，应用程序执行的排序任务与主应用程序是分开的。 如果用户取消排序，应用程序便会发送 cancel 事件，指示停止排序过程。  
  
## <a name="event-terms-and-concepts"></a>事件术语和概念  
 此部分介绍了 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] 中的事件术语和概念。  
  
### <a name="declaring-events"></a>声明事件  
 可以使用 `Event` 关键字在类、结构、模块和接口中声明事件，如以下示例所示：  
  
 [!code-vb[VbVbalrEvents#24](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_1.vb)]  
  
### <a name="raising-events"></a>引发事件  
 事件类似于消息，指示某重要事件已发生。 广播消息的行为称为*引发*事件。 在 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] 中，使用 `RaiseEvent` 语句引发事件，如以下示例所示：  
  
 [!code-vb[VbVbalrEvents#25](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_2.vb)]  
  
 必须在声明事件的类、模块或结构范围内引发事件。 例如，派生类不能引发继承自基类的事件。  
  
### <a name="event-senders"></a>事件发送方  
 所有能够引发事件的对象都是*事件发送方*，亦称为“*事件源*”。 例如，窗体、控件和用户定义对象都是事件发送方。  
  
### <a name="event-handlers"></a>事件处理程序  
 *事件处理程序*是在相应事件发生时调用的过程。 可以将签名一致的任意有效子例程用作事件处理程序。 不过，不能将函数用作事件处理程序，因为它不能向事件源返回值。  
  
 [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] 对事件处理程序采用标准命名约定，即名称中包含事件发送方的名称、下划线和事件名称。 例如，`button1` 按钮的 `Click` 事件将命名为 `Sub button1_Click`。  
  
> [!NOTE]
>  我们建议在为你自己的事件定义事件处理程序时采用此命名约定，但这不是一项强制性要求；可以命名任意有效的子例程名称。  
  
## <a name="associating-events-with-event-handlers"></a>关联事件与事件处理程序  
 必须先使用 `Handles` 或 `AddHandler` 语句关联事件处理程序与事件，然后才能使用事件处理程序。  
  
### <a name="withevents-and-the-handles-clause"></a>WithEvents 和 Handles 子句  
 使用 `WithEvents` 语句和 `Handles` 子句，可以声明性的方式指定事件处理程序。 使用 `WithEvents` 关键字声明的对象引发的事件可以由使用 `Handles` 语句针对相应事件指定的任意过程进行处理，如以下示例所示：  
  
 [!code-vb[VbVbalrEvents#1](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_3.vb)]  
  
 `WithEvents` 语句和 `Handles` 子句通常是事件处理程序的最佳选择，因为它们使用的声明性语法简化了事件处理程序的编码、读取和调试。 不过，请注意，使用 `WithEvents` 变量还要遵循以下限制：  
  
-   不能将 `WithEvents` 变量用作对象变量。 也就是说，不能将其声明为 `Object`，必须在声明变量时指定类名。  
  
-   由于共享事件未与类实例绑定，因此不能使用 `WithEvents` 以声明性方式处理共享事件。 同样，不能使用 `WithEvents` 或 `Handles` 处理 `Structure` 中的事件。 在这两种情况下，均可使用 `AddHandler` 语句处理这些事件。  
  
-   无法创建 `WithEvents` 变量的数组。  
  
 `WithEvents` 变量允许一个事件处理程序处理一种或多种事件，也允许一个或多个事件处理程序处理同一种事件。  
  
 虽然 `Handles` 子句是关联事件与事件处理程序的标准方法，但只能在编译时关联事件与事件处理程序。  
  
 在某些情况下（如事件与窗体或控件相关联），[!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] 会自动存根空事件处理程序，并将其与事件相关联。 例如，在设计模式下双击窗体上的命令按钮时，[!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] 会为命令按钮创建空事件处理程序和 `WithEvents` 变量，如以下代码所示：  
  
 [!code-vb[VbVbalrEvents#26](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_4.vb)]  
  
### <a name="addhandler-and-removehandler"></a>AddHandler 和 RemoveHandler  
 `AddHandler` 语句与 `Handles` 子句类似，两者都允许指定事件处理程序。 不同之处在于，`AddHandler` 与 `RemoveHandler` 结合使用比 `Handles` 子句更具灵活性，你可以动态添加、删除和更改与事件关联的事件处理程序。 若要处理共享事件或结构中的事件，必须使用 `AddHandler`。  
  
 `AddHandler` 需要使用两个自变量：事件发送方（如控件）引发的事件的名称和计算结果为委托的表达式。 使用 `AddHandler` 时，无需显式指定委托类，因为 `AddressOf` 语句始终返回对委托的引用。 下面的示例将事件处理程序与对象引发的事件相关联：  
  
 [!code-vb[VbVbalrEvents#28](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_5.vb)]  
  
 `RemoveHandler` 用于解除事件与事件处理程序的关联，所用语法与 `AddHandler` 一样。 例如:   
  
 [!code-vb[VbVbalrEvents#29](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_6.vb)]  
  
 在以下示例中，事件处理程序与事件相关联，且此事件已引发。 事件处理程序捕获此事件并显示消息。  
  
 然后删除第一个事件处理程序，并将另一个事件处理程序与此事件相关联。 当此事件再次引发时，显示不同的消息。  
  
 最后删除第二个事件处理程序，然后第三次引发此事件。 因为不再有事件处理程序与此事件相关联，所以不会执行任何操作。  
  
 [!code-vb[VbVbalrEvents#38](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_7.vb)]  
  
## <a name="handling-events-inherited-from-a-base-class"></a>处理继承自基类的事件  
 *派生类*继承了基类特征的类，可以使用 `Handles``MyBase` 语句处理基类引发的事件。  
  
#### <a name="to-handle-events-from-a-base-class"></a>处理继承自基类的事件的具体操作  
  
-   向事件处理程序过程的声明行添加 `Handles MyBase.` *eventname* 语句，在派生类中声明事件处理程序，其中 *eventname* 是要处理的继承自基类的事件名称。 例如:   
  
     [!code-vb[VbVbalrEvents#12](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_8.vb)]  
  
## <a name="related-sections"></a>相关章节  
  
|标题|说明|  
|-----------|-----------------|  
|[演练：声明和引发事件](../../../../visual-basic/programming-guide/language-features/events/walkthrough-declaring-and-raising-events.md)|分步展示了如何声明和引发类事件。|  
|[演练：处理事件](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md)|展示了如何编写事件处理程序过程。|  
|[如何：声明自定义事件以避免阻止](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-avoid-blocking.md)|介绍了如何定义允许异步调用事件处理程序的自定义事件。|  
|[如何：声明自定义事件以节省内存](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-conserve-memory.md)|介绍了如何定义仅在事件处理时占用内存的自定义事件。|  
|[Visual Basic 中继承的事件处理程序疑难解答](../../../../visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)|列出了在继承的组件中使用事件处理程序时遇到的常见问题。|  
|[事件](../../../../standard/events/index.md)|概述了 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 中的事件模型。|  
|[在 Windows 窗体中创建事件处理程序](https://msdn.microsoft.com/library/dacysss4.aspx)|介绍了如何处理与 Windows 窗体对象关联的事件。|  
|[委托](../../../../visual-basic/programming-guide/language-features/delegates/index.md)|概述了 Visual Basic 中的委托。|

