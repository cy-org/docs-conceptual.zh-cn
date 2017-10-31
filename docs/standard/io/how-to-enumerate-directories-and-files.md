---
title: "如何：枚举目录和文件 | Microsoft Docs"
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
  - "I/O [.NET Framework]，枚举目录和文件"
ms.assetid: 86b69a08-3bfa-4e5f-b4e1-3b7cb8478215
caps.latest.revision: 18
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 18
---
# 如何：枚举目录和文件
可以通过使用一些方法来枚举目录和文件，这些方法返回一个目录和文件的名称字符串的可枚举集合。  也可以使用将返回 <xref:System.IO.DirectoryInfo>、<xref:System.IO.FileInfo> 或 <xref:System.IO.FileSystemInfo> 对象的可枚举集合的方法。  当您与目录和文件的大型集合时，可枚举的集合比数组提供更好的性能。  
  
 此外，还可以使用通过上述方法获得的可枚举集合为集合类（如 <xref:System.Collections.Generic.List%601> 类）的构造函数提供 <xref:System.Collections.Generic.IEnumerable%601> 参数。  
  
 如果只需要获取目录或文件的名称，请使用 <xref:System.IO.Directory> 类的枚举方法。  如果需要获取目录或文件的其他属性，请使用 <xref:System.IO.DirectoryInfo> 和 <xref:System.IO.FileSystemInfo> 类。  
  
 下表提供了返回可枚举集合的方法的指南。  
  
|要枚举的项|要返回的可枚举集合|要使用的方法|  
|-----------|---------------|------------|  
|目录|目录名称。|<xref:System.IO.Directory.EnumerateDirectories%2A?displayProperty=fullName>|  
||目录信息\(<xref:System.IO.DirectoryInfo>\)。|<xref:System.IO.DirectoryInfo.EnumerateDirectories%2A?displayProperty=fullName>|  
|文件|文件名|<xref:System.IO.Directory.EnumerateFiles%2A?displayProperty=fullName>|  
||文件信息\(<xref:System.IO.FileInfo>\)。|<xref:System.IO.DirectoryInfo.EnumerateFiles%2A?displayProperty=fullName>|  
|文件系统信息|文件系统项。|<xref:System.IO.Directory.EnumerateFileSystemEntries%2A?displayProperty=fullName>|  
||文件系统信息\(<xref:System.IO.FileSystemInfo>\)。|<xref:System.IO.DirectoryInfo.EnumerateFileSystemInfos%2A?displayProperty=fullName>|  
  
 虽然可以使用 <xref:System.IO.SearchOption>枚举提供的<xref:System.IO.SearchOption>搜索选项立即枚举父目录的子目录中的所有文件，但未经授权的访问异常 \(<xref:System.UnauthorizedAccessException>\)可能会导致枚举无法完成。  如果可能出现这些异常，则可以捕获它们并继续操作，采用的方式是先枚举目录，然后再枚举文件。  
  
### 枚举目录名称  
  
-   使用 <xref:System.IO.Directory.EnumerateDirectories%28System.String%29?displayProperty=fullName> 方法可按指定路径获取顶级目录名称的列表。  
  
     [!code-csharp[System.IO.EnumDirs1#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.enumdirs1/cs/program.cs#1)]
     [!code-vb[System.IO.EnumDirs1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.enumdirs1/vb/program.vb#1)]  
  
### 枚举目录中子目录中文件名  
  
-   使用<xref:System.IO.Directory.EnumerateFiles%28System.String%2CSystem.String%2CSystem.IO.SearchOption%29?displayProperty=fullName>方法可搜索所有目录以按指定路径获取与指定搜索模式匹配的文件名称的列表。  
  
     [!code-csharp[System.IO.Directory.EnumerateFiles#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.directory.enumeratefiles/cs/program.cs#1)]
     [!code-vb[System.IO.Directory.EnumerateFiles#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.directory.enumeratefiles/vb/program.vb#1)]  
  
### 枚举 DirectoryInfo 对象的集合  
  
-   使用 <xref:System.IO.DirectoryInfo.EnumerateDirectories%2A?displayProperty=fullName> 方法可获取顶级目录的集合。  
  
     [!code-csharp[System.IO.DirectoryInfo.EnumDirs#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.directoryinfo.enumdirs/cs/program.cs#1)]
     [!code-vb[System.IO.DirectoryInfo.EnumDirs#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.directoryinfo.enumdirs/vb/module1.vb#1)]  
  
### 枚举所有目录中的 FileInfo 对象的集合  
  
-   使用 <xref:System.IO.DirectoryInfo.EnumerateFiles%2A?displayProperty=fullName> 方法可获取所有目录中与指定搜索模式匹配的文件的集合。  本示例先枚举顶级目录以捕获可能出现的未经授权的访问异常，然后再枚举文件。  
  
     [!code-csharp[System.IO.DirectoryInfo.EnumerateDirectories#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.directoryinfo.enumeratedirectories/cs/program.cs#1)]
     [!code-vb[System.IO.DirectoryInfo.EnumerateDirectories#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.directoryinfo.enumeratedirectories/vb/program.vb#1)]  
  
## 请参阅  
 [文件和流 I\/O](../../../docs/standard/io/index.md)