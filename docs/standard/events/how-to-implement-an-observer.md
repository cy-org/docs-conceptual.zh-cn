---
title: "如何：实现观察程序 | Microsoft Docs"
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
  - "观察程序 [.NET Framework]，观察程序设计模式"
  - "观察程序设计模式 [.NET Framework]，实现观察程序"
ms.assetid: 8ecfa9f5-b500-473d-bcf0-5652ffb1e53d
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：实现观察程序
观察者设计模式要求在观察者（注册通知）和提供程序（监视数据并将通知发送至一个或多个观察者）之间插入分隔符。  本主题讨论如何创建观察者。  相关主题[如何：实现提供程序](../../../docs/standard/events/how-to-implement-a-provider.md)讨论如何创建提供程序。  
  
### 创建观察者  
  
1.  定义作为实现 <xref:System.IObserver%601?displayProperty=fullName> 接口的类型的观察者。  例如，下面的代码定义一个名为 `TemperatureReporter` 的类型，它是使用 `Temperature` 泛型类型参数构造的 <xref:System.IObserver%601?displayProperty=fullName> 实现。  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#8)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#8)]  
  
2.  如果观察者可以在提供程序调用其 <xref:System.IObserver%601.OnCompleted%2A?displayProperty=fullName> 实现之前停止接收通知，请定义保留提供程序的 <xref:System.IObservable%601.Subscribe%2A?displayProperty=fullName> 方法返回的 <xref:System.IDisposable> 实现的私有变量。  还应定义调用提供程序的 <xref:System.IObservable%601.Subscribe%2A> 方法并存储返回的 <xref:System.IDisposable> 对象的订阅方法。  例如，下面的代码定义一个名为 `unsubscriber` 的私有变量，并定义一个调用提供程序的 <xref:System.IObservable%601.Subscribe%2A> 方法并将返回的对象指派给 `unsubscriber` 变量的 `Subscribe` 方法。  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#9)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#9)]  
  
3.  定义使观察者可以在提供程序调用其 <xref:System.IObserver%601.OnCompleted%2A?displayProperty=fullName> 实现之前停止接收通知的方法（如果需要此功能）。  下面的示例定义 `Unsubscribe` 方法。  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#10)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#10)]  
  
4.  提供由 <xref:System.IObserver%601> 接口定义的三种方法的实现：<xref:System.IObserver%601.OnNext%2A?displayProperty=fullName>、<xref:System.IObserver%601.OnError%2A?displayProperty=fullName> 和 <xref:System.IObserver%601.OnCompleted%2A?displayProperty=fullName>。  根据提供程序和应用程序的需求，<xref:System.IObserver%601.OnError%2A> 和 <xref:System.IObserver%601.OnCompleted%2A> 方法可以为存根实现。  注意，<xref:System.IObserver%601.OnError%2A> 方法不应将传递的 <xref:System.Exception> 对象作为异常处理，而 <xref:System.IObserver%601.OnCompleted%2A> 方法可以自由调用提供程序的 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 实现。  下面的示例演示 `TemperatureReporter` 类的 <xref:System.IObserver%601> 实现。  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#11)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#11)]  
  
## 示例  
 下面的示例包含 `TemperatureReporter` 类（提供温度监控应用程序的 <xref:System.IObserver%601> 实现）的完整源代码。  
  
 [!code-csharp[Conceptual.ObserverDesign.HowTo#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/observer.cs#12)]
 [!code-vb[Conceptual.ObserverDesign.HowTo#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/observer.vb#12)]  
  
## 请参阅  
 <xref:System.IObserver%601>   
 [观察程序设计模式](../../../docs/standard/events/observer-design-pattern.md)   
 [如何：实现提供程序](../../../docs/standard/events/how-to-implement-a-provider.md)   
 [观察程序设计模式最佳做法](../../../docs/standard/events/observer-design-pattern-best-practices.md)