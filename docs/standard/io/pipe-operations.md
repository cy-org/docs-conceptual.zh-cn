---
title: ".NET Framework 中的管道操作 | Microsoft Docs"
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
  - "管道 [.NET Framework]"
  - "管道操作 [.NET Framework]"
  - "进程间通信 [.NET Framework]，管道"
  - "I/O [.NET Framework]，管道"
ms.assetid: 7b964ebd-7a4f-4d28-8194-7841f9e4c702
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# .NET Framework 中的管道操作
管道提供了一种进程间通信的方法。  有两种类型的管道：  
  
-   匿名管道。  
  
     匿名管道提供本地计算机上的进程间通信。  匿名管道需要的系统开销比命名管道少，但它提供的服务也很有限。  匿名管道为单向的，不能在网络上使用。  它们只支持单一服务器实例。  匿名管道对线程间通信或是父子进程之间的通信非常有用，对于后者，管道句柄可以轻松地传递给子进程（在子进程创建之时）。  
  
     在NET Framework，可通过使用 <xref:System.IO.Pipes.AnonymousPipeServerStream> and <xref:System.IO.Pipes.AnonymousPipeClientStream> 类来实现匿名管道。  
  
     请参见[如何：使用匿名管道进行本地进程间通信](../../../docs/standard/io/how-to-use-anonymous-pipes-for-local-interprocess-communication.md)。  
  
-   命名管道。  
  
     命名管道提供一个管道服务器与一个或多个管道客户端之间的进程间通信。  命名管道可以是单向的，也可以是双向的。  它们支持基于消息的通信，允许多个客户端使用相同的管道名称同时连接服务器进程。  命名管道还支持模拟，这使得连接进程可以在远程服务器上使用它们自己的权限。  
  
     在.NET Framework, 可通过使用 <xref:System.IO.Pipes.NamedPipeServerStream> and <xref:System.IO.Pipes.NamedPipeClientStream> 类来实现命名管道。  
  
     请参见[如何：使用命名管道进行网络进程间通信](../../../docs/standard/io/how-to-use-named-pipes-for-network-interprocess-communication.md)。  
  
## 请参阅  
 [文件和流 I\/O](../../../docs/standard/io/index.md)   
 [如何：使用匿名管道进行本地进程间通信](../../../docs/standard/io/how-to-use-anonymous-pipes-for-local-interprocess-communication.md)   
 [如何：使用命名管道进行网络进程间通信](../../../docs/standard/io/how-to-use-named-pipes-for-network-interprocess-communication.md)