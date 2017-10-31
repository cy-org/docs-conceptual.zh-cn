---
title: "如何：实现提供程序 | Microsoft Docs"
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
  - "观察程序设计模式 [.NET Framework]，实现提供程序"
  - "提供程序 [.NET Framework]，在观察程序设计模式中"
  - "可观察对象 [.NET Framework]，在观察程序设计模式中"
ms.assetid: 790b5d8b-d546-40a6-beeb-151b574e5ee5
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：实现提供程序
观察者设计模式要求在提供程序（监视数据和发送通知）和一个或多个观察者（接收提供程序的通知，即回调）之间进行区分。  本主题讨论如何创建提供程序。  相关主题[如何：实现观察程序](../../../docs/standard/events/how-to-implement-an-observer.md)讨论如何创建观察者。  
  
### 创建提供程序  
  
1.  定义提供程序负责发送给观察者的数据。  尽管提供程序和它发送给观察者的数据可以为一个类型，但是通常它们都采用不同的类型表示。  例如，在温度监控应用程序中，`Temperature` 结构定义提供程序（由下一步中定义的 `TemperatureMonitor` 类表示）监控的数据和观察者订阅的数据。  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/data.cs#1)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/data.vb#1)]  
  
2.  定义数据提供程序，这是实现 <xref:System.IObservable%601?displayProperty=fullName> 接口的类型。  提供程序的泛型类型参数是提供程序发送给观察者的类型。  下面的示例定义了一个 `TemperatureMonitor` 类，它是具有 `Temperature` 泛型类型参数的构造 <xref:System.IObservable%601?displayProperty=fullName> 实现。  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#2)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#2)]  
  
3.  确定提供程序存储观察者引用的方式，以便每个观察者都能在适当的时候得到通知。  最常用于此目的是集合对象，如泛型 <xref:System.Collections.Generic.List%601> 对象。  下面的示例定义了一个专用的 <xref:System.Collections.Generic.List%601> 对象，它在 `TemperatureMonitor` 类构造函数中实例化。  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#3)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#3)]  
  
4.  定义提供程序可以返回至订阅者的 <xref:System.IDisposable> 实现，以便它们能够随时停止接收通知。  下面的示例定义了一个嵌套的 `Unsubscriber` 类，在实例化类时，会向该类传递对订阅者集合和订阅者的引用。  此代码允许订阅者调用对象的 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 实现，以将其自身从订阅者集合中移除。  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#4)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#4)]  
  
5.  实现 <xref:System.IObservable%601.Subscribe%2A?displayProperty=fullName> 方法。  将向该方法传递对 <xref:System.IObserver%601?displayProperty=fullName> 接口的引用，并且该方法应存储在步骤 3 中为该目的而设计的对象中。  然后，该方法应该返回步骤 4 中开发的 <xref:System.IDisposable> 实现。  下面的示例演示 `TemperatureMonitor` 类中 <xref:System.IObservable%601.Subscribe%2A> 方法的实现。  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#5)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#5)]  
  
6.  通过调用观察者的 <xref:System.IObserver%601.OnNext%2A?displayProperty=fullName>、<xref:System.IObserver%601.OnError%2A?displayProperty=fullName> 和 <xref:System.IObserver%601.OnCompleted%2A?displayProperty=fullName> 实现，根据需要通知观察者。  在某些情况下，提供程序在发生错误时可能不会调用 <xref:System.IObserver%601.OnError%2A> 方法。  例如，下面的 `GetTemperature` 方法模拟一个监视器，它每五秒读取一次温度数据，并对照之前的读数，如果温度的变化大于或等于 0.1 度则通知观察者。  如果设备不报告温度（即其值为 null），则提供程序会通知观察者传输已完成。  请注意，除调用每个观察者的 <xref:System.IObserver%601.OnCompleted%2A> 方法外，`GetTemperature` 方法还会清除 <xref:System.Collections.Generic.List%601> 集合。  在这种情况下，提供程序不调用其观察者的 <xref:System.IObserver%601.OnError%2A> 方法。  
  
     [!code-csharp[Conceptual.ObserverDesign.HowTo#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#6)]
     [!code-vb[Conceptual.ObserverDesign.HowTo#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#6)]  
  
## 示例  
 下面的示例包含定义温度监控应用程序的 <xref:System.IObservable%601> 实现的完整源代码。  它包括 `Temperature` 结构（发送给观察者的数据）和 `TemperatureMonitor` 类（即 <xref:System.IObservable%601> 实现）。  
  
 [!code-csharp[Conceptual.ObserverDesign.HowTo#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.observerdesign.howto/cs/provider.cs#7)]
 [!code-vb[Conceptual.ObserverDesign.HowTo#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.observerdesign.howto/vb/provider.vb#7)]  
  
## 请参阅  
 <xref:System.IObservable%601>   
 [观察程序设计模式](../../../docs/standard/events/observer-design-pattern.md)   
 [如何：实现观察程序](../../../docs/standard/events/how-to-implement-an-observer.md)   
 [观察程序设计模式最佳做法](../../../docs/standard/events/observer-design-pattern-best-practices.md)