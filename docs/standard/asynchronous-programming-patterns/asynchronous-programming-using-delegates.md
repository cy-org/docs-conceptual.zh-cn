---
title: "Asynchronous Programming Using Delegates | Microsoft Docs"
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
  - "BeginInvoke method"
  - "asynchronous programming, delegates"
  - "asynchronous delegates"
  - "calling synchronous methods in asynchronous manner"
  - "EndInvoke method"
  - "calling asynchronous methods"
  - "delegates [.NET Framework], asynchronous"
  - "synchronous calling in asynchronous manner"
ms.assetid: 38a345ca-6963-4436-9608-5c9defef9c64
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Asynchronous Programming Using Delegates
使用委托可以通过异步方式调用同步方法。  当同步调用一个委托时，`Invoke` 方法直接对当前线程调用目标方法。  如果调用 `BeginInvoke` 方法，则公共语言运行时 \(CLR\) 会对请求进行排队并立即返回到调用方。  会对来自线程池的线程异步调用目标方法。  提交请求的原始线程自由地继续与目标方法并行执行。  如果在对 `BeginInvoke` 方法的调用中指定了回调方法，则当目标方法结束时将调用该回调方法。  在回调方法中，`EndInvoke` 方法获取返回值和所有输入\/输出参数或仅供输出参数。  如果在调用 `BeginInvoke` 时未指定任何回调方法，则可以从调用 `BeginInvoke` 的线程中调用 `EndInvoke`。  
  
> [!IMPORTANT]
>  编译器应使用由用户指定的委托签名发出具有 `Invoke`、`BeginInvoke` 和 `EndInvoke` 方法的委托类。  应将 `BeginInvoke` 和 `EndInvoke` 方法修饰为本机方法。  因为这些方法被标记为本机的，所以 CLR 在类加载时自动提供该实现。  加载程序确保它们未被重写。  
  
## 本节内容  
 [Calling Synchronous Methods Asynchronously](../../../docs/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)  
 讨论如何使用委托对普通方法进行异步调用，并提供简单的代码示例演示等待异步调用返回的四种方法。  
  
 [异步委托编程示例](../Topic/Asynchronous%20Delegates%20Programming%20Sample.md)  
 通过一个更加复杂的代码示例（求解数字的因数）演示如何使用委托进行异步调用。  
  
## 相关章节  
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)  
 描述如何通过 .NET Framework 进行异步编程。  
  
## 请参阅  
 <xref:System.Delegate>