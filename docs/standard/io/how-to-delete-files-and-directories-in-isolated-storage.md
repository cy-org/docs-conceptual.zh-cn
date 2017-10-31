---
title: "如何：在独立存储中删除文件和目录 | Microsoft Docs"
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
  - "使用独立存储的数据存储，删除文件和目录"
  - "目录 [.NET Framework]，独立存储"
  - "文件 [.NET Framework]，独立存储"
  - "独立存储，删除文件和目录"
  - "数据存储，删除文件和目录"
  - "存储，创建文件和目录"
  - "删除独立步骤文件中的文件"
  - "使用独立存储存储数据，删除文件和目录"
  - "删除独立步骤文件中的目录"
ms.assetid: 8fcc0dea-435b-4d40-ba4d-ba056265c202
caps.latest.revision: 12
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：在独立存储中删除文件和目录
您可以删除独立存储文件中的目录和文件。  在存储区中，文件名和目录名是操作系统的依赖项和指定相对于虚拟文件系统的根。  在Windows 操作系统它们不区分大小写。  
  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile?displayProperty=fullName>类提供了两种删除目录和文件的实例方法：<xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> 和<xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteFile%2A>。  如果尝试删除并不存在的文件和目录，则会引发<xref:System.IO.IsolatedStorage.IsolatedStorageException>。  如果在名称中包含，<xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A> 的通配符引发异常 <xref:System.IO.IsolatedStorage.IsolatedStorageException> 和 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteFile%2A> 会引发 <xref:System.ArgumentException> 异常。  
  
 如果目录中包含任何文件或子目录，<xref:System.IO.IsolatedStorage.IsolatedStorageFile.DeleteDirectory%2A>方法将会失败。  可以使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A> 和 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A> 方法检索现有文件和目录。  有关搜索存储的虚拟文件系统的更多信息，请参见 [如何：在独立存储中查找现有文件和目录](../../../docs/standard/io/how-to-find-existing-files-and-directories-in-isolated-storage.md)。  
  
## 示例  
 下面的代码示例先创建若干个目录和文件，然后将它们删除。  
  
 [!code-cpp[Conceptual.IsolatedStorage#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source4.cpp#4)]
 [!code-csharp[Conceptual.IsolatedStorage#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source4.cs#4)]
 [!code-vb[Conceptual.IsolatedStorage#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source4.vb#4)]  
  
## 请参阅  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile?displayProperty=fullName>   
 [独立存储](../../../docs/standard/io/isolated-storage.md)