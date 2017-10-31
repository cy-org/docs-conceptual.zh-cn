---
title: "Mutexes | Microsoft Docs"
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
  - "wait handles"
  - "threading [.NET Framework], Mutex class"
  - "Mutex class, about Mutex class"
  - "threading [.NET Framework], cross-process synchronization"
ms.assetid: 9dd06e25-12c0-4a9e-855a-452dc83803e2
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Mutexes
可以使用 <xref:System.Threading.Mutex> 对象提供对资源的独占访问。  <xref:System.Threading.Mutex> 类比 <xref:System.Threading.Monitor> 类使用更多系统资源，但是它可以跨应用程序域边界进行封送处理，可用于多个等待，并且可用于同步不同进程中的线程。  有关托管同步机制的比较，请参见 [Overview of Synchronization Primitives](../../../docs/standard/threading/overview-of-synchronization-primitives.md)。  
  
 有关代码示例，请参见 <xref:System.Threading.Mutex.%23ctor%2A> 构造函数的参考文档。  
  
## 使用 Mutex  
 线程调用 mutex 的 <xref:System.Threading.WaitHandle.WaitOne%2A> 方法请求所有权。  该调用会一直阻塞到 mutex 可用，或直至达到可选的超时间隔。  如果没有任何线程拥有它，则 Mutex 的状态为已发信号的状态。  
  
 线程通过调用其 <xref:System.Threading.Mutex.ReleaseMutex%2A> 方法释放 mutex。  mutex 具有线程关联；即 mutex 只能由拥有它的线程释放。  如果线程释放不是它拥有的 mutex，则会在该线程中引发 <xref:System.ApplicationException>。  
  
 由于 <xref:System.Threading.Mutex> 类从 <xref:System.Threading.WaitHandle> 派生，所以您还可以结合其他等待句柄调用 <xref:System.Threading.WaitHandle> 的静态 <xref:System.Threading.WaitHandle.WaitAll%2A> 或 <xref:System.Threading.WaitHandle.WaitAny%2A> 方法请求 <xref:System.Threading.Mutex> 的所有权。  
  
 如果某个线程拥有 <xref:System.Threading.Mutex>，则该线程就可以在重复的等待\-请求调用中指定同一个 <xref:System.Threading.Mutex>，而不必阻止其执行；但是，它必须释放 <xref:System.Threading.Mutex>，次数与释放所属权的次数相同。  
  
## 被放弃的 Mutex  
 如果线程终止而未释放 <xref:System.Threading.Mutex>，则认为该 mutex 已放弃。  这通常指示存在严重的编程错误，因为该 mutex 正在保护的资源可能会处于不一致的状态。  在 .NET Framework 2.0 版中，获取该 mutex 的下一个线程中将引发 <xref:System.Threading.AbandonedMutexException>。  
  
> [!NOTE]
>  在 .NET Framework 1.0 和 1.1 版中，放弃的 <xref:System.Threading.Mutex> 被设置为已发送信号状态，下一个等待线程将获得所有权。  如果没有等待线程，则 <xref:System.Threading.Mutex> 保持已发送信号状态。  不引发异常。  
  
 对于系统范围的 mutex，被放弃的 mutex 可能指示应用程序已突然终止（例如，通过使用 Windows 任务管理器终止）。  
  
## 本地 mutex 和系统 mutex  
 Mutex 分两种类型：本地 mutex 和命名系统 mutex。  如果使用接受名称的构造函数创建了 <xref:System.Threading.Mutex> 对象，那么该对象将与具有该名称的操作系统对象相关联。  命名的系统 mutex 在整个操作系统中都可见，并且可用于同步进程活动。  您可以创建多个 <xref:System.Threading.Mutex> 对象来表示同一命名系统 mutex，而且您可以使用 <xref:System.Threading.Mutex.OpenExisting%2A> 方法打开现有的命名系统 mutex。  
  
 本地 mutex 仅存在于进程当中。  进程中引用本地 <xref:System.Threading.Mutex> 对象的任意线程都可以使用本地 mutex。  每个 <xref:System.Threading.Mutex> 对象都是一个单独的本地 mutex。  
  
### 系统 mutex 的访问控制安全性  
 .NET Framework 2.0 版提供查询和设置命名的系统对象的 Windows 访问控制安全性的能力。  建议从创建那一刻起就开始保护系统 mutex，因为系统对象是全局对象，因此可能被您自己的代码以外的代码锁定。  
  
 有关 mutex 的访问控制安全性的信息，请参见 <xref:System.Security.AccessControl.MutexSecurity> 和 <xref:System.Security.AccessControl.MutexAccessRule> 类、<xref:System.Security.AccessControl.MutexRights> 枚举、<xref:System.Threading.Mutex> 类的 <xref:System.Threading.Mutex.GetAccessControl%2A>、<xref:System.Threading.Mutex.SetAccessControl%2A> 和 <xref:System.Threading.Mutex.OpenExisting%2A> 方法以及 <xref:System.Threading.Mutex.%23ctor%28System.Boolean%2CSystem.String%2CSystem.Boolean%40%2CSystem.Security.AccessControl.MutexSecurity%29> 构造函数。  
  
## 请参阅  
 <xref:System.Threading.Mutex>   
 <xref:System.Threading.Mutex.%23ctor%2A>   
 <xref:System.Security.AccessControl.MutexSecurity>   
 <xref:System.Security.AccessControl.MutexAccessRule>   
 [Threading](../../../docs/standard/threading/index.md)   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)   
 [监视器](../Topic/Monitors.md)   
 [Threads and Threading](../../../docs/standard/threading/threads-and-threading.md)