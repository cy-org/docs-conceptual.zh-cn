---
title: "Foreground and Background Threads | Microsoft Docs"
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
  - "threading [.NET Framework], foreground"
  - "threading [.NET Framework], background"
  - "foreground threads"
  - "background threads"
ms.assetid: cfe0d632-dd35-47e0-91ad-f742a444005e
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Foreground and Background Threads
托管线程或者是后台线程，或者是前台线程。  后台线程不会使托管执行环境处于运行状态，除此之外，后台线程与前台线程是一样的。  一旦所有前台线程在托管进程（其中 .exe 文件是托管程序集）中被停止，系统将停止所有后台线程并关闭。  
  
> [!NOTE]
>  当运行时因为进程关闭而停止某个后台线程时，不会在该线程中引发异常。  但是，当线程是因为 <xref:System.AppDomain.Unload%2A?displayProperty=fullName> 方法卸载应用程序域而停止时，将同时在后台和前台线程中引发 <xref:System.Threading.ThreadAbortException>。  
  
 可使用 <xref:System.Threading.Thread.IsBackground%2A?displayProperty=fullName> 属性确定线程是后台线程还是前台线程，或更改其状态。  通过将其 <xref:System.Threading.Thread.IsBackground%2A> 属性设置为 `true`，可在任何时候将线程更改为后台线程。  
  
> [!IMPORTANT]
>  线程的前台或后台状态不影响线程中未经处理的异常的结果。  在 .NET Framework 2.0 版中，前台或后台线程中的未经处理的异常都将导致应用程序终止。  请参见 [Exceptions in Managed Threads](../../../docs/standard/threading/exceptions-in-managed-threads.md)。  
  
 属于托管线程池的线程（即其 <xref:System.Threading.Thread.IsThreadPoolThread%2A> 属性为 `true` 的线程）是后台线程。  从非托管代码进入托管执行环境的所有线程都被标记为后台线程。  通过创建并启动新的 <xref:System.Threading.Thread> 对象而生成的所有线程都默认为前台线程。  
  
 如果使用一个线程监视活动（例如套接字连接），请将其 <xref:System.Threading.Thread.IsBackground%2A> 属性设置为 `true`，以便该线程不会阻止进程终止。  
  
## 请参阅  
 <xref:System.Threading.Thread.IsBackground%2A?displayProperty=fullName>   
 <xref:System.Threading.Thread>   
 <xref:System.Threading.ThreadAbortException>