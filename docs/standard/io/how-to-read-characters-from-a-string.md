---
title: "如何：从字符串中读取字符 | Microsoft Docs"
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
  - "从字符串中读取字符"
  - "数据流，从字符串中读取字符"
  - "I/O [.NET Framework]，从字符串中读取字符"
  - "读取数据，字符串"
  - "流，从字符串中读取字符"
ms.assetid: 27ea5e52-6db8-42d8-980a-50bcfc7fd270
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：从字符串中读取字符
下面的代码示例演示如何从命字符串同步和异步读取字符。  
  
## 示例  
 此示例从字符串同步读取 13 个字符，将它们存储在数组，并显示这些字符。  在数组中读取字符串的其余字符，然后将其存储开始第六元素中，并且显示数组的内容。  
  
 [!code-cpp[Conceptual.StringReader#1](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.stringreader/cpp/source.cpp#1)]
 [!code-csharp[Conceptual.StringReader#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.stringreader/cs/source.cs#1)]
 [!code-vb[Conceptual.StringReader#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.stringreader/vb/source.vb#1)]  
  
## 示例  
 下面的示例从字符数组中读取所有异步 <xref:System.Windows.Controls.TextBox> 控件，并将其存储。  该异步然后编写适用于换行符后面的一行。每个字母或空白字符到 <xref:System.Windows.Controls.TextBlock> 控件。  
  
 [!code-csharp[Conceptual.StringReader#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.stringreader/cs/source2.cs#2)]
 [!code-vb[Conceptual.StringReader#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.stringreader/vb/source2.vb#2)]  
  
## 请参阅  
 <xref:System.IO.StringReader>   
 <xref:System.IO.StringReader.Read%2A?displayProperty=fullName>   
 [异步文件 I\/O](../../../docs/standard/io/异步文件-i-o.md)   
 [NIB: How to: Create a Directory Listing](http://msdn.microsoft.com/zh-cn/4d2772b1-b991-4532-a8a6-6ef733277e69)   
 [如何：对新建的数据文件进行读取和写入](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)   
 [如何：打开并追加到日志文件](../../../docs/standard/io/how-to-open-and-append-to-a-log-file.md)   
 [如何：从文件读取文本](../../../docs/standard/io/how-to-read-text-from-a-file.md)   
 [如何：向文件写入文本](../../../docs/standard/io/how-to-write-text-to-a-file.md)   
 [如何：向字符串写入字符](../../../docs/standard/io/how-to-write-characters-to-a-string.md)   
 [文件和流 I\/O](../../../docs/standard/io/index.md)