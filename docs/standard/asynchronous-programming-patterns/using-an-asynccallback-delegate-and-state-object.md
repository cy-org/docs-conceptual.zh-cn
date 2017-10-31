---
title: "Using an AsyncCallback Delegate and State Object | Microsoft Docs"
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
  - "asynchronous programming, delegates"
  - "AsyncCallback delegate, samples"
  - "asynchronous programming, state objects"
  - "IAsyncResult interface, samples"
ms.assetid: e3e5475d-c5e9-43f0-928e-d18df8ca1f1d
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# Using an AsyncCallback Delegate and State Object
当您使用 <xref:System.AsyncCallback> 委托处理单独线程中的异步操作的结果时，可以将状态对象用于传递回调之间的信息以及用于检索最终结果。  本主题由正在展开示例的做法在 [Using an AsyncCallback Delegate to End an Asynchronous Operation](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md) 中演示。  
  
## 示例  
 下面的代码示例演示如何使用 <xref:System.Net.Dns> 类中的异步方法来检索用户指定的计算机的域名系统 \(DNS\) 信息。  此示例定义了 `HostRequest` 类并使用该类来存储状态信息。  此示例中为用户输入的每个计算机名都创建了一个 `HostRequest` 对象。  此对象被传递给了 <xref:System.Net.Dns.BeginGetHostByName%2A> 方法。  每当请求完成时，都会调用 `ProcessDnsInformation` 方法。  可使用 <xref:System.IAsyncResult.AsyncState%2A> 属性来检索 `HostRequest` 对象。  `ProcessDnsInformation` 方法使用 `HostRequest` 对象来存储请求返回的 <xref:System.Net.IPHostEntry> 或请求引发的 <xref:System.Net.Sockets.SocketException>。  当所有的请求都完成后，应用程序会循环访问 `HostRequest` 对象，显示 DNS 信息或 <xref:System.Net.Sockets.SocketException> 错误信息。  
  
 [!code-csharp[AsyncDesignPattern#5](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/AsyncDelegateWithStateObject.cs#5)]
 [!code-vb[AsyncDesignPattern#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/AsyncDelegateWithStateObject.vb#5)]  
  
## 请参阅  
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)   
 [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)   
 [Using an AsyncCallback Delegate to End an Asynchronous Operation](../../../docs/standard/asynchronous-programming-patterns/using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md)