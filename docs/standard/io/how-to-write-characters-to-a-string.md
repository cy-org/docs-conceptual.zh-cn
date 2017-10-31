---
title: "如何：向字符串写入字符 | Microsoft Docs"
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
  - "数据流，将字符写入字符串"
  - "将字符写入字符串"
  - "流，将字符写入字符串"
  - "I/O [.NET Framework]，将字符写入字符串"
ms.assetid: 1222cbeb-0760-44bf-9888-914a2a37174b
caps.latest.revision: 17
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：向字符串写入字符
下面的代码示例从字符数组以同步和异步的方式写入字符到字符串。  
  
## 示例  
 下面的示例从数组同步写入5个字符到字符串。  
  
 [!code-csharp[Conceptual.StringBuilder#9](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/example2.cs#9)]
 [!code-vb[Conceptual.StringBuilder#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/example2.vb#9)]  
  
## 示例  
 下面的示例从字符数组中读取所有异步 <xref:System.Windows.Controls.TextBox> 控件，并将其存储。  该异步然后编写适用于换行符后面的一行。每个字母或空白字符到 <xref:System.Windows.Controls.TextBlock> 控件。  
  
 [!code-csharp[Conceptual.StringReader#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.stringreader/cs/source2.cs#2)]
 [!code-vb[Conceptual.StringReader#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.stringreader/vb/source2.vb#2)]  
  
## 请参阅  
 <xref:System.IO.StringWriter>   
 <xref:System.IO.StringWriter.Write%2A?displayProperty=fullName>   
 <xref:System.Text.StringBuilder>   
 [文件和流 I\/O](../../../docs/standard/io/index.md)   
 [异步文件 I\/O](../../../docs/standard/io/异步文件-i-o.md)   
 [如何：枚举目录和文件](../../../docs/standard/io/how-to-enumerate-directories-and-files.md)   
 [如何：对新建的数据文件进行读取和写入](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)   
 [如何：打开并追加到日志文件](../../../docs/standard/io/how-to-open-and-append-to-a-log-file.md)   
 [如何：从文件读取文本](../../../docs/standard/io/how-to-read-text-from-a-file.md)   
 [如何：向文件写入文本](../../../docs/standard/io/how-to-write-text-to-a-file.md)   
 [如何：从字符串中读取字符](../../../docs/standard/io/how-to-read-characters-from-a-string.md)