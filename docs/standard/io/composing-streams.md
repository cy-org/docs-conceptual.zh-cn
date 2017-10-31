---
title: "编写流 | Microsoft Docs"
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
  - "流，基流"
  - "I/O [.NET Framework]，编写流"
  - "流类，编写流"
  - "基流"
  - "流，备用存储区"
ms.assetid: da761658-a535-4f26-a452-b30df47f73d5
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 10
---
# 编写流
备份存储区是一个存储媒介，例如磁盘或内存。  每个不同的备份存储区都实现其自己的流作为 <xref:System.IO.Stream> 类的实现。  每个流类型也都从其给定的备份存储区读取字节并向其给定的备份存储区写入字节。  连接到备份存储区的流叫做基流。  基流具有的构造函数具有将流连接到备份存储区所需的参数。  例如，<xref:System.IO.FileStream> 具有指定路径参数（指定进程将如何共享文件的参数）等的构造函数。  
  
 <xref:System.IO> 类的设计提供简化的流构成。  可以将基流附加到一个或多个提供所需功能的传递流。  读取器或编写器可以附加到链的末端，这样便可以方便地读取或写入所需的类型。  
  
 下面的代码示例围绕现有 `MyFile.txt` 创建 **FileStream**，为 `MyFile.txt` 提供缓冲。（请注意，默认情况下缓冲 **FileStreams**。）然后，创建 <xref:System.IO.StreamReader> 以读取 **FileStream** 中的字符，FileStream 将作为 **StreamReader** 的构造函数参数传递给它。  <xref:System.IO.StreamReader.ReadLine%2A> 将进行读取，直到 <xref:System.IO.StreamReader.Peek%2A> 再也找不到任何字符为止。  
  
 [!code-cpp[System.IO.StreamReader#20](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.StreamReader/CPP/source2.cpp#20)]
 [!code-csharp[System.IO.StreamReader#20](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.StreamReader/CS/source2.cs#20)]
 [!code-vb[System.IO.StreamReader#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.StreamReader/VB/source2.vb#20)]  
  
 下面的代码示例围绕现有 `MyFile.txt` 创建 **FileStream**，为 `MyFile.txt` 提供缓冲。（请注意，默认情况下缓冲 **FileStreams**。）然后，创建 **BinaryReader** 以读取 **FileStream** 中的字节，FileStream 将作为 **BinaryReader** 的构造函数参数传递给它。  <xref:System.IO.BinaryReader.ReadByte%2A> 将进行读取，直到 <xref:System.IO.BinaryReader.PeekChar%2A> 再也找不到任何字节为止。  
  
 [!code-cpp[System.IO.StreamReader#21](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.StreamReader/CPP/source3.cpp#21)]
 [!code-csharp[System.IO.StreamReader#21](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.StreamReader/CS/source3.cs#21)]
 [!code-vb[System.IO.StreamReader#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.StreamReader/VB/source3.vb#21)]  
  
## 请参阅  
 <xref:System.IO.StreamReader>   
 <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=fullName>   
 <xref:System.IO.StreamReader.Peek%2A?displayProperty=fullName>   
 <xref:System.IO.FileStream>   
 <xref:System.IO.BinaryReader>   
 <xref:System.IO.BinaryReader.ReadByte%2A?displayProperty=fullName>   
 <xref:System.IO.BinaryReader.PeekChar%2A?displayProperty=fullName>