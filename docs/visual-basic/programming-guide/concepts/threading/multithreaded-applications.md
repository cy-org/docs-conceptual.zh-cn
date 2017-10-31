---
title: "多线程应用程序 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 02b0444b-2e68-4f2c-bc28-28c046004017
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5bde7f49a2f2bc8a2e6c1eeab3722428b8a37a95
ms.lasthandoff: 03/13/2017

---
# <a name="multithreaded-applications-visual-basic"></a>多线程应用程序 (Visual Basic)
使用 Visual Basic 中，您可以编写在同时执行多个任务的应用程序。 具有潜力支持其他任务的任务可以单独在线程上执行，该过程称为*多线程处理*或*自由线程处理*。  
  
 使用多线程处理会更快地响应用户输入因为单独的线程上执行处理器密集型任务用户界面将保持活动状态的应用程序。 多线程编程时也很有帮助创建可扩展应用程序，因为您可以随着负载的增加添加线程。  
  
## <a name="creating-and-using-threads"></a>创建和使用线程  
 如果您需要更好地控制应用程序的线程的行为，您可以自己管理线程。 但是，请注意，编写正确的多线程应用程序可能很困难︰ 您的应用程序可能会停止响应或遇到暂时性错误引起的争用条件。 有关详细信息，请参阅[线程安全组件](http://msdn.microsoft.com/library/4f7c7377-a782-4bd0-aaa3-9db8c12945ee)。  
  
 声明类型的变量创建一个新线程<xref:System.Threading.Thread>并调用构造函数中，在提供的过程或你想要在新线程上执行的方法的名称。</xref:System.Threading.Thread> 下面的代码提供了一个示例。  
  
```vb  
Dim newThread As New System.Threading.Thread(AddressOf AMethod)  
```  
  
### <a name="starting-and-stopping-threads"></a>启动和停止的线程  
 若要启动新线程的执行，使用<xref:System.Threading.Thread.Start%2A>方法，如下面的代码中所示。</xref:System.Threading.Thread.Start%2A>  
  
```vb  
newThread.Start()  
```  
  
 若要停止线程的执行，使用<xref:System.Threading.Thread.Abort%2A>方法，如下面的代码中所示。</xref:System.Threading.Thread.Abort%2A>  
  
```vb  
newThread.Abort()  
```  
  
 除了启动和终止线程，您也可以暂停线程通过调用<xref:System.Threading.Thread.Sleep%2A>或<xref:System.Threading.Thread.Suspend%2A>方法中，使用恢复挂起的线程<xref:System.Threading.Thread.Resume%2A>方法，并销毁线程时使用的<xref:System.Threading.Thread.Abort%2A>方法</xref:System.Threading.Thread.Abort%2A></xref:System.Threading.Thread.Resume%2A></xref:System.Threading.Thread.Suspend%2A></xref:System.Threading.Thread.Sleep%2A>  
  
### <a name="thread-methods"></a>线程方法  
 下表显示了一些可用于控制各个线程的方法。  
  
|方法|操作|  
|------------|------------|  
|<xref:System.Threading.Thread.Start%2A></xref:System.Threading.Thread.Start%2A>|使线程开始运行。|  
|<xref:System.Threading.Thread.Sleep%2A></xref:System.Threading.Thread.Sleep%2A>|使线程暂停一段指定时间。|  
|<xref:System.Threading.Thread.Suspend%2A></xref:System.Threading.Thread.Suspend%2A>|在到达某一安全点时，线程暂停。|  
|<xref:System.Threading.Thread.Abort%2A></xref:System.Threading.Thread.Abort%2A>|在到达某一安全点时停止某个线程。|  
|<xref:System.Threading.Thread.Resume%2A></xref:System.Threading.Thread.Resume%2A>|重新启动挂起的线程|  
|<xref:System.Threading.Thread.Join%2A></xref:System.Threading.Thread.Join%2A>|导致当前线程等待另一个线程来完成。 如果使用的超时值，此方法返回`True`如果线程在分配的时间内完成。|  
  
### <a name="safe-points"></a>安全点  
 这些方法中的大多数都一目了然，但这一概念*安全点*可能还不熟悉给您。 安全点是在代码中的位置位置是安全的公共语言运行时来执行自动*垃圾回收*，释放未使用的变量并回收内存的过程。 当您调用<xref:System.Threading.Thread.Abort%2A>或<xref:System.Threading.Thread.Suspend%2A>方法的线程，公共语言运行时分析的代码，并确定要停止正在运行的线程的合适位置的位置。</xref:System.Threading.Thread.Suspend%2A> </xref:System.Threading.Thread.Abort%2A>  
  
### <a name="thread-properties"></a>线程属性  
 线程也包含几个有用的属性，如下面的表中所示︰  
  
|属性|值|  
|--------------|-----------|  
|<xref:System.Threading.Thread.IsAlive%2A></xref:System.Threading.Thread.IsAlive%2A>|包含值`True`如果某个线程处于活动状态。|  
|<xref:System.Threading.Thread.IsBackground%2A></xref:System.Threading.Thread.IsBackground%2A>|获取或设置一个布尔值，该值指示是否一个线程为或应该是后台线程。 后台线程与前台线程类似但后台线程不会阻止从停止的进程。 一旦某个进程的所有前台线程已都停止，公共语言运行时就会结束该进程通过调用<xref:System.Threading.Thread.Abort%2A>仍处于活动状态的后台线程上的方法。</xref:System.Threading.Thread.Abort%2A>|  
|<xref:System.Threading.Thread.Name%2A></xref:System.Threading.Thread.Name%2A>|获取或设置线程的名称。 最常用于在调试时查找各个线程。|  
|<xref:System.Threading.Thread.Priority%2A></xref:System.Threading.Thread.Priority%2A>|获取或设置一个值，由操作系统来确定线程调度优先顺序。|  
|<xref:System.Threading.Thread.ThreadState%2A></xref:System.Threading.Thread.ThreadState%2A>|包含描述线程的状态或状态的值。|  
  
## <a name="thread-priorities"></a>线程优先级  
 每个线程都具有用于确定需要执行进程 \ 处理器时间的方式大或小切片的优先级属性。 操作系统分配到高优先级的线程的较长的时间段和为低优先级的线程的较短的时间段。 值创建新线程`Normal`，但您可以更改<xref:System.Threading.Thread.Priority%2A>属性中的任何值<xref:System.Threading.ThreadPriority>枚举。</xref:System.Threading.ThreadPriority> </xref:System.Threading.Thread.Priority%2A>  
  
 请参阅<xref:System.Threading.ThreadPriority>有关各种线程优先级的详细说明。</xref:System.Threading.ThreadPriority>  
  
## <a name="foreground-and-background-threads"></a>前台和后台线程  
 一个*前台线程*无限制地运行而*后台线程*停止时的最后一个前台线程已停止。 您可以使用<xref:System.Threading.Thread.IsBackground%2A>属性来确定或更改后台线程的状态。</xref:System.Threading.Thread.IsBackground%2A>  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Threading.Thread></xref:System.Threading.Thread>   
 [线程同步 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/thread-synchronization.md)   
 [参数和多线程过程 (Visual Basic 中) 的返回值](../../../../visual-basic/programming-guide/concepts/threading/parameters-and-return-values-for-multithreaded-procedures.md)   
 [线程处理 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/threading/index.md)
