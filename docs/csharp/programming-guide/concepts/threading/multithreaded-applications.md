---
title: "多线程应用程序 (C#)"
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
ms.assetid: b7015cfb-d506-4eac-b2f8-b2caaa9cc977
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: dfe0f9c6e911295270df8464d1070a524412466d
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="multithreaded-applications-c"></a>多线程应用程序 (C#)
借助 C#，可以编写同时执行多个任务的应用程序。 可在单独的线程上执行可能妨碍其他任务的任务，这些线程是称为多线程处理或自由线程处理的进程。  
  
 使用多线程处理的应用程序可以更快地响应用户输入，因为在单独的线程上执行处理器密集型任务时，用户界面将保持活动状态。 创建可扩展的应用程序时，多线程编程也很有用，因为可以随着负载的增加添加线程。  
  
## <a name="creating-and-using-threads"></a>创建和使用线程  
 如果需要更强地控制应用程序线程的行为，可以自己管理线程。 但是，请注意，编写正确的多线程应用程序可能很困难：应用程序可能会停止响应或遇到争用条件引起的暂时性错误。 有关详细信息，请参阅[线程安全组件](http://msdn.microsoft.com/library/4f7c7377-a782-4bd0-aaa3-9db8c12945ee)。  
  
 通过声明类型 <xref:System.Threading.Thread> 的变量和调用构造函数，然后提供要在新线程上执行的过程或方法的名称来新建线程。 下面的代码提供了一个示例。  
  
```csharp  
System.Threading.Thread newThread =  
    new System.Threading.Thread(AMethod);  
```  
  
### <a name="starting-and-stopping-threads"></a>启动和停止线程  
 要开始执行新线程，请使用 <xref:System.Threading.Thread.Start%2A> 方法，如下面的代码中所示。  
  
```csharp  
newThread.Start();  
```  
  
 要停止执行线程，请使用 <xref:System.Threading.Thread.Abort%2A> 方法，如下面的代码中所示。  
  
```csharp  
newThread.Abort();  
```  
  
 除了启动和停止线程，还可以通过调用 <xref:System.Threading.Thread.Sleep%2A> 或 <xref:System.Threading.Thread.Suspend%2A> 方法暂停线程；通过使用 <xref:System.Threading.Thread.Resume%2A> 方法恢复挂起的线程，以及通过使用 <xref:System.Threading.Thread.Abort%2A> 方法销毁线程  
  
### <a name="thread-methods"></a>线程方法  
 下表显示了一些可用于控制各个线程的方法。  
  
|方法|操作|  
|------------|------------|  
|<xref:System.Threading.Thread.Start%2A>|使线程开始运行。|  
|<xref:System.Threading.Thread.Sleep%2A>|使线程暂停指定的一段时间。|  
|<xref:System.Threading.Thread.Suspend%2A>|线程到达某一安全点时暂停。|  
|<xref:System.Threading.Thread.Abort%2A>|线程到达某一安全点时停止。|  
|<xref:System.Threading.Thread.Resume%2A>|重新启动挂起的线程|  
|<xref:System.Threading.Thread.Join%2A>|使当前线程等待其他线程完成。 如果与超时值配合使用，当线程在分配的时间内完成时，此方法会返回 `True`。|  
  
### <a name="safe-points"></a>安全点  
 这些方法中的大多数都明白易晓，但可能对安全点这一概念会比较陌生。 安全点是代码中的位置，公共语言运行时可在其中安全执行自动垃圾回收（释放未使用的变量并回收内存的过程）。 调用线程的 <xref:System.Threading.Thread.Abort%2A> 或 <xref:System.Threading.Thread.Suspend%2A> 方法时，公共语言运行时将分析代码并确定线程停止运行的合适位置。  
  
### <a name="thread-properties"></a>线程属性  
 线程还包含多个有用的属性，如下表中所示：  
  
|属性|值|  
|--------------|-----------|  
|<xref:System.Threading.Thread.IsAlive%2A>|如果线程处于活动状态，将包含值 `True`。|  
|<xref:System.Threading.Thread.IsBackground%2A>|获取或设置布尔值，该值指示线程是否为或应为后台线程。 后台线程类似前台线程，但后台线程不会阻止进程停止。 属于某个进程的所有前台线程均停止后，公共语言运行时通过对仍处于活动状态的后台进程调用 <xref:System.Threading.Thread.Abort%2A> 方法来结束进程。|  
|<xref:System.Threading.Thread.Name%2A>|获取或设置线程的名称。 最常用于在调试时查找各个线程。|  
|<xref:System.Threading.Thread.Priority%2A>|获取或设置由操作系统用来确定线程计划优先顺序的值。|  
|<xref:System.Threading.Thread.ThreadState%2A>|包含描述线程状态的值。|  
  
## <a name="thread-priorities"></a>线程优先级  
 每个线程都具有优先级属性，用来确定线程必须执行的一段处理器时间的大小。 操作系统向高优先级线程分配较长时间段。而向低优先级线程分配较短时间段。 新线程是使用 `Normal` 的值创建的，但可将 <xref:System.Threading.Thread.Priority%2A> 属性更改为 <xref:System.Threading.ThreadPriority> 枚举中的任何值。  
  
 有关各个线程优先级的详细说明，请参阅 <xref:System.Threading.ThreadPriority>。  
  
## <a name="foreground-and-background-threads"></a>前台和后台线程  
 前台线程可无限制地运行，而后台线程将在最后一个前台线程停止后立即停止。 可以使用 <xref:System.Threading.Thread.IsBackground%2A> 属性来确定或更改线程的后台状态。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Threading.Thread>   
 [线程同步 (C#)](../../../../csharp/programming-guide/concepts/threading/thread-synchronization.md)   
 [多线程过程的参数和返回值 (C#)](../../../../csharp/programming-guide/concepts/threading/parameters-and-return-values-for-multithreaded-procedures.md)   
 [线程处理 [C#]](../../../../csharp/programming-guide/concepts/threading/index.md)

