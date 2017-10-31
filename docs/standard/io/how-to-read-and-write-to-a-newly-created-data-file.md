---
title: "如何：对新建的数据文件进行读取和写入 | Microsoft Docs"
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
  - "BinaryReader 类, 示例"
  - "BinaryWriter 类, 示例"
  - "I/O [.NET Framework], 读取数据"
  - "I/O [.NET Framework], 写入数据"
  - "流, 读写数据"
ms.assetid: e209d949-31e8-44ea-8e38-87f9093f3093
caps.latest.revision: 16
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：对新建的数据文件进行读取和写入
<xref:System.IO.BinaryWriter> 和 <xref:System.IO.BinaryReader?displayProperty=fullName>类用于读取和写入数据，而不是用于读取和写入字符串。  下面的代码示例演示如何向新的空文件流 `Test.data`写入数据及从中读取数据。  在当前目录中创建了数据文件之后，也就同时创建了相关的 <xref:System.IO.BinaryWriter> 和 <xref:System.IO.BinaryReader> objects are created, and the <xref:System.IO.BinaryWriter>用于向 `Test.data`写入整数 0 到 10，Test.data 将文件指针置于文件尾。  在将文件指针设置回初始位置后，<xref:System.IO.BinaryReader>对象读出指定的内容。  
  
## 示例  
 [!code-cpp[System.IO.BinaryReaderWriter#7](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.IO.BinaryReaderWriter/CPP/source6.cpp#7)]
 [!code-csharp[System.IO.BinaryReaderWriter#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.IO.BinaryReaderWriter/CS/source6.cs#7)]
 [!code-vb[System.IO.BinaryReaderWriter#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.IO.BinaryReaderWriter/VB/source6.vb#7)]  
  
## 可靠编程  
 如果当前目录中已存在 `Test.data`，则会引发 <xref:System.IO.IOException>异常。  始终使用 <xref:System.IO.FileMode?displayProperty=fullName>创建新文件初始化文件流，而不引发异常  
  
## 请参阅  
 <xref:System.IO.BinaryReader>   
 <xref:System.IO.BinaryWriter>   
 <xref:System.IO.FileStream>   
 <xref:System.IO.FileStream.Seek%2A?displayProperty=fullName>   
 <xref:System.IO.SeekOrigin>   
 [如何：枚举目录和文件](../../../docs/standard/io/how-to-enumerate-directories-and-files.md)   
 [如何：打开并追加到日志文件](../../../docs/standard/io/how-to-open-and-append-to-a-log-file.md)   
 [如何：从文件读取文本](../../../docs/standard/io/how-to-read-text-from-a-file.md)   
 [如何：向文件写入文本](../../../docs/standard/io/how-to-write-text-to-a-file.md)   
 [如何：从字符串中读取字符](../../../docs/standard/io/how-to-read-characters-from-a-string.md)   
 [如何：向字符串写入字符](../../../docs/standard/io/how-to-write-characters-to-a-string.md)   
 [文件和流 I\/O](../../../docs/standard/io/index.md)