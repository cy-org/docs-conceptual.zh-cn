---
title: "EventWaitHandle | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "threading [.NET Framework], EventWaitHandle class"
  - "EventWaitHandle class"
  - "event wait handles [.NET Framework]"
  - "threading [.NET Framework], cross-process synchronization"
ms.assetid: 11ee0b38-d663-4617-b793-35eb6c64e9fc
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# EventWaitHandle
<xref:System.Threading.EventWaitHandle> 类允许线程通过发出信号和等待信号来互相通信。  事件等待句柄（简称事件）就是可以通过发出相应的信号来释放一个或多个等待线程的等待句柄。  信号发出后，可以用手动或自动方式重置事件等待句柄。  <xref:System.Threading.EventWaitHandle> 类既可以表示本地事件等待句柄（本地事件），也可以表示命名系统事件等待句柄（命名事件或系统事件，对所有进程可见）。  
  
> [!NOTE]
>  事件等待句柄不是 .NET Framework 中通常所指的事件。  它不涉及任何委托或事件处理程序。  之所以用“事件”一词来描述它们，一是因为人们习惯上将它们称为操作系统事件，二是因为发出等待句柄信号的行为提示等待线程发生了一个事件。  
  
 本地和命名事件等待句柄都使用系统同步对象，<xref:Microsoft.Win32.SafeHandles.SafeWaitHandle> 包装保护着这些对象以确保资源的释放。  使用完对象后，您可以使用 <xref:System.Threading.WaitHandle.System%23IDisposable%23Dispose%2A> 方法立即释放资源。  
  
## 自动重置的事件等待句柄  
 您可以通过在创建 <xref:System.Threading.EventWaitHandle> 对象时指定 <xref:System.Threading.EventResetMode?displayProperty=fullName> 来创建自动重置事件。  顾名思义，在释放一个等待线程后，此同步事件会在发出相应的信号时自动重置。  应通过调用事件的 <xref:System.Threading.EventWaitHandle.Set%2A> 方法来发出事件信号。  
  
 自动重置事件通常用来一次为一个线程提供对资源的独占访问。  线程通过调用 <xref:System.Threading.WaitHandle.WaitOne%2A> 方法来请求资源。  如果没有其他线程持有等待句柄，该方法会返回 `true`，同时调用线程会掌握对资源的控制。  
  
> [!IMPORTANT]
>  与所有同步机制一样，您必须确保在访问受保护的资源之前所有代码路径都在正确的等待句柄上等待。  线程同步具有互操作性。  
  
 如果在没有线程等待时发出自动重置事件信号，则该信号将一直保留到有一个线程尝试在其上等待为止。  然后，该事件释放线程并立即重置，这会阻止后面的线程。  
  
## 手动重置的事件等待句柄  
 通过在创建 <xref:System.Threading.EventWaitHandle> 对象时指定 <xref:System.Threading.EventResetMode?displayProperty=fullName> 可以创建手动重置事件。  顾名思义，此同步事件必须在发出其事件信号后手动重置。  在它重置之前，通过调用其 <xref:System.Threading.EventWaitHandle.Reset%2A> 方法便可以重置它，从而使在该事件句柄上等待的线程立即继续而不受阻止。  
  
 手动重置事件就像马棚的门。  当未发出事件信号时，会阻止在其上等待的线程，就像阻拦马棚中的马。  通过调用事件的 <xref:System.Threading.EventWaitHandle.Set%2A> 方法发出事件信号时，所有等待的线程都可以继续了。  在调用事件的 <xref:System.Threading.EventWaitHandle.Reset%2A> 方法前，一直会发出事件信号。  这使得手动重置事件成了阻止在某一线程完成任务之前需等待的线程的理想方式。  
  
 如同让马离开马棚一样，操作系统需要时间来安排释放的线程并让它们恢复执行。  如果在所有线程恢复执行之前调用了 <xref:System.Threading.EventWaitHandle.Reset%2A> 方法，则剩余的线程会再次阻止。  哪些线程恢复执行？哪些线程阻止？这取决于一些随机因素，例如系统上的负载、等待计划程序的线程数等等。  如果发出事件信号的线程在发出信号之后结束（这是最常见使用模式），这就不是问题了。  如果您要发出事件信号的线程在所有等待线程恢复执行之后开始新任务，则您必须阻止它，直到所有等待线程恢复执行为止。  否则，将出现争用条件，而且您的代码的行为将不可预测。  
  
## 自动和手动事件的通用功能  
 通常，<xref:System.Threading.EventWaitHandle> 上会有一个或多个线程被阻止到未阻止的线程调用 <xref:System.Threading.EventWaitHandle.Set%2A> 方法时，此方法然后会释放其中的一个等待线程（如果是自动重置事件）或所有的等待线程（如果是手动重置事件）。  线程可以发出 <xref:System.Threading.EventWaitHandle> 信号，然后通过调用静态 <xref:System.Threading.WaitHandle.SignalAndWait%2A?displayProperty=fullName> 方法阻止该事件等待句柄，这就像原子操作一样。  
  
 <xref:System.Threading.EventWaitHandle> 对象可与静态 <xref:System.Threading.WaitHandle.WaitAll%2A?displayProperty=fullName> 和 <xref:System.Threading.WaitHandle.WaitAny%2A?displayProperty=fullName> 方法一起使用。  因为 <xref:System.Threading.EventWaitHandle> 和 <xref:System.Threading.Mutex> 类都派生自 <xref:System.Threading.WaitHandle>，您可以将这两个类与这些方法一起使用。  
  
### 命名事件  
 Windows 操作系统允许事件等待句柄具有名称。  命名事件是系统级的事件。  即，创建命名事件后，它对所有进程中的所有线程都是可见的。  因此，命名事件可用于同步进程的活动以及线程的活动。  
  
 您可以使用一个能够指定事件名称的构造函数来创建表示命名系统事件的 <xref:System.Threading.EventWaitHandle> 对象。  
  
> [!NOTE]
>  因为命名事件是系统级的事件，所以可以有多个表示相同命名事件的 <xref:System.Threading.EventWaitHandle> 对象。  每当调用构造函数或 <xref:System.Threading.EventWaitHandle.OpenExisting%2A> 方法时，都会创建一个新的 <xref:System.Threading.EventWaitHandle> 对象。  重复指定相同名称会创建多个表示相同命名事件的对象。  
  
 使用命名事件时要小心。  因为它们是系统级的事件，所以使用同一名称的其他进程可能会意外地阻止您的线程。  在同一计算机上执行的恶意代码可能以此作为一个切入点来发动拒绝服务攻击。  
  
 应使用访问控制安全机制来保护表示命名事件的 <xref:System.Threading.EventWaitHandle> 对象，最好通过使用可用于指定 <xref:System.Security.AccessControl.EventWaitHandleSecurity> 对象的构造函数来实施保护。  您还可以使用 <xref:System.Threading.EventWaitHandle.SetAccessControl%2A> 方法来应用访问控制安全，但这一做法会在事件等待句柄的创建时间和受保护时间之间留出一段漏洞时间。  使用访问控制安全机制来保护事件可帮助阻止恶意攻击，但无法解决意外发生的名称冲突问题。  
  
> [!NOTE]
>  与 <xref:System.Threading.EventWaitHandle> 类不同，派生类 <xref:System.Threading.AutoResetEvent> 和 <xref:System.Threading.ManualResetEvent> 只能表示本地等待句柄。  它们不能表示命名系统事件。  
  
## 请参阅  
 <xref:System.Threading.EventWaitHandle>   
 <xref:System.Threading.WaitHandle>   
 <xref:System.Threading.AutoResetEvent>   
 <xref:System.Threading.ManualResetEvent>   
 [EventWaitHandle, AutoResetEvent, CountdownEvent, ManualResetEvent](../../../docs/standard/threading/eventwaithandle-autoresetevent-countdownevent-manualresetevent.md)