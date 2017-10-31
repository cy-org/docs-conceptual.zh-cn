---
title: "声明和引发事件 (Visual Basic 中) |Microsoft 文档"
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
- declarations, events
- events [Visual Basic], walkthroughs
- declaring events, walkthroughs
- events [Visual Basic], declaring
- events [Visual Basic], raising
- raising events, walkthroughs
ms.assetid: 8ffb3be8-097d-4d3c-b71e-04555ebda2a2
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 233673c1d42684b7caa9042d18fb341a1043a31b
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-declaring-and-raising-events-visual-basic"></a>演练：声明和引发事件 (Visual Basic)
本演练演示如何声明和引发事件的一个名为类`Widget`。 完成步骤后，您可能需要阅读的配套主题，[演练︰ 处理事件](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md)，它演示如何使用来自事件`Widget`对象提供应用程序中的状态信息。  
  
## <a name="the-widget-class"></a>小组件类  
 假定您有目前`Widget`类。 您`Widget`类具有方法会很长时间才能执行，并且您希望您的应用程序能够提供某种进度指示器。  
  
 当然，你可以制作`Widget`对象会显示完成百分比的对话框中，但这样您将会使用在其中每个项目在该对话框`Widget`类。 一个好的对象的设计原则是让使用对象句柄的用户界面的应用程序，除非该对象的总体目的就是管理表单或对话框。  
  
 用途`Widget`是执行其他任务，所以最好添加`PercentDone`事件并让调用的过程`Widget`方法的处理事件和显示状态更新。 `PercentDone`事件还可以提供用于取消该任务的机制。  
  
#### <a name="to-build-the-code-example-for-this-topic"></a>若要生成本主题的代码示例  
  
1.  打开一个新[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Windows 应用程序项目，然后创建名为窗体`Form1`。  
  
2.  添加两个按钮和标签与`Form1`。  
  
3.  下表中所示命名对象。  
  
    |对象|属性|设置|  
    |------------|--------------|-------------|  
    |`Button1`|`Text`|启动任务|  
    |`Button2`|`Text`|取消|  
    |`Label`|`(Name)`, `Text`|lblPercentDone 0|  
  
4.  在**项目**菜单上，选择**添加类**添加一个名为类`Widget.vb`到项目。  
  
#### <a name="to-declare-an-event-for-the-widget-class"></a>若要声明构件类的事件  
  
-   使用`Event`关键字来声明中的事件`Widget`类。 请注意，一个事件可以有`ByVal`和`ByRef`参数，为`Widget`的`PercentDone`事件所示︰  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents #&1;](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-declaring-and-raising-events_1.vb)]  
  
 当调用对象收到`PercentDone`事件，`Percent`参数中包含的任务已完成的百分比。 `Cancel`参数可以设置为`True`取消引发该事件的方法。  
  
> [!NOTE]
>  您可以声明事件参数，就像参数的过程，但存在以下例外︰ 事件不能有`Optional`或`ParamArray`参数，且事件不具有返回值。  
  
 `PercentDone`事件由引发`LongTask`方法`Widget`类。 `LongTask`采用两个参数︰ 该方法自称要工作和之前的最小时间间隔的时间长度`LongTask`暂停以引发`PercentDone`事件。  
  
#### <a name="to-raise-the-percentdone-event"></a>若要引发 PercentDone 事件  
  
1.  若要简化对访问`Timer`此类使用的属性添加`Imports`到您的类模块的声明部分顶部的语句上方`Class Widget`语句。  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents #&2;](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-declaring-and-raising-events_2.vb)]  
  
2.  将下面的代码添加到 `Widget` 类中:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents #&3;](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-declaring-and-raising-events_3.vb)]  
  
 当您的应用程序调用`LongTask`方法，`Widget`类引发`PercentDone`事件每个`MinimumInterval`秒为单位。 该事件返回时，`LongTask`检查以查看是否`Cancel`参数设置为`True`。  
  
 此处有必要的几个免责声明。 为简单起见，`LongTask`过程假定您事先知道任务将花费多长时间。 这几乎不会是这种情况。 将任务划分为大小相等的块区可能很困难，且通常最重要的事情向用户只需在获得的内容不会进行的指示之前经过的时间量。  
  
 您可能已经发现了另一个缺陷在此示例中。 `Timer`属性返回的自午夜以来经过的秒数; 因此，应用程序何故停止响应如果只是在午夜之前启动。 更仔细的测量时间的方法将执行如下考虑在内，边界条件或根本不用它们，如使用属性`Now`。  
  
 现在，`Widget`类可引发事件，您可以将移动到下一个演练。 [演练︰ 处理事件](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md)演示如何使用`WithEvents`将与一个事件处理程序相关联`PercentDone`事件。  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.DateAndTime.Timer%2A></xref:Microsoft.VisualBasic.DateAndTime.Timer%2A>   
 <xref:Microsoft.VisualBasic.DateAndTime.Now%2A></xref:Microsoft.VisualBasic.DateAndTime.Now%2A>   
 [演练︰ 处理事件](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md)   
 [事件](../../../../visual-basic/programming-guide/language-features/events/index.md)
