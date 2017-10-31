---
title: "Destroying Threads | Microsoft Docs"
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
  - "destroying threads"
  - "threading [.NET Framework], destroying threads"
ms.assetid: df54e648-c5d1-47c9-bd29-8e4438c1db6d
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Destroying Threads
<xref:System.Threading.Thread.Abort%2A> 方法用于永久地停止托管线程。  调用 <xref:System.Threading.Thread.Abort%2A> 时，公共语言运行时在目标线程中引发 <xref:System.Threading.ThreadAbortException>，目标线程可捕捉此异常。  有关更多信息，请参见 <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName>。  
  
> [!NOTE]
>  如果调用线程的 <xref:System.Threading.Thread.Abort%2A> 方法时线程正在执行非托管代码，则运行时将其标记为 <xref:System.Threading.ThreadState?displayProperty=fullName>。  线程返回到托管代码时引发此异常。  
  
 一旦线程被中止，它将无法重新启动。  
  
 <xref:System.Threading.Thread.Abort%2A> 方法不直接导致线程中止，因为目标线程可捕捉 <xref:System.Threading.ThreadAbortException> 并在 `finally` 块中执行任意数量的代码。  如果需要等待线程结束，则可调用 <xref:System.Threading.Thread.Join%2A?displayProperty=fullName>。  <xref:System.Threading.Thread.Join%2A?displayProperty=fullName> 是一个阻塞调用，在线程实际停止执行之前或在可选的超时间隔结束之前，它不会返回。  中止的线程可调用 <xref:System.Threading.Thread.ResetAbort%2A> 方法，也可在 `finally` 块中执行无限处理，因此，如果不指定超时，则不能保证等待会结束。  
  
 等待对 <xref:System.Threading.Thread.Join%2A?displayProperty=fullName> 方法的调用的线程可由其他线程调用 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName> 来中断。  
  
## 处理 ThreadAbortException  
 如果希望中止线程，可以从您的代码中调用 <xref:System.Threading.Thread.Abort%2A>，也可以卸载线程运行时所在的应用程序域（<xref:System.AppDomain.Unload%2A?displayProperty=fullName> 使用 <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName> 终止线程），线程必须处理 <xref:System.Threading.ThreadAbortException> 并在 `finally` 子句中执行所有最终处理，如下面的代码所示。  
  
```vb  
Try  
    ' Code that is executing when the thread is aborted.  
Catch ex As ThreadAbortException  
    ' Clean-up code can go here.  
    ' If there is no Finally clause, ThreadAbortException is  
    ' re-thrown by the system at the end of the Catch clause.   
Finally  
    ' Clean-up code can go here.  
End Try  
' Do not put clean-up code here, because the exception   
' is rethrown at the end of the Finally clause.  
```  
  
```csharp  
try   
{  
    // Code that is executing when the thread is aborted.  
}   
catch (ThreadAbortException ex)   
{  
    // Clean-up code can go here.  
    // If there is no Finally clause, ThreadAbortException is  
    // re-thrown by the system at the end of the Catch clause.   
}  
// Do not put clean-up code here, because the exception   
// is rethrown at the end of the Finally clause.  
```  
  
 清理代码必须在 `catch` 子句或 `finally` 子句中，因为系统在 `finally` 子句的结尾处再次引发 <xref:System.Threading.ThreadAbortException>，如果没有 `finally` 子句，则在 `catch` 子句的结尾处再次引发该异常。  
  
 通过调用 <xref:System.Threading.Thread.ResetAbort%2A?displayProperty=fullName> 方法可以防止系统再次引发该异常。  但是，仅当您自己的代码引发 <xref:System.Threading.ThreadAbortException> 时，才应这样做。  
  
## 请参阅  
 <xref:System.Threading.ThreadAbortException>   
 <xref:System.Threading.Thread>   
 [Using Threads and Threading](../../../docs/standard/threading/using-threads-and-threading.md)