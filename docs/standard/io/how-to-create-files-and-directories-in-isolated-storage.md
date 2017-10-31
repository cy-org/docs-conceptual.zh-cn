---
title: "如何：在独立存储中创建文件和目录 | Microsoft Docs"
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
  - "目录 [.NET Framework]，独立存储"
  - "文件 [.NET Framework]，独立存储"
  - "独立存储，创建文件和目录"
  - "数据存储，创建文件和目录"
  - "使用独立存储的数据存储，创建文件和目录"
  - "存储，创建文件和目录"
  - "使用独立存储存储数据，创建文件和目录"
ms.assetid: 2ca4d2a4-809b-4f00-bc08-bf4a64d3a5c3
caps.latest.revision: 12
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：在独立存储中创建文件和目录
获得隔离存储区之后，您可以创建用于存储数据的目录和文件。  在存储区中，文件名和目录名是相对于虚文件系统的根目录指定的。  
  
 若要创建目录，请使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateDirectory%2A?displayProperty=fullName>实例方法。  如果您指定一个未创建目录的子目录，则会同时创建两个目录。  如果您指定一个已存在的目录，方法返回，而不创建目录，因此，不会引发异常。  但是，如果您指定了包含无效字符的目录名称，则 <xref:System.IO.IsolatedStorage.IsolatedStorageException>异常被抛出。  
  
 使用<xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateFile%2A?displayProperty=fullName>方法，创建文件。  
  
 在 Windows 操作系统，独立存储文件和目录名不区分大小写。  就是，如果您创建了一个名为 `ThisFile.txt` 的文件，然后又创建了名为 `THISFILE.TXT` 的另一个文件，实际上只创建了一个文件。  显示时，文件名保持其原有的大小写。  
  
## 示例  
 下面的代码示例阐释如何在独立存储区创建文件和目录。  
  
 [!code-csharp[Conceptual.IsolatedStorage#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source.cs#1)]
 [!code-vb[Conceptual.IsolatedStorage#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source.vb#1)]  
  
## 请参阅  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile>   
 <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream>   
 [独立存储](../../../docs/standard/io/isolated-storage.md)