---
title: "版本 3.5 中的套接字性能增强"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: 225aa5f9-c54b-4620-ab64-5cd100cfd54c
caps.latest.revision: 9
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 3e0e648fb14e07b62f70c614af84a98a256f6095
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="socket-performance-enhancements-in-version-35"></a>版本 3.5 中的套接字性能增强
版本 3.5 中增强了 <xref:System.Net.Sockets.Socket?displayProperty=fullName> 类，以供使用异步网络 I/O 实现最高性能的应用程序使用。 已添加了一系列新类，作为 <xref:System.Net.Sockets.Socket> 类的一组增强功能的一部分，这些增强功能提供了一种可供专用高性能套接字应用程序使用的替代异步模式。 这些增强功能专为需要高性能的网络服务器应用程序而设计。 应用程序可以独占方式使用增强型异步模式，或仅在其应用程序的目标热区域（例如，接收大量数据时）使用。  
  
## <a name="class-enhancements"></a>类增强功能  
 这些增强功能的主要功能是避免在大容量异步套接字 I/O 期间重复分配和同步对象。 当前由异步套接字 I/O 的 <xref:System.Net.Sockets.Socket> 类实现的 Begin/End 设计模式需要为每个异步套接字操作分配一个 <xref:System.IAsyncResult?displayProperty=fullName> 对象。  
  
 在新的 <xref:System.Net.Sockets.Socket> 类增强功能中，异步套接字操作由应用程序分配和维护的可重用 <xref:System.Net.Sockets.SocketAsyncEventArgs?displayProperty=fullName> 类对象描述。 高性能套接字应用程序非常清楚必须维持的重叠套接字操作的数量。 该应用程序可创建所需的 <xref:System.Net.Sockets.SocketAsyncEventArgs> 对象数量。 例如，如果服务器应用程序始终需要 15 个套接字接受操作，以支持传入的客户端连接速率，则可以预先为此分配 15 个可重用的 <xref:System.Net.Sockets.SocketAsyncEventArgs> 对象。  
  
 使用此类执行异步套接字操作的模式包括以下步骤：  
  
1.  分配一个新的 <xref:System.Net.Sockets.SocketAsyncEventArgs> 上下文对象，或从应用程序池中获取一个空闲对象。  
  
2.  将上下文对象的属性设置为要执行的操作（例如，回调代理方法和数据缓冲区）。  
  
3.  调用适当的套接字方法 (xxxAsync) 以启动异步操作。  
  
4.  如果异步套接字方法 (xxxAsync) 在回调中返回 true，请查询完成状态的上下文属性。  
  
5.  如果异步套接字方法 (xxxAsync) 在回调中返回 false，则已同步完成该操作。 可查询上下文属性获取操作结果。  
  
6.  重新使用上下文进行另一项操作，将其放回池中，或放弃它。  
  
 新的异步套接字操作上下文对象的生存期由应用程序代码中的引用和异步 I/O 引用确定。 作为参数提交给异步套接字操作方法之一后，应用程序不必保留对异步套接字操作上下文对象的引用。 完成回调返回之前，应用程序会继续引用它。 然而，应用程序保留对上下文对象的引用是有利的，这样可将其重新用于将来的异步套接字操作。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Net.Sockets.Socket?displayProperty=fullName>   
 <xref:System.Net.Sockets.SendPacketsElement?displayProperty=fullName>   
 <xref:System.Net.Sockets.SocketAsyncEventArgs?displayProperty=fullName>   
 <xref:System.Net.Sockets.SocketAsyncOperation?displayProperty=fullName>   
 [网络编程示例](../../../docs/framework/network-programming/network-programming-samples.md)   
 [套接字性能技术示例](http://go.microsoft.com/fwlink/?LinkID=179570)

