---
title: "线程池 (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 98ae68c1-ace8-44b9-9317-8920ac9ef2b6
caps.latest.revision: 5
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d2f8e5a2d7a83dc6fef72ef87b4003ae49656d8f
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="thread-pooling-c"></a>线程池 (C#)
线程池是可用于在后台执行多种任务的线程集合。 （有关背景信息，请参阅[线程处理 (C#)](../../../../csharp/programming-guide/concepts/threading/index.md)。）这使主线程可以自由地异步执行其他任务。  
  
 线程池通常用于服务器应用程序。 每个传入请求都将分配给线程池中的一个线程，因此可以异步处理请求，而不会占用主线程，也不会延迟后续请求的处理。  
  
 一旦池中的线程完成任务，它将返回到等待线程队列中，等待被重复使用。 通过这种重复使用，应用程序可以避免产生为每个任务创建新线程的开销。  
  
 线程池通常具有最大线程数限制。 如果所有线程处于忙碌状态，则额外的任务将放入队列中，直到有线程可用时才能够得到处理。  
  
 你可以实现自己的线程池，但是通过 <xref:System.Threading.ThreadPool> 类使用 .NET Framework 提供的线程池更容易。  
  
 通过使用线程池，可针对想运行的过程调用具有一个委托的 <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A?displayProperty=fullName> 方法，然后 C# 将创建线程并运行此过程。  
  
## <a name="thread-pooling-example"></a>线程池示例  
 下面的示例演示如何使用线程池来启动若干任务。  
  
```csharp  
public void DoWork()  
{  
    // Queue a task.  
    System.Threading.ThreadPool.QueueUserWorkItem(  
        new System.Threading.WaitCallback(SomeLongTask));  
    // Queue another task.  
    System.Threading.ThreadPool.QueueUserWorkItem(  
        new System.Threading.WaitCallback(AnotherLongTask));  
}  
  
private void SomeLongTask(Object state)  
{  
    // Insert code to perform a long task.  
}  
  
private void AnotherLongTask(Object state)  
{  
    // Insert code to perform a long task.  
}  
```  
  
 线程池的一个优点是可以将状态对象中的自变量传递到任务过程。 如果要调用的过程需要多个自变量，可将结构或类的实例强制转换为 `Object` 数据类型。  
  
## <a name="thread-pool-parameters-and-return-values"></a>线程池参数和返回值  
 不能直接从线程池线程返回值。 不允许使用通过函数调用来返回值的标准方法，因为 `Sub` 过程是唯一一种可以排队到线程池的过程。 一种提供参数和返回值的方法是将参数、返回值和方法包装在一个包装类中，如[多线程过程的参数和返回值 (C#)](../../../../csharp/programming-guide/concepts/threading/parameters-and-return-values-for-multithreaded-procedures.md) 中所述。  
  
 一种提供参数和返回值的更简单方法是使用 <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A> 方法的可选 `ByVal` 状态对象变量。 如果使用此变量来传递对类实例的引用，则该实例的成员可以由线程池线程修改，并用作返回值。  
  
 最初，可以修改由值传递的变量所引用的对象可能并不明显。 由于只有对象引用由值传递，因此可以执行此操作。 当对由对象引用所引用的对象的成员进行更改时，这些更改将应用于实际的类实例。  
  
 不能使用结构在状态对象内部返回值。 由于结构属于值类型，异步进程所做的更改不会更改原始结构的成员。 如果不需要返回值，可以使用结构来提供参数。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Threading.ThreadPool.QueueUserWorkItem%2A>   
 <xref:System.Threading>   
 <xref:System.Threading.ThreadPool>   
 [如何：使用线程池 (C#)](../../../../csharp/programming-guide/concepts/threading/how-to-use-a-thread-pool.md)   
 [线程处理 (C#)](../../../../csharp/programming-guide/concepts/threading/index.md)   
 [多线程应用程序 (C#)](../../../../csharp/programming-guide/concepts/threading/multithreaded-applications.md)   
 [线程同步 (C#)](../../../../csharp/programming-guide/concepts/threading/thread-synchronization.md)

