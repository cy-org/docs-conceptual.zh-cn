---
title: "处理事件 (Visual Basic 中) |Microsoft 文档"
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
- event handling [Visual Basic], walkthroughs
- walkthroughs [Visual Basic], event handling
- variables [Visual Basic], WithEvents
- events [Visual Basic], walkthroughs
- WithEvents keyword, walkthroughs
- event handlers [Visual Basic], walkthroughs
ms.assetid: f145b3fc-5ae0-4509-a2aa-1ff6934706bd
caps.latest.revision: 18
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
ms.openlocfilehash: 17cd0bddbe8c89cf60e19f3f2af6f448ad465d70
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-handling-events-visual-basic"></a>演练：处理事件 (Visual Basic)
这是演示如何处理事件的两个主题的第二个。 第一个主题，[演练︰ 声明和引发事件](../../../../visual-basic/programming-guide/language-features/events/walkthrough-declaring-and-raising-events.md)，演示如何声明和引发事件。 本部分使用窗体和该演练中的类来说明如何处理时其发生的事件。  
  
 `Widget`类的示例使用传统的事件处理语句。 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供用于处理事件的其他技术。 作为一个练习，您可以修改该示例以使用`AddHandler`和`Handles`语句。  
  
### <a name="to-handle-the-percentdone-event-of-the-widget-class"></a>若要处理的小组件类 PercentDone 事件  
  
1.  将以下代码中的放置`Form1`:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents #&4;](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_1.vb)]  
  
     `WithEvents`关键字指定变量`mWidget`用于处理对象的事件。 通过提供从其创建对象的类的名称指定对象的类型。  
  
     该变量`mWidget`中声明`Form1`因为`WithEvents`变量必须是类级别。 这是类的您将它们放入的类型无关，则返回 true。  
  
     该变量`mblnCancel`用于取消`LongTask`方法。  
  
## <a name="writing-code-to-handle-an-event"></a>编写代码来处理事件  
 一旦您声明变量的使用`WithEvents`，变量名都会显示在左侧的下拉列表的类**代码编辑器**。 当您选择`mWidget`、`Widget`右侧下拉列表中不显示类的事件。 选择一个事件将显示对应的事件过程以前缀`mWidget`和一条下划线。 与相关联的所有事件过程`WithEvents`变量指定的变量名称作为前缀。  
  
#### <a name="to-handle-an-event"></a>若要处理的事件  
  
1.  选择`mWidget`从左侧的下拉列表中**代码编辑器**。  
  
2.  选择`PercentDone`右侧下拉列表中的事件。 **代码编辑器**打开`mWidget_PercentDone`事件过程。  
  
    > [!NOTE]
    >  **代码编辑器**很有用，但并不是必需的插入新的事件处理程序。 在本演练中，就更直接，只是事件处理程序将直接复制到您的代码。  
  
3.  将以下代码添加到 `mWidget_PercentDone` 事件处理程序中：  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents #&5;](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_2.vb)]  
  
     每当`PercentDone`引发事件、 事件过程中显示在完成百分比`Label`控件。 `DoEvents`方法允许标签来重绘，并且还为用户提供机会单击**取消**按钮。  
  
4.  添加以下代码为`Button2_Click`事件处理程序︰  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents #&6;](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_3.vb)]  
  
 如果用户单击**取消**按钮`LongTask`运行的，`Button2_Click`执行事件就立即`DoEvents`语句允许发生的事件处理。 类级变量`mblnCancel`设置为`True`，和`mWidget_PercentDone`事件然后测试它，并将`ByRef Cancel`参数`True`。  
  
## <a name="connecting-a-withevents-variable-to-an-object"></a>连接到一个对象的 WithEvents 变量  
 `Form1`现在已设置好处理`Widget`对象的事件。 剩下的就是要查找`Widget`某个位置。  
  
 当您声明一个变量`WithEvents`在设计时，没有对象，则与之相关联。 一个`WithEvents`变量是就像任何其他对象变量一样。 您必须创建一个对象，并为其分配一个引用`WithEvents`变量。  
  
#### <a name="to-create-an-object-and-assign-a-reference-to-it"></a>若要创建一个对象，并为其分配一个引用  
  
1.  选择**（form1 事件）**从左侧的下拉列表中**代码编辑器**。  
  
2.  选择`Load`右侧下拉列表中的事件。 **代码编辑器**打开`Form1_Load`事件过程。  
  
3.  添加以下代码为`Form1_Load`事件过程中以创建`Widget`:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents #&7;](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_4.vb)]  
  
 此代码执行时，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]创建`Widget`对象，并将其事件连接到与关联的事件过程`mWidget`。 自此以后，每当`Widget`引发其`PercentDone`事件，`mWidget_PercentDone`事件过程中执行。  
  
#### <a name="to-call-the-longtask-method"></a>若要调用 LongTask 方法  
  
-   将以下代码添加到 `Button1_Click` 事件处理程序中：  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents #&8;](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_5.vb)]  
  
 之前`LongTask`标签，显示完成百分比必须进行初始化，并且类级别调用方法`Boolean`标志取消该方法必须设置为`False`。  
  
 `LongTask`被调用，任务持续时间为 12.2 秒。 `PercentDone`事件引发一次每&1; /&3; 的第二个。 引发事件时，每次`mWidget_PercentDone`事件过程中执行。  
  
 当`LongTask`操作后，`mblnCancel`测试以查看是否`LongTask`正常结束，或者如果它已停止，因为`mblnCancel`已设置为`True`。 仅在前一种情况中将更新的完成百分比。  
  
#### <a name="to-run-the-program"></a>运行程序  
  
1.  按 f5 键以将项目放在运行模式下。  
  
2.  单击**启动任务**按钮。 每次`PercentDone`引发事件，标签已更新为包含任务已完成的百分比。  
  
3.  单击**取消**按钮以停止该任务。 请注意，外观的**取消**按钮并不立即单击时更改。 `Click`才会发生直到`My.Application.DoEvents`语句允许事件处理。  
  
    > [!NOTE]
    >  `My.Application.DoEvents`窗体一样方法不完全相同的方式处理事件。 例如，在本演练中，您必须单击**取消**按钮两次。 若要使表单能够直接处理事件，可以使用多线程处理。 有关详细信息，请参阅[线程处理](http://msdn.microsoft.com/library/552f6c68-dbdb-4327-ae36-32cf9063d88c)。  
  
 您可能会发现有意义，按 f11 键运行该程序，并单步执行代码行一次。 您可以清楚地看到如何执行进入`LongTask`，，然后简要重新进入`Form1`每次`PercentDone`引发事件。  
  
 会发生什么情况如果，在执行过程中的代码返回`Form1`、`LongTask`方法再次被调用？ 如果堆栈溢出可能会出现最坏的情形，`LongTask`每次引发事件时调用。  
  
 您可能会导致该变量`mWidget`来处理另一个事件`Widget`对象的引用赋给新`Widget`到`mWidget`。 事实上，您可以在代码`Button1_Click`每次单击按钮时执行此操作。  
  
#### <a name="to-handle-events-for-a-different-widget"></a>若要处理不同的小组件的事件  
  
-   添加下面的代码行`Button1_Click`过程中，紧靠前读取的行`mWidget.LongTask(12.2, 0.33)`:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents #&9;](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_6.vb)]  
  
 上面的代码创建一个新`Widget`每次单击按钮。 只要`LongTask`方法完成后，对引用`Widget`发布后，与`Widget`被销毁。  
  
 一个`WithEvents`变量可以包含只有一个对象引用，一次，因此，如果您分配一个不同`Widget`对象传递给`mWidget`上, 一个`Widget`将不再处理对象的事件。 如果`mWidget`是唯一包含对旧的引用的对象变量`Widget`，该对象被销毁。 如果你想要处理来自多个事件`Widget`对象，请使用`AddHandler`语句，以分别处理每个对象的事件。  
  
> [!NOTE]
>  您可以声明任意多个`WithEvents`需要作为您的变量，但数组`WithEvents`不支持变量。  
  
## <a name="see-also"></a>另请参阅  
 [演练︰ 声明和引发事件](../../../../visual-basic/programming-guide/language-features/events/walkthrough-declaring-and-raising-events.md)   
 [事件](../../../../visual-basic/programming-guide/language-features/events/index.md)
