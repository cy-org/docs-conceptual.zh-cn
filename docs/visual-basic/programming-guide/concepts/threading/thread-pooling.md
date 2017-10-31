---
title: "线程池 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 4903fb7a-eaad-435a-9add-1d1b32de3b83
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
ms.openlocfilehash: 6037d7ea17e260d44bae571aa25d413996f5a123
ms.lasthandoff: 03/13/2017

---
# <a name="thread-pooling-visual-basic"></a>线程池 (Visual Basic)
一个*线程池*是可以用来在后台执行多种任务的线程集合。 (请参阅[线程处理 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/threading/index.md)的背景信息。)这将使主线程可以自由以异步方式执行其他任务。  
  
 线程池通常用于在服务器应用程序。 每个传入请求被分配给一个线程从线程池，以便可以进行异步处理请求，而无需占用主线程或延迟的后续请求处理。  
  
 后在池中的线程完成其任务，它将返回到等待线程的队列可以重复使用。 这种重用使应用程序可避免创建新的每个任务的线程的开销。  
  
 线程池通常具有最大线程数。 如果所有线程都都正忙于，其他任务都被放在队列中，直到它们能够得到处理线程变为可用。  
  
 可以实现您自己的线程池，但很容易地使用线程池提供的.NET Framework<xref:System.Threading.ThreadPool>类。</xref:System.Threading.ThreadPool>  
  
 使用线程池，您调用<xref:System.Threading.ThreadPool.QueueUserWorkItem%2A?displayProperty=fullName>想要运行，有关该过程与委托的方法和 Visual Basic 创建线程，并运行您的过程。</xref:System.Threading.ThreadPool.QueueUserWorkItem%2A?displayProperty=fullName>  
  
## <a name="thread-pooling-example"></a>线程池示例  
 下面的示例演示如何使用线程池来开始几个任务。  
  
```vb  
Public Sub DoWork()  
    ' Queue a task.  
    System.Threading.ThreadPool.QueueUserWorkItem(  
        New System.Threading.WaitCallback(AddressOf SomeLongTask))  
    ' Queue another task.  
    System.Threading.ThreadPool.QueueUserWorkItem(  
        New System.Threading.WaitCallback(AddressOf AnotherLongTask))  
End Sub  
Private Sub SomeLongTask(ByVal state As Object)  
    ' Insert code to perform a long task.  
End Sub  
Private Sub AnotherLongTask(ByVal state As Object)  
    ' Insert code to perform another long task.  
End Sub  
```  
  
 线程池的一个优点是，您可以将参数传递一个状态对象到任务过程。 如果您正在调用的过程需要多个参数，您可以强制转换的结构或到类的实例`Object`数据类型。  
  
## <a name="thread-pool-parameters-and-return-values"></a>线程池参数和返回值  
 从一个线程池线程返回值并不简单。 不能使用函数调用返回值的标准方法，因为`Sub`过程是唯一的一种可排入线程池的过程。 一种方法可以提供参数，并返回值是通过包装这些参数，返回值和方法在包装器类，如中所述[参数和多线程过程 (Visual Basic 中) 的返回值](../../../../visual-basic/programming-guide/concepts/threading/parameters-and-return-values-for-multithreaded-procedures.md)。  
  
 提供的参数和返回值的数据更容易方法是通过使用可选`ByVal`状态对象变量<xref:System.Threading.ThreadPool.QueueUserWorkItem%2A>方法。</xref:System.Threading.ThreadPool.QueueUserWorkItem%2A> 如果使用此变量来传递到类的实例的引用，则可以修改由线程池线程的实例的成员，并将其用作返回值。  
  
 开始时它可能不明显，可以修改通过值传递的变量引用的对象。 您可以这样做，因为仅将对象引用通过值传递。 如果对引用的对象引用的对象的成员进行更改，所做的更改适用于实际的类实例。  
  
 结构不能用于返回状态对象内的值。 结构是值类型，因为异步进程所做的更改不会更改原始结构的成员。 使用结构时返回值，则不需要提供参数。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A></xref:System.Threading.ThreadPool.QueueUserWorkItem%2A>   
 <xref:System.Threading></xref:System.Threading>   
 <xref:System.Threading.ThreadPool></xref:System.Threading.ThreadPool>   
 [如何︰ 使用线程池 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/how-to-use-a-thread-pool.md)   
 [线程处理 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/index.md)   
 [多线程应用程序 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/multithreaded-applications.md)   
 [线程同步 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/thread-synchronization.md)
