---
title: "如何：打开并追加到日志文件 | Microsoft Docs"
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
  - "日志文件，打开"
  - "流，打开并追加到日志文件"
  - "日志文件，追加到"
  - "I/O [.NET Framework]，日志文件"
ms.assetid: 74423362-1721-49cb-aa0a-e04005f72a06
caps.latest.revision: 15
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：打开并追加到日志文件
<xref:System.IO.StreamWriter> 和 <xref:System.IO.StreamReader> 向流写入字符并从流读取字符。  下面的代码示例打开 `log.txt` 文件（如果文件不存在则创建文件）以进行输入，并将信息附加到文件尾。  然后将文件的内容写入标准输出以便显示。  除此示例演示的做法外，还可以将信息存储为单个字符串或字符串数组，<xref:System.IO.File.WriteAllText%2A> 或 <xref:System.IO.File.WriteAllLines%2A> 方法可以用于实现相同的功能。  
  
> [!NOTE]
>  Visual Basic 用户可以选择使用由 <xref:Microsoft.VisualBasic.Logging.Log> 类或 <xref:Microsoft.VisualBasic.FileIO.FileSystem> 类提供的方法和属性创建或写入日志文件。  
  
## 示例  
 [!code-csharp[Conceptual.BasicIO.TextFiles#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/source2.cs#2)]
 [!code-vb[Conceptual.BasicIO.TextFiles#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/source2.vb#2)]  
  
## 请参阅  
 <xref:System.IO.StreamWriter>   
 <xref:System.IO.StreamReader>   
 <xref:System.IO.File.AppendText%2A?displayProperty=fullName>   
 <xref:System.IO.File.OpenText%2A?displayProperty=fullName>   
 <xref:System.IO.StreamReader.ReadLine%2A?displayProperty=fullName>   
 [如何：枚举目录和文件](../../../docs/standard/io/how-to-enumerate-directories-and-files.md)   
 [如何：对新建的数据文件进行读取和写入](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)   
 [如何：从文件读取文本](../../../docs/standard/io/how-to-read-text-from-a-file.md)   
 [如何：向文件写入文本](../../../docs/standard/io/how-to-write-text-to-a-file.md)   
 [如何：从字符串中读取字符](../../../docs/standard/io/how-to-read-characters-from-a-string.md)   
 [如何：向字符串写入字符](../../../docs/standard/io/how-to-write-characters-to-a-string.md)   
 [文件和流 I\/O](../../../docs/standard/io/index.md)