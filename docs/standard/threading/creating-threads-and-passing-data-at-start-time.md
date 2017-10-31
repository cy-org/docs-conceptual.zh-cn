---
title: "Creating Threads and Passing Data at Start Time | Microsoft Docs"
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
  - "threading [.NET Framework], creating"
  - "threading [.NET Framework], passing data to threads"
  - "threading [.NET Framework], retrieving data from threads"
ms.assetid: 52b32222-e185-4f42-91a7-eaca65c0ab6d
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# Creating Threads and Passing Data at Start Time
在创建操作系统进程时，操作系统将插入一个线程以执行该进程（包括任何原始应用程序域）中的代码。  从此刻起，就可以创建和销毁应用程序域，而不必创建或销毁任何操作系统线程。  如果正在执行的代码是托管代码，则可以通过检索类型为 <xref:System.Threading.Thread> 的静态 <xref:System.Threading.Thread.CurrentThread%2A> 属性来获取正在当前应用程序域中执行的线程的 <xref:System.Threading.Thread> 对象。  本主题描述线程创建，并讨论用于向线程过程传递数据的替代方法。  
  
## 创建线程  
 创建新的 <xref:System.Threading.Thread> 对象时，将创建新的托管线程。  <xref:System.Threading.Thread> 类具有接受一个 <xref:System.Threading.ThreadStart> 委托或 <xref:System.Threading.ParameterizedThreadStart> 委托的构造函数：该委托包装调用 <xref:System.Threading.Thread.Start%2A> 方法时由新线程调用的方法。  多次调用 <xref:System.Threading.Thread.Start%2A> 将引发 <xref:System.Threading.ThreadStateException>。  
  
 <xref:System.Threading.Thread.Start%2A> 方法立即返回，经常是在实际启动新线程之前。  可以使用 <xref:System.Threading.Thread.ThreadState%2A> 和 <xref:System.Threading.Thread.IsAlive%2A> 属性确定任何时刻的线程状态，但是绝不应该将这些属性用于同步线程活动。  
  
> [!NOTE]
>  线程一旦启动，就不必保留对 <xref:System.Threading.Thread> 对象的引用。  该线程会继续执行，直到线程过程结束为止。  
  
 下面的代码示例创建两个新线程以调用另一个对象上的实例和静态方法。  
  
 [!code-cpp[System.Threading.ThreadStart2#2](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CPP/source2.cpp#2)]
 [!code-csharp[System.Threading.ThreadStart2#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CS/source2.cs#2)]
 [!code-vb[System.Threading.ThreadStart2#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Threading.ThreadStart2/VB/source2.vb#2)]  
  
## 将数据传递给线程和从线程检索数据  
 在 .NET Framework 2.0 版中，<xref:System.Threading.ParameterizedThreadStart> 委托提供了一种简便方法，可以在调用 <xref:System.Threading.Thread.Start%2A?displayProperty=fullName> 方法重载时将包含数据的对象传递给线程。  有关代码示例，请参见 <xref:System.Threading.ParameterizedThreadStart>。  
  
 使用 <xref:System.Threading.ParameterizedThreadStart> 委托不是传递数据的类型安全的方法，因为 <xref:System.Threading.Thread.Start%2A?displayProperty=fullName> 方法重载接受任何对象。  一种替代方法是将线程过程和数据封装在帮助器类中，并使用 <xref:System.Threading.ThreadStart> 委托执行线程过程。  该技术在下面的两个代码示例中演示。  
  
 这两个委托都没有返回值，因为没有地方用于从异步调用中返回数据。  为检索线程方法的结果，您可以使用回调方法，如第二个代码示例中所示。  
  
 [!code-cpp[System.Threading.ThreadStart2#3](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CPP/source3.cpp#3)]
 [!code-csharp[System.Threading.ThreadStart2#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CS/source3.cs#3)]
 [!code-vb[System.Threading.ThreadStart2#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Threading.ThreadStart2/VB/source3.vb#3)]  
  
### 使用回调方法检索数据  
 下面的示例演示了一个从线程中检索数据的回调方法。  包含数据和线程方法的类的构造函数也接受代表回调方法的委托；在线程方法结束前，它调用该回调委托。  
  
 [!code-cpp[System.Threading.ThreadStart2#4](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CPP/source4.cpp#4)]
 [!code-csharp[System.Threading.ThreadStart2#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Threading.ThreadStart2/CS/source4.cs#4)]
 [!code-vb[System.Threading.ThreadStart2#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Threading.ThreadStart2/VB/source4.vb#4)]  
  
## 请参阅  
 <xref:System.Threading.Thread>   
 <xref:System.Threading.ThreadStart>   
 <xref:System.Threading.ParameterizedThreadStart>   
 <xref:System.Threading.Thread.Start%2A?displayProperty=fullName>   
 [Threading](../../../docs/standard/threading/index.md)   
 [Using Threads and Threading](../../../docs/standard/threading/using-threads-and-threading.md)