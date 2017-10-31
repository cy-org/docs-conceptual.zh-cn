---
title: "如何：使用匿名管道进行本地进程间通信 | Microsoft Docs"
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
  - "匿名管道 [.NET Framework]"
  - "本地计算机通信 [.NET Framework], 管道"
  - "单向通信 [.NET Framework]"
  - "父子通信 [.NET Framework]"
  - "管道 [.NET Framework]"
ms.assetid: e7773c77-c646-4a01-8a96-a003d59fc4c9
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：使用匿名管道进行本地进程间通信
匿名管道提供本地计算机上的进程间通信。  他们提供的功能比命名管道少，它需要的系统开销也少。  您可以使用匿名管道更加轻松地在本地计算机上进行进程间通信。  不能使用匿名管道通过网络进行通信。  
  
 若要实现匿名管道，请使用 <xref:System.IO.Pipes.AnonymousPipeServerStream> 和 <xref:System.IO.Pipes.AnonymousPipeClientStream> 类。  
  
## 示例  
 下面的示例演示使用匿名管道将字符串从父进程发送到子进程的方式。  此示例使用 <xref:System.IO.Pipes.PipeDirection> 的 <xref:System.IO.Pipes.PipeDirection> 值在父进程中创建一个 <xref:System.IO.Pipes.AnonymousPipeServerStream> 对象。  然后，父进程通过使用客户端句柄创建一个 <xref:System.IO.Pipes.AnonymousPipeClientStream> 对象来创建一个子进程。  该子进程的 <xref:System.IO.Pipes.PipeDirection> 值为 <xref:System.IO.Pipes.PipeDirection>。  
  
 然后，父进程将用户提供的字符串发送给子进程。  该字符串将显示在子进程中的控制台上。  
  
 下面的示例演示服务器进程。  
  
 [!code-cpp[System.IO.Pipes.AnonymousPipeServerStream_Sample#01](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeServerStream_Sample/cpp/program.cpp#01)]
 [!code-csharp[System.IO.Pipes.AnonymousPipeServerStream_Sample#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeServerStream_Sample/cs/Program.cs#01)]
 [!code-vb[System.IO.Pipes.AnonymousPipeServerStream_Sample#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeServerStream_Sample/vb/program.vb#01)]  
  
## 示例  
 下面的示例演示客户端进程。  服务器进程启动客户端进程，并为该进程提供一个客户端句柄。  应该将从客户端代码得到的可执行文件命名为 `pipeClient.exe` 并在运行该服务器进程之前将其复制到服务器可执行文件所在的目录中。  
  
 [!code-cpp[System.IO.Pipes.AnonymousPipeClientStream_Sample#01](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeClientStream_Sample/cpp/program.cpp#01)]
 [!code-csharp[System.IO.Pipes.AnonymousPipeClientStream_Sample#01](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeClientStream_Sample/cs/Program.cs#01)]
 [!code-vb[System.IO.Pipes.AnonymousPipeClientStream_Sample#01](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.Pipes.AnonymousPipeClientStream_Sample/vb/program.vb#01)]  
  
## 请参阅  
 [管道](../../../docs/standard/io/pipe-operations.md)   
 [如何：使用命名管道进行网络进程间通信](../../../docs/standard/io/how-to-use-named-pipes-for-network-interprocess-communication.md)