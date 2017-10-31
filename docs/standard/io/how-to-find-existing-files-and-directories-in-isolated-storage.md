---
title: "如何：在独立存储中查找现有文件和目录 | Microsoft Docs"
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
  - "存储，查找文件和目录"
  - "在独立存储文件中查找文件"
  - "目录 [.NET Framework]，独立存储"
  - "独立存储，查找文件和目录"
  - "使用独立存储的数据存储，查找文件和目录"
  - "文件 [.NET Framework]，独立存储"
  - "数据存储，查找文件和目录"
  - "在独立存储文件中查找目录"
  - "使用独立存储来存储数据，查找文件和目录"
ms.assetid: eb28458a-6161-4e7a-9ada-30ef93761b5c
caps.latest.revision: 12
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：在独立存储中查找现有文件和目录
为了搜索独立存储的目录，请使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A?displayProperty=fullName> 方法。  此方法采用表示搜索模式的字符串。  在搜索模式可以使用单字符 \(?\) 和多字符 \(\*\) 通配符，但是通配符必须出现在名称的最后一部分。  例如，`directory1/*ect*` 是有效的搜索字符串，但是`*ect*/directory2` 不是。  
  
 若要搜索文件，请使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A?displayProperty=fullName> 方法。  对应用于<xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A> 的搜索字符串中通配符的相同限制也适用于 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A>。  
  
 方法都不是递归的；<xref:System.IO.IsolatedStorage.IsolatedStorageFile> 类在你的存储中，不提供用于列出所有目录或文件的任何方法。  但是，为递归方法在下面的代码示例中显示。  
  
## 示例  
 下面的代码示例阐释如何在独立存储区创建文件和目录。  首先，检索一个为用户、域和程序集隔离的存储区并放入 `isoStore` 变量。  <xref:System.IO.IsolatedStorage.IsolatedStorageFile.CreateDirectory%2A> 方法用于设置几个不同的目录，<xref:System.IO.IsolatedStorage.IsolatedStorageFileStream.%23ctor%28System.String%2CSystem.IO.FileMode%2CSystem.IO.IsolatedStorage.IsolatedStorageFile%29> constructor 。  然后，代码依次通过 `GetAllDirectories` 方法的结果。  该方法使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetDirectoryNames%2A> 来查找当前目录中的所有目录名。  这些名称存储在数组中，然后 `GetAllDirectories` 调用其本身，传入它所找到的每个目录。  结果是返回的所有目录名在数组中。  然后，代码调用 `GetAllFiles` 方法。  该方法调用 `GetAllDirectories`以查找所有目录的名称，然后它检查每个目录以查找使用<xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetFileNames%2A>方法的文件。  结果返回到数组中用于显示。  
  
 [!code-cpp[Conceptual.IsolatedStorage#9](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source8.cpp#9)]
 [!code-csharp[Conceptual.IsolatedStorage#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source8.cs#9)]
 [!code-vb[Conceptual.IsolatedStorage#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source8.vb#9)]  
  
## 请参阅  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile>   
 [独立存储](../../../docs/standard/io/isolated-storage.md)