---
title: "Garbage Collection Notifications | Microsoft Docs"
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
  - "garbage collection, notifications"
ms.assetid: e12d8e74-31e3-4035-a87d-f3e66f0a9b89
caps.latest.revision: 23
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 23
---
# Garbage Collection Notifications
有一些解决方案，其中公共语言运行时执行的完整垃圾回收 \(也就是,第2代回收\)有时可能会对性能产生负面影响。  对于处理大量请求的服务器而言，此问题尤为突出；在这种情况下，长时间的垃圾回收可能会导致请求超时。  若要防止在重要时间段发生完整垃圾回收，可以让系统通知您即将发生完整垃圾回收，您可以采取措施将工作负荷重定向到其他服务器实例。  您也可以在当前服务器实例不需要处理请求时自己引发回收。  
  
 <xref:System.GC.RegisterForFullGCNotification%2A> 方法注册一个通知，当运行时察觉到即将发生完整垃圾回收时将引发该通知。  此通知包含两部分：何时将发生完整垃圾回收以及完整垃圾回收何时完成。  
  
> [!WARNING]
>  只阻止垃圾回收应引发通知。  在 [\<gcConcurrent\>](../../../docs/framework/configure-apps/file-schema/runtime/gcconcurrent-element.md) 配置元素启用，后台垃圾回收不会发出通知。  
  
 若要确定何时引发了通知，请使用 <xref:System.GC.WaitForFullGCApproach%2A> 和 <xref:System.GC.WaitForFullGCComplete%2A> 方法。  通常，可在 `while` 循环中使用这些方法来持续获取显示通知状态的 <xref:System.GCNotificationStatus> 枚举。  如果该值为 <xref:System.GCNotificationStatus>，则可以执行以下操作：  
  
-   为了响应使用 <xref:System.GC.WaitForFullGCApproach%2A> 方法获取的通知，可以重定向工作负荷并可以自己引发回收。  
  
-   为了响应使用 <xref:System.GC.WaitForFullGCComplete%2A> 方法获取的通知，可以使当前服务器实例再次可用于处理请求。  还可以收集信息。  例如，可以使用 <xref:System.GC.CollectionCount%2A> 方法记录回收次数。  
  
 <xref:System.GC.WaitForFullGCApproach%2A> 和 <xref:System.GC.WaitForFullGCComplete%2A> 方法应一起使用。  只使用其中一个方法可能导致不确定的结果。  
  
## 完整垃圾回收  
 在发生以下任何一种情况时，运行时进行完整垃圾回收：  
  
-   提升至第 2 级的内存量已经足以进行下一次第 2 级回收。  
  
-   提升至大对象堆的内存量已经足以进行下一次第 2 级回收。  
  
-   其他原因导致第 1 级回收提升至第 2 级回收。  
  
 在 <xref:System.GC.RegisterForFullGCNotification%2A> 方法中指定的阈值适用于前两种情况。  但在第一种情况中，由于以下两个原因，在与指定的阈值成比例的时间点您不总是能够收到通知。  
  
-   运行时不检查每个小型对象分配（出于性能原因）。  
  
-   只有第 1 级回收将内存提升至第 2 级。  
  
 第三种情况也增加了您在何时收到通知的不确定性。  可以在这段时间内对请求进行重定向，或者在系统可以更好地处理垃圾回收时由您自己引发垃圾回收，从而缓解在不恰当的时机发生完整垃圾回收所造成的不良影响。虽然这种做法不能提供完全的保障，但已证明是一种行之有效的方式。  
  
## 通知阈值参数  
 <xref:System.GC.RegisterForFullGCNotification%2A> 方法有两个参数用于指定第 2 级对象和大对象堆的阈值。  在达到这些值时，应引发垃圾回收通知。  下表介绍了这些参数。  
  
|参数|说明|  
|--------|--------|  
|`maxGenerationThreshold`|一个介于 1 和 99 之间的数字，指定基于提升至第 2 级的对象引发通知的时间。|  
|`largeObjectHeapThreshold`|一个介于 1 和 99 之间的数字，指定基于在大对象堆中分配的对象引发通知的时间。|  
  
 如果指定的值过高，则很有可能发生这样的情况：您虽然收到通知，但要等待很长一段时间之后运行时才会引发回收。  如果您自己引发回收，则回收的对象可能比运行时引发回收时回收的对象要多。  
  
 如果指定的值过低，则运行时可能在您来不及收到通知时就已引发回收。  
  
## 示例  
  
### 说明  
 在下面的示例中，有一组服务器为传入的 Web 请求提供服务。  为了模拟处理请求的工作负荷，该示例将一些字节数组添加到 <xref:System.Collections.Generic.List%601> 集合中。  每个服务器都注册一个垃圾回收通知，然后在 `WaitForFullGCProc` 用户方法上启动一个线程，以持续监视由 <xref:System.GC.WaitForFullGCApproach%2A> 和 <xref:System.GC.WaitForFullGCComplete%2A> 方法返回的 <xref:System.GCNotificationStatus> 枚举。  
  
 当引发通知时，<xref:System.GC.WaitForFullGCApproach%2A> 和 <xref:System.GC.WaitForFullGCComplete%2A> 方法调用各自的事件处理用户方法：  
  
-   `OnFullGCApproachNotify`  
  
     此方法调用 `RedirectRequests` 用户方法，该用户方法指示请求队列服务器挂起向服务器发送请求的操作。  该示例通过将类级变量 `bAllocate` 设置为 `false` 以便不再分配对象，对此操作进行模拟。  
  
     接下来，调用 `FinishExistingRequests` 用户方法完成对挂起的服务器请求的处理。  该示例通过清除 <xref:System.Collections.Generic.List%601> 集合来模拟此操作。  
  
     最后，会由于工作负荷变轻而引发垃圾回收。  
  
-   `OnFullGCCompleteNotify`  
  
     此方法调用用户方法 `AcceptRequests` 以继续接受请求，因为服务器不再容易遭遇完整垃圾回收。  该示例通过将 `bAllocate` 变量设置为 `true` 以便可以继续将对象添加到 <xref:System.Collections.Generic.List%601> 集合，对此操作进行模拟。  
  
 下面的代码包含示例的 `Main` 方法。  
  
 [!code-cpp[GCNotification#2](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#2)]
 [!code-csharp[GCNotification#2](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#2)]
 [!code-vb[GCNotification#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#2)]  
  
 下面的代码包含 `WaitForFullGCProc` 用户方法，该方法包含一个用于检查垃圾回收通知的连续 while 循环。  
  
 [!code-cpp[GCNotification#8](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#8)]
 [!code-csharp[GCNotification#8](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#8)]
 [!code-vb[GCNotification#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#8)]  
  
 下面的代码包含 `OnFullGCApproachNotify` 方法，该方法从  
  
 `WaitForFullGCProc` 方法。  
  
 [!code-cpp[GCNotification#5](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#5)]
 [!code-csharp[GCNotification#5](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#5)]
 [!code-vb[GCNotification#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#5)]  
  
 下面的代码包含 `OnFullGCApproachComplete` 方法，该方法从  
  
 `WaitForFullGCProc` 方法。  
  
 [!code-cpp[GCNotification#6](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#6)]
 [!code-csharp[GCNotification#6](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#6)]
 [!code-vb[GCNotification#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#6)]  
  
 下面的代码包含从 `OnFullGCApproachNotify` 和 `OnFullGCCompleteNotify` 方法调用的用户方法。  这些用户方法重定向请求，完成现有请求，在发生完整垃圾回收之后再继续请求。  
  
 [!code-cpp[GCNotification#9](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#9)]
 [!code-csharp[GCNotification#9](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#9)]
 [!code-vb[GCNotification#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#9)]  
  
 完整代码示例如下：  
  
 [!code-cpp[GCNotification#1](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#1)]
 [!code-csharp[GCNotification#1](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#1)]
 [!code-vb[GCNotification#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#1)]  
  
## 请参阅  
 [Garbage Collection](../../../docs/standard/garbage-collection/index.md)