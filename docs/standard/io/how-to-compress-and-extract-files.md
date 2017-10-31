---
title: "如何：压缩和解压缩文件 | Microsoft Docs"
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
  - "I/O [.NET Framework]，压缩"
  - "压缩"
  - "压缩文件"
ms.assetid: e9876165-3c60-4c84-a272-513e47acf579
caps.latest.revision: 19
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 19
---
# 如何：压缩和解压缩文件
<xref:System.IO.Compression>命名空间包含如下的基本的文件和流压缩和解压缩服务的类型。  还可以使用这些类型来读取和修改压缩文件的内容：  
  
-   <xref:System.IO.Compression.ZipFile>  
  
-   <xref:System.IO.Compression.ZipArchive>  
  
-   <xref:System.IO.Compression.ZipArchiveEntry>  
  
-   <xref:System.IO.Compression.DeflateStream>  
  
-   <xref:System.IO.Compression.GZipStream>  
  
 下面的示例演示当使用压缩文件时可以执行的某些功能。  
  
## 示例  
 此示例演示如何使用 <xref:System.IO.Compression.ZipFile> 类创建和提取有一个 .zip 文件扩展名的压缩文件。  它压缩文件夹的内容到新的.zip文件，然后提取一个新文件夹内容。  若要使用<xref:System.IO.Compression.ZipFile> 类，您必须引用项目的 `System.IO.Compression.FileSystem` 程序集。  
  
 [!code-csharp[System.IO.Compression.ZipFile#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.zipfile/cs/program1.cs#1)]
 [!code-vb[System.IO.Compression.ZipFile#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.zipfile/vb/program1.vb#1)]  
  
## 示例  
 下面的示例演示如何通过现存的.zip文件的内容重复存档并提取有一个 .txt 扩展名的文件。  它使用 <xref:System.IO.Compression.ZipArchive> 类访问现有的 .zip 文件与 <xref:System.IO.Compression.ZipArchiveEntry> 类来检查压缩文件的各个项。  它提供 <xref:System.IO.Compression.ZipArchiveEntry> 对象使用一个外接方法 \(<xref:System.IO.Compression.ZipFileExtensions.ExtractToFile%2A>\)。  扩展方法可以在 <xref:System.IO.Compression.ZipFileExtensions?displayProperty=fullName> 类使用。  若要使用<xref:System.IO.Compression.ZipFileExtensions> 类，您必须引用项目的 `System.IO.Compression.FileSystem` 程序集。  
  
 [!code-csharp[System.IO.Compression.ZipArchive#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchive/cs/program1.cs#1)]
 [!code-vb[System.IO.Compression.ZipArchive#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchive/vb/program1.vb#1)]  
  
## 示例  
 下一个示例使用 <xref:System.IO.Compression.ZipArchive> 类访问现有的 .zip 文件，然后添加新文件到压缩文件。  当添加到现有的 .zip 文件时，新文件获取压缩。  
  
 [!code-csharp[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/cs/program1.cs#1)]
 [!code-vb[System.IO.Compression.ZipArchiveMode#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.compression.ziparchivemode/vb/program1.vb#1)]  
  
## 示例  
 也可以使用 <xref:System.IO.Compression.GZipStream> 和 <xref:System.IO.Compression.DeflateStream> 类压缩和解压缩数据。  它们使用相同的压缩算法。  写入文件扩展名为 .gz 的压缩<xref:System.IO.Compression.GZipStream> 对象可以通过使用许多常用工具，除了 <xref:System.IO.Compression.GZipStream>提供的方法之外，被解压。  下面的示例演示如何使用 <xref:System.IO.Compression.GZipStream> 类压缩和解压缩文件目录。  
  
 [!code-csharp[IO.Compression.GZip1#1](../../../samples/snippets/csharp/VS_Snippets_CLR/IO.Compression.GZip1/CS/gziptest.cs#1)]
 [!code-vb[IO.Compression.GZip1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/IO.Compression.GZip1/VB/gziptest.vb#1)]  
  
## 请参阅  
 <xref:System.IO.Compression.ZipArchive>   
 <xref:System.IO.Compression.ZipFile>   
 <xref:System.IO.Compression.ZipArchiveEntry>   
 <xref:System.IO.Compression.DeflateStream>   
 <xref:System.IO.Compression.GZipStream>   
 [文件和流 I\/O](../../../docs/standard/io/index.md)