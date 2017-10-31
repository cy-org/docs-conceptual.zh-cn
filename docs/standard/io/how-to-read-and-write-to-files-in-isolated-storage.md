---
title: "如何：在独立存储中读取和写入文件 | Microsoft Docs"
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
  - "使用独立存储的数据存储, 读取和写至文件"
  - "数据存储区, 读取和写至文件"
  - "文件, 独立存储"
  - "独立存储, 读取和写至文件"
  - "读取数据"
  - "在存储区中读取文件"
  - "存储, 读取和写至文件"
  - "使用独立存储来存储数据, 读取和写至文件"
  - "写到存储区中的文件"
ms.assetid: f977ebdc-1b55-475a-bc3d-3376470b08ae
caps.latest.revision: 15
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：在独立存储中读取和写入文件
读取或写入文件，一个在独立存储区的文件，有流读取器 \(<xref:System.IO.StreamReader> 对象\) 的 <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> 对象或流编写器 \(<xref:System.IO.StreamWriter> 对象\)。  
  
## 示例  
 下面的代码示例获取独立存储而检查名为 TestStore.txt 的文件是否存在。  如果不存在，则创建该文件并将“Hello Isolated Storage”写入文件。  如果 TestStore.txt 已存在，则代码示例读取文件。  
  
 [!code-csharp[Conceptual.IsolatedStorage#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source5.cs#5)]
 [!code-vb[Conceptual.IsolatedStorage#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source5.vb#5)]  
  
## 请参阅  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile>   
 <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream>   
 <xref:System.IO.FileMode?displayProperty=fullName>   
 <xref:System.IO.FileAccess?displayProperty=fullName>   
 <xref:System.IO.StreamReader?displayProperty=fullName>   
 <xref:System.IO.StreamWriter?displayProperty=fullName>   
 [文件和流 I\/O](../../../docs/standard/io/index.md)   
 [独立存储](../../../docs/standard/io/isolated-storage.md)