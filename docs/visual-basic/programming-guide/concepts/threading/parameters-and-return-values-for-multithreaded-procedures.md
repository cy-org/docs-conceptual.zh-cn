---
title: "参数和返回值为多线程过程 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: cbdce172-7ff6-41a9-bb21-53a7c6f538a5
caps.latest.revision: 4
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d5d8adde531d31aa6bf353f53bd4cfecc084f515
ms.lasthandoff: 03/13/2017

---
# <a name="parameters-and-return-values-for-multithreaded-procedures-visual-basic"></a>参数和多线程过程 (Visual Basic 中) 的返回值
提供和多线程应用程序中返回值是很复杂，因为线程类的构造函数必须传递一个过程，不采用任何参数并不返回值的引用。 以下部分说明一些简单的方法来提供参数，以在单独的线程从过程返回的值。  
  
## <a name="supplying-parameters-for-multithreaded-procedures"></a>提供多线程过程的参数  
 提供多线程的方法调用的参数的最好办法是将目标方法包装在一个类并为该类类型的值将用作新线程的参数定义的字段。 这种方法的优点是可以具有其自己的参数，都创建新类的实例，每次想要启动新线程。 例如，假设您有一个计算一个三角形，如以下代码所示的区域的函数︰  
  
```vb  
Function CalcArea(ByVal Base As Double, ByVal Height As Double) As Double  
    CalcArea = 0.5 * Base * Height  
End Function  
```  
  
 您可以编写一个类用于包装`CalcArea`函数，并且创建字段来存储输入的参数，如下所示︰  
  
```vb  
Class AreaClass  
    Public Base As Double  
    Public Height As Double  
    Public Area As Double  
    Sub CalcArea()  
        Area = 0.5 * Base * Height  
        MessageBox.Show("The area is: " & Area.ToString)  
    End Sub  
End Class  
```  
  
 若要使用`AreaClass`，您可以创建`AreaClass`对象，并设置`Base`和`Height`属性，如下面的代码中所示︰  
  
```vb  
Protected Sub TestArea()  
    Dim AreaObject As New AreaClass  
    Dim Thread As New System.Threading.Thread(  
                        AddressOf AreaObject.CalcArea)  
    AreaObject.Base = 30  
    AreaObject.Height = 40  
    Thread.Start()  
End Sub  
```  
  
 请注意，`TestArea`过程不检查的值`Area`字段之后调用`CalcArea`方法。 因为`CalcArea`的单独线程上运行`Area`字段不能保证如果您在调用后立即检查设置`Thread.Start`。 下一节讨论了更好的方法可从多线程过程返回值。  
  
## <a name="returning-values-from-multithreaded-procedures"></a>从多线程过程返回值  
 从在单独的线程运行的过程返回值很复杂的过程不能是函数，也不能使用的事实`ByRef`参数。 返回值的最简单方法是使用<xref:System.ComponentModel.BackgroundWorker>组件可管理您的线程，并引发一个事件完成任务后，和过程与一个事件处理程序的结果。</xref:System.ComponentModel.BackgroundWorker>  
  
 下面的示例通过从在单独的线程上运行的过程引发一个事件来返回一个值︰  
  
```vb  
Private Class AreaClass2  
    Public Base As Double  
    Public Height As Double  
    Function CalcArea() As Double  
        ' Calculate the area of a triangle.  
        Return 0.5 * Base * Height  
    End Function  
End Class  
  
Private WithEvents BackgroundWorker1 As New System.ComponentModel.BackgroundWorker  
  
Private Sub TestArea2()  
    Dim AreaObject2 As New AreaClass2  
    AreaObject2.Base = 30  
    AreaObject2.Height = 40  
  
    ' Start the asynchronous operation.  
    BackgroundWorker1.RunWorkerAsync(AreaObject2)  
End Sub  
  
' This method runs on the background thread when it starts.  
Private Sub BackgroundWorker1_DoWork(  
    ByVal sender As Object,   
    ByVal e As System.ComponentModel.DoWorkEventArgs  
    ) Handles BackgroundWorker1.DoWork  
  
    Dim AreaObject2 As AreaClass2 = CType(e.Argument, AreaClass2)  
    ' Return the value through the Result property.  
    e.Result = AreaObject2.CalcArea()  
End Sub  
  
' This method runs on the main thread when the background thread finishes.  
Private Sub BackgroundWorker1_RunWorkerCompleted(  
    ByVal sender As Object,  
    ByVal e As System.ComponentModel.RunWorkerCompletedEventArgs  
    ) Handles BackgroundWorker1.RunWorkerCompleted  
  
    ' Access the result through the Result property.  
    Dim Area As Double = CDbl(e.Result)  
    MessageBox.Show("The area is: " & Area.ToString)  
End Sub  
```  
  
 您可以提供参数，并通过使用可选值返回到线程池线程`ByVal`的状态对象变量<xref:System.Threading.ThreadPool.QueueUserWorkItem%2A>方法。</xref:System.Threading.ThreadPool.QueueUserWorkItem%2A> 线程计时器线程还支持用于此目的的状态对象。 有关线程池和线程计时器的信息，请参阅[线程池 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/threading/thread-pooling.md)[线程池](http://msdn.microsoft.com/library/4b8bb2c8-8ca4-457c-9afd-d11bc9a05701)和[线程计时器 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/threading/thread-timers.md)。  
  
## <a name="see-also"></a>另请参阅  
 [演练︰ 利用 BackgroundWorker 组件 (Visual Basic 中) 的多线程处理](../../../../visual-basic/programming-guide/concepts/threading/walkthrough-multithreading-with-the-backgroundworker-component.md)   
 [线程池 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/thread-pooling.md)   
 [线程同步 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/thread-synchronization.md)   
 [事件](../../../../visual-basic/programming-guide/language-features/events/index.md)   
 [多线程应用程序 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/multithreaded-applications.md)   
 [委托](../../../../visual-basic/programming-guide/language-features/delegates/index.md)   
 [在组件多线程处理](http://msdn.microsoft.com/library/2fc31e68-fb71-4544-b654-0ce720478779)
