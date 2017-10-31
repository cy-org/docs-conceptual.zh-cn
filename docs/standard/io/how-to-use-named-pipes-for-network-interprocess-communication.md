---
title: "如何：使用命名管道进行网络进程间通信 | Microsoft Docs"
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
  - "全双工通信 [.NET Framework], 命名管道"
  - "模拟 [.NET Framework], 命名管道"
  - "基于消息的通信 [.NET Framework], 命名管道"
  - "通过命名管道的多个连接"
  - "命名管道 [.NET Framework]"
  - "网络通信 [.NET Framework], 命名管道"
  - "管道 [.NET Framework]"
ms.assetid: 4e4d7e64-9f1b-4026-98f7-20488ac7b42b
caps.latest.revision: 16
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：使用命名管道进行网络进程间通信
命名管道提供一个管道服务器与一个或多个管道客户端之间的进程间通信。  它们提供比匿名管道更多的功能，在本地计算机上提供进程间的通信。  命名的管道支持网络和多个服务器实例的全双工通信；基于消息的通信；以及客户端模拟，这使得在远程服务器上可以使用他们自己的权限集来连接进程。  
  
 若要实现名称管道，请使用 <xref:System.IO.Pipes.NamedPipeServerStream> 和 <xref:System.IO.Pipes.NamedPipeClientStream> 类。  
  
## 示例  
 下面的示例演示如何使用 <xref:System.IO.Pipes.NamedPipeServerStream> 类创建命名管道。  在此示例中，服务器进程创建了四个线程。  每个线程可以接受一个客户端连接。  连接的客户端进程随后向服务器提供一个文件名。  如果客户端具有足够的权限，服务器进程就会打开文件并将其内容发送回客户端。  
  
 [!code-cpp[System.IO.Pipes.NamedPipeServerStream_ImpersonationSample1#01](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeServerStream_ImpersonationSample1/cpp/program.cpp#01)]
 [!code-csharp[System.IO.Pipes.NamedPipeServerStream_ImpersonationSample1#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeServerStream_ImpersonationSample1/cs/Program.cs#01)]
 [!code-vb[System.IO.Pipes.NamedPipeServerStream_ImpersonationSample1#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeServerStream_ImpersonationSample1/vb/program.vb#01)]  
  
## 示例  
 下面的示例演示使用 <xref:System.IO.Pipes.NamedPipeClientStream> 类的客户端进程。  客户端连接服务器进程并向服务器发送一个文件名。  该示例使用模拟，所以运行客户端应用程序的标识必须具有访问文件的权限。  服务器随后将文件内容发送回客户端。  文件内容随后显示在控制台上。  
  
 [!code-csharp[System.IO.Pipes.NamedPipeClientStream_ImpersonationSample1#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeClientStream_ImpersonationSample1/cs/Program.cs#01)]
 [!code-vb[System.IO.Pipes.NamedPipeClientStream_ImpersonationSample1#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Pipes.NamedPipeClientStream_ImpersonationSample1/vb/program.vb#01)]  
  
## 可靠编程  
 此示例中的客户端进程和服务器进程预期在同一台计算机上运行，因此提供给 <xref:System.IO.Pipes.NamedPipeClientStream> 对象的服务器名称是 `"."`。  如果客户端进程和服务器进程位于不同的计算机上，则应该用运行服务器进程的计算机的网络名称来替换 `"."`。  
  
## 请参阅  
 <xref:System.Security.Principal.TokenImpersonationLevel>   
 <xref:System.IO.Pipes.NamedPipeServerStream.GetImpersonationUserName%2A>   
 [管道](../../../docs/standard/io/pipe-operations.md)   
 [如何：使用匿名管道进行本地进程间通信](../../../docs/standard/io/how-to-use-anonymous-pipes-for-local-interprocess-communication.md)