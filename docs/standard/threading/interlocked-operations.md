---
title: "Interlocked Operations | Microsoft Docs"
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
  - "Interlocked class, about Interlocked class"
  - "threading [.NET Framework], Interlocked class"
ms.assetid: cbda7114-c752-4f3e-ada1-b1e8dd262f2b
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# Interlocked Operations
<xref:System.Threading.Interlocked> 类提供这样一些方法，即同步对多个线程共享的变量的访问的方法。  如果该变量位于共享内存中，则不同进程的线程就可以使用该机制。  互锁操作是原子的，即整个操作是不能由相同变量上的另一个互锁操作所中断的单元。  这在抢先多线程操作系统中是很重要的，在这样的操作系统中，线程可以在从某个内存地址加载值之后但是在有机会更改和存储该值之前被挂起。  
  
 <xref:System.Threading.Interlocked> 类提供了以下操作：  
  
-   在 .NET Framework 2.0 版中，<xref:System.Threading.Interlocked.Add%2A> 方法向变量添加一个整数值并返回该变量的新值。  
  
-   在 .NET Framework 2.0 版中，<xref:System.Threading.Interlocked.Read%2A> 方法作为一个原子操作读取一个 64 位整数值。  这在 32 位操作系统上是有用的，在 32 位操作系统上，读取一个 64 位整数通常不是一个原子操作。  
  
-   <xref:System.Threading.Interlocked.Increment%2A> 和 <xref:System.Threading.Interlocked.Decrement%2A> 方法递增或递减某个变量并返回结果值。  
  
-   <xref:System.Threading.Interlocked.Exchange%2A> 方法执行指定的变量中的值的原子交换，返回该值并将其替换为新值。  在 .NET Framework 2.0 版中，可以使用此方法的一个泛型重载在任何引用类型的变量上执行此交换。  请参见<xref:System.Threading.Interlocked.Exchange%60%601%28%60%600%40%2C%60%600%29>。  
  
-   <xref:System.Threading.Interlocked.CompareExchange%2A> 方法也交换两个值，但是视比较的结果而定。  在 .NET Framework 2.0 版中，可以使用此方法的一个泛型重载在任何引用类型的变量上执行此交换。  请参见<xref:System.Threading.Interlocked.CompareExchange%60%601%28%60%600%40%2C%60%600%2C%60%600%29>。  
  
 在现代处理器中，<xref:System.Threading.Interlocked> 类的方法经常可以由单个指令来实现。  因此，它们提供性能非常高的同步，并且可用于构建更高级的同步机制，例如自旋锁。  
  
 有关结合使用 <xref:System.Threading.Monitor> 和 <xref:System.Threading.Interlocked> 类的示例，请参见 [监视器](../Topic/Monitors.md)。  
  
## CompareExchange 示例  
 <xref:System.Threading.Interlocked.CompareExchange%2A> 方法可用来保护比简单的递增和递减更为复杂的计算。  下面的示例演示一个线程安全的方法，该方法向存储为浮点数的累计值执行加运算。（对于整数，<xref:System.Threading.Interlocked.Add%2A> 方法是更简单的解决方案。）有关完整的代码示例，请参见接受单精度和双精度浮点参数（<xref:System.Threading.Interlocked.CompareExchange%28System.Single%40%2CSystem.Single%2CSystem.Single%29> 和 <xref:System.Threading.Interlocked.CompareExchange%28System.Double%40%2CSystem.Double%2CSystem.Double%29>）的 <xref:System.Threading.Interlocked.CompareExchange%2A> 的重载。  
  
 [!code-cpp[Conceptual.Interlocked#1](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interlocked/cpp/source1.cpp#1)]
 [!code-csharp[Conceptual.Interlocked#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interlocked/cs/source1.cs#1)]
 [!code-vb[Conceptual.Interlocked#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interlocked/vb/source1.vb#1)]  
  
## Exchange 和 CompareExchange 的非类型化重载  
 <xref:System.Threading.Interlocked.Exchange%2A> 和 <xref:System.Threading.Interlocked.CompareExchange%2A> 方法具有接受 <xref:System.Object> 类型的参数的重载。  这其中每个重载的第一个参数都是 `ref Object`（在 Visual Basic 中为 `ByRef … As Object`），类型安全要求将传递给此参数的变量严格类型化为 <xref:System.Object>；不能在调用这些方法时简单地将第一个参数强制转换为 <xref:System.Object> 类型。  
  
> [!NOTE]
>  在 .NET Framework 2.0 版中，使用 <xref:System.Threading.Interlocked.Exchange%2A> 和 <xref:System.Threading.Interlocked.CompareExchange%2A> 方法的泛型重载交换强类型变量。  
  
 下面的代码示例演示一个只能设置一次的 `ClassA` 类型的属性，就如它在 .NET Framework 1.0 或 1.1 版中实现那样。  
  
 [!code-cpp[Conceptual.Interlocked#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.interlocked/cpp/source2.cpp#2)]
 [!code-csharp[Conceptual.Interlocked#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.interlocked/cs/source2.cs#2)]
 [!code-vb[Conceptual.Interlocked#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.interlocked/vb/source2.vb#2)]  
  
## 请参阅  
 <xref:System.Threading.Interlocked>   
 <xref:System.Threading.Monitor>   
 [Threading](../../../docs/standard/threading/index.md)   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)