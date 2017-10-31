---
title: "Cleaning Up Unmanaged Resources | Microsoft Docs"
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
  - "Close method"
  - "Dispose method"
  - "garbage collector"
  - "garbage collection, unmanaged resources"
  - "cleanup operations"
  - "explicit cleanups"
  - "unmanaged resource cleanup"
  - "Finalize method"
ms.assetid: a17b0066-71c2-4ba4-9822-8e19332fc213
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# Cleaning Up Unmanaged Resources
对于应用创建的大多数对象，可以依赖 .NET Framework 的垃圾回收器来处理内存管理。  但是，如果创建包括非托管资源的对象，则当你在应用中使用完非托管资源后，必须显式释放这些资源。  最常用的非托管资源类型是包装操作系统资源的对象，如文件、窗口、网络连接或数据库连接。  虽然垃圾回收器可以跟踪封装非托管资源的对象的生存期，但无法了解如何发布并清理这些非托管资源。  
  
 如果你的类型使用非托管资源，则应执行以下操作：  
  
-   实现[释放模式](../../../docs/standard/design-guidelines/dispose-pattern.md)。  这要求你提供 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 实现以启用非托管资源的确定性释放。  当不再需要此对象（或其使用的资源）时，类型使用者可调用 <xref:System.IDisposable.Dispose%2A>。  <xref:System.IDisposable.Dispose%2A> 方法立即释放非托管资源。  
  
-   在类型使用者忘记调用 <xref:System.IDisposable.Dispose%2A> 的情况下，准备释放非托管资源。  可通过两种方法实现此目的：  
  
    -   使用安全句柄包装非托管资源。  这是推荐采用的方法。  安全句柄派生自 <xref:System.Runtime.InteropServices.SafeHandle?displayProperty=fullName> 类并包含可靠的 <xref:System.Object.Finalize%2A> 方法。  在使用安全句柄时，只需实现 <xref:System.IDisposable> 接口并在 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 实现中调用安全句柄的 <xref:System.Runtime.InteropServices.SafeHandle.Dispose%2A> 方法。  如果未调用安全句柄的 <xref:System.IDisposable.Dispose%2A> 方法，则垃圾回收器将自动调用安全句柄的终结器。  
  
         \- 或 \-  
  
    -   重写 <xref:System.Object.Finalize%2A?displayProperty=fullName> 方法。  当类型使用者无法调用 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 以确定性地释放非托管资源时，终止会启用对非托管资源的非确定性释放。  但是，由于对象终止是一项复杂且易出错的操作，建议你使用安全句柄而不是提供你自己的终结器。  
  
 然后，类型使用者可直接调用 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 实现以释放非托管资源使用的内存。  在正确实现 <xref:System.IDisposable.Dispose%2A> 方法时，安全句柄的 <xref:System.Object.Finalize%2A> 方法或 <xref:System.Object.Finalize%2A?displayProperty=fullName> 方法的重写会在未调用 <xref:System.IDisposable.Dispose%2A> 方法的情况下阻止清理资源。  
  
## 本节内容  
 [Implementing a Dispose Method](../../../docs/standard/garbage-collection/implementing-dispose.md)  
 描述如何实现用于释放非托管资源的[释放模式](../../../docs/standard/design-guidelines/dispose-pattern.md)。  
  
 [Using Objects That Implement IDisposable](../../../docs/standard/garbage-collection/using-objects.md)  
 描述类型使用者如何确保调用其 <xref:System.IDisposable.Dispose%2A> 实现。  建议使用 C\# `using` 语句或 Visual Basic `Using` 语句来执行此操作。  
  
## 参考  
 <xref:System.IDisposable?displayProperty=fullName>  
 定义用于释放非托管资源的 <xref:System.IDisposable.Dispose%2A> 方法。  
  
 <xref:System.Object.Finalize%2A?displayProperty=fullName>  
 如果 <xref:System.IDisposable.Dispose%2A> 方法未释放非托管资源，则准备对象终止。  
  
 <xref:System.GC.SuppressFinalize%2A?displayProperty=fullName>  
 取消终止。  通常，从 `Dispose` 方法调用此方法来阻止执行终结器。