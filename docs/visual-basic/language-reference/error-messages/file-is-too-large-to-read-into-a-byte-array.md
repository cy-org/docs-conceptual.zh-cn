---
title: "文件太大，无法读取到字节数组中 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
ms.assetid: 686630a6-a439-46c7-8d7b-34613ae4c5d8
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 文件太大，无法读取到字节数组中
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

尝试读取到字节数组中的文件的大小超过了 4 GB。  `My.Computer.FileSystem.ReadAllBytes` 方法无法读取超过此大小的文件。  
  
### 更正此错误  
  
-   请使用 <xref:System.IO.StreamReader> 来读取该文件。  有关更多信息，请参见 [.NET Framework 文件 I\/O 和文件系统基础知识 \(Visual Basic\)](../../../visual-basic/developing-apps/programming/drives-directories-files/basics-of-net-framework-file-io-and-the-file-system.md)。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllBytes%2A>   
 <xref:System.IO.StreamReader>   
 [使用 Visual Basic 访问文件](../../../visual-basic/developing-apps/programming/drives-directories-files/file-access.md)   
 [如何：使用 StreamReader 读取文件中的文本](../../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-text-from-files-with-a-streamreader.md)