---
title: "文件和流 I/O"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IO namespace
- files, I/O
- System.IO namespace
- I/O [.NET Framework]
- streams, I/O
- data streams, I/O
ms.assetid: 4f4a33a9-66b7-4cd7-a285-4ad3e4276cd2
caps.latest.revision: 33
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: fbd31e6bff5502291fd24b57b55c81046da330d3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/05/2017

---
# <a name="file-and-stream-io"></a>文件和流 I/O
文件和流 I/O（输入/输出）是指在存储媒介中传入或传出数据。 在 .NET Framework 中，[System.IO](http://go.microsoft.com/fwlink/?LinkId=231142) 命名空间包含允许以异步方式和同步方式对数据流和文件进行读取和写入操作的类型。 这些命名空间还包含对文件执行压缩和解压缩的类型，以及通过管道和串行端口启用通信的类型。  
  
 文件是一个由字节组成的有序的命名集合，它具有永久存储。 在处理文件时，你将处理目录路径、磁盘存储、文件和目录名称。 相反，流是一个字节序列，可用于对后备存储进行读取和写入操作，后备存储可以是多个存储媒介之一（例如，磁盘或内存）。 正如存在除磁盘之外的多种后备存储一样，也存在除文件流之外的多种流（如网络、内存和管道流）。  
  
## <a name="files-and-directories"></a>文件和目录  
 你可以使用 <xref:System.IO?displayProperty=fullName> 命名空间中的类型与文件和目录进行交互。 例如，你可以获取和设置文件和目录的属性，并基于搜索条件检索文件和目录的集合。  
  
 下面是一些常用的文件和目录类：  
  
-   <xref:System.IO.File> - 提供用于创建、复制、删除、移动和打开文件的静态方法，并可帮助创建 <xref:System.IO.FileStream> 对象。  
  
-   <xref:System.IO.FileInfo> - 提供用于创建、复制、删除、移动和打开文件的实例方法，并可帮助创建 <xref:System.IO.FileStream> 对象。  
  
-   <xref:System.IO.Directory> - 提供用于创建、移动和枚举目录和子目录的静态方法。  
  
-   <xref:System.IO.DirectoryInfo> - 提供用于创建、移动和枚举目录和子目录的实例方法。  
  
-   <xref:System.IO.Path> - 提供用于以跨平台的方式处理目录字符串的方法和属性。  
  
 除了使用这些类之外，Visual Basic 用户还可以对文件 I/O 使用 <xref:Microsoft.VisualBasic.FileIO.FileSystem?displayProperty=fullName> 类提供的方法和属性。  
  
 请参阅[如何：复制目录](../../../docs/standard/io/how-to-copy-directories.md)、[如何：创建目录列表](http://msdn.microsoft.com/en-us/4d2772b1-b991-4532-a8a6-6ef733277e69)和[如何：枚举目录和文件](../../../docs/standard/io/how-to-enumerate-directories-and-files.md)。  
  
## <a name="streams"></a>流  
 抽象基类 <xref:System.IO.Stream> 支持读取和写入字节。 所有表示流的类都继承自 <xref:System.IO.Stream> 类。 <xref:System.IO.Stream> 类及其派生类提供数据源和存储库的常见视图，使程序员不必了解操作系统和基础设备的具体细节。  
  
 流涉及三个基本操作：  
  
-   读取 - 将数据从流传输到数据结构（如字节数组）中。  
  
-   写入 - 将数据从数据源传输到流。  
  
-   查找 - 对流中的当前位置进行查询和修改。  
  
 根据基础数据源或存储库，流可能只支持这些功能中的一部分。 例如，<xref:System.IO.Pipes.PipeStream> 类不支持查找。 流的 <xref:System.IO.Stream.CanRead%2A>、<xref:System.IO.Stream.CanWrite%2A> 和 <xref:System.IO.Stream.CanSeek%2A> 属性指定流支持的操作。  
  
 下面是一些常用的流类：  
  
-   <xref:System.IO.FileStream> - 用于对文件进行读取和写入操作。  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> - 用于对独立存储中的文件进行读取或写入操作。  
  
-   <xref:System.IO.MemoryStream> - 用于作为后备存储对内存进行读取和写入操作。  
  
-   <xref:System.IO.BufferedStream> - 用于改进读取和写入操作的性能。  
  
-   <xref:System.Net.Sockets.NetworkStream> - 用于通过网络套接字进行读取和写入。  
  
-   <xref:System.IO.Pipes.PipeStream> - 用于通过匿名和命名管道进行读取和写入。  
  
-   <xref:System.Security.Cryptography.CryptoStream> - 用于将数据流链接到加密转换。  
  
 有关异步使用流的示例，请参阅[异步文件 I/O](../../../docs/standard/io/asynchronous-file-i-o.md)。  
  
## <a name="readers-and-writers"></a>读取器和编写器  
 <xref:System.IO?displayProperty=fullName> 命名空间还提供用于在流中读取和写入已编码字符的类型。 通常，流用于字节输入和输出。 读取器和编写器类型处理编码字符与字节之间的来回转换，以便流可以完成操作。 每个读取器和编写器类都与流关联，可以通过类的 `BaseStream` 属性进行检索。  
  
 下面是一些常用的读取器和编写器类：  
  
-   <xref:System.IO.BinaryReader> 和 <xref:System.IO.BinaryWriter> - 用于将基元数据类型作为二进制值进行读取和写入。  
  
-   <xref:System.IO.StreamReader> 和 <xref:System.IO.StreamWriter> - 用于通过使用编码值在字符和字节之间来回转换来读取和写入字符。  
  
-   <xref:System.IO.StringReader> 和 <xref:System.IO.StringWriter> - 用于从字符串读取字符以及将字符写入字符串中。  
  
-   <xref:System.IO.TextReader> 和 <xref:System.IO.TextWriter> - 用作其他读取器和编写器（读取和写入字符和字符串，而不是二进制数据）的抽象基类。  
  
 请参阅[如何：从文件读取文本](../../../docs/standard/io/how-to-read-text-from-a-file.md)、[如何：向文件写入文本](../../../docs/standard/io/how-to-write-text-to-a-file.md)、[如何：从字符串中读取字符](../../../docs/standard/io/how-to-read-characters-from-a-string.md)和[如何：向字符串写入字符](../../../docs/standard/io/how-to-write-characters-to-a-string.md)。  
  
## <a name="asynchronous-io-operations"></a>异步 I/O 操作  
 读取或写入大量数据会占用大量资源。 如果你的应用程序需要保持对用户的响应性，则你应异步执行这些任务。 在执行同步 I/O 操作时，UI 线程将受阻，直至完成占用大量资源的操作。  在开发 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用时使用异步 I/O 操作可防止造成应用程序已停止工作的印象。  
  
 异步成员在其名称中包含 `Async`，如 <xref:System.IO.Stream.CopyToAsync%2A>、<xref:System.IO.Stream.FlushAsync%2A>、<xref:System.IO.Stream.ReadAsync%2A> 和 <xref:System.IO.Stream.WriteAsync%2A> 方法。 你可以将这些方法与 `async` 和 `await` 关键字一起使用。  
  
 有关详细信息，请参阅[异步文件 I/O](../../../docs/standard/io/asynchronous-file-i-o.md)。  
  
## <a name="compression"></a>压缩  
 压缩是指减小文件大小以便存储的过程。 解压缩是提取压缩文件的内容以使这些内容采用可用格式的过程。 <xref:System.IO.Compression?displayProperty=fullName> 命名空间包含用于对文件和流进行压缩或解压缩的类型。  
  
 在对文件和流进行压缩和解压缩时，经常使用以下类：  
  
-   <xref:System.IO.Compression.ZipArchive> - 用于在 zip 存档中创建和检索条目。  
  
-   <xref:System.IO.Compression.ZipArchiveEntry> - 用于表示压缩文件。  
  
-   <xref:System.IO.Compression.ZipFile> - 用于创建、提取和打开压缩包。  
  
-   <xref:System.IO.Compression.ZipFileExtensions> - 用于创建和提供压缩包中的条目。  
  
-   <xref:System.IO.Compression.DeflateStream> - 用于使用 Deflate 算法对流进行压缩和解压缩。  
  
-   <xref:System.IO.Compression.GZipStream> - 用于采用 gzip 数据格式对流进行压缩和解压缩。  
  
 请参阅[如何：压缩和提取文件](../../../docs/standard/io/how-to-compress-and-extract-files.md)。  
  
## <a name="isolated-storage"></a>独立存储  
 独立存储是一种数据存储机制，它在代码与保存的数据之间定义了标准化的关联方式，从而提供隔离性和安全性。 存储提供按用户、程序集和（可选）域隔离的虚拟文件系统。 当你的应用程序无权访问用户文件时，独立存储特别有用。 你可以通过一种由计算机的安全策略控制的方式保存应用程序的设置或文件。  
  
 独立存储不可用于 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 应用；请改用 [Windows.Storage](http://msdn.microsoft.com/library/windows/apps/windows.storage.aspx) 命名空间中的应用程序数据类。 有关详细信息，请参阅 Windows 开发人员中心中的[应用程序数据](http://go.microsoft.com/fwlink/?LinkId=229175)。  
  
 在实现独立存储时，经常使用以下类：  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorage> - 提供用于独立存储实现的基类。  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorageFile> - 提供包含文件和目录的独立存储区。  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream> - 公开独立存储中的文件。  
  
 请参阅[独立存储](../../../docs/standard/io/isolated-storage.md)。  
  
## <a name="io-operations-in-windows-store-apps"></a>Windows 应用商店应用程序中的 I/O 操作  
 [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] 包含许多用于对流进行读取和写入操作的类型；但是，该集不包含所有的 .NET Framework I/O 类型。  
  
 在 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用中使用 I/O 操作时，要注意一些重要差异：  
  
-   专门与文件操作相关的类型（如 <xref:System.IO.File>、<xref:System.IO.FileInfo>、<xref:System.IO.Directory> 和 <xref:System.IO.DirectoryInfo>）未包含在[!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] 中。 请改用 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 的 [Windows.Storage](http://msdn.microsoft.com/library/windows/apps/windows.storage.aspx) 命名空间中的类型，如 [StorageFile](http://msdn.microsoft.com/library/windows/apps/windows.storage.storagefile.aspx) 和 [StorageFolder](http://msdn.microsoft.com/library/windows/apps/windows.storage.storagefolder.aspx)。  
  
-   独立存储不可用；请改用[应用程序数据](http://go.microsoft.com/fwlink/?LinkId=229175)。  
  
-   使用异步方法（如 <xref:System.IO.Stream.ReadAsync%2A> 和 <xref:System.IO.Stream.WriteAsync%2A>）可防止 UI 线程受阻。  
  
-   基于路径的压缩类型 <xref:System.IO.Compression.ZipFile> 和 <xref:System.IO.Compression.ZipFileExtensions> 不可用。 请改用 [Windows.Storage.Compression](http://msdn.microsoft.com/library/windows/apps/windows.storage.compression.aspx) 命名空间中的类型。  
  
 如果需要，你可以在 .NET Framework 流和 Windows 运行时流之间进行转换。 有关详细信息，请参阅[如何：在 .NET Framework 流和 Windows 运行时流之间进行转换](../../../docs/standard/io/how-to-convert-between-dotnet-streams-and-winrt-streams.md)或 [System.IO.WindowsRuntimeStreamExtensions](https://msdn.microsoft.com/library/system.io.windowsruntimestreamextensions.aspx)。 <!--zz TODO: <xref:System.IO.WindowsRuntimeStreamExtensions>--> 
  
 若要深入了解 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 应用中的 I/O 操作，请参阅 Windows 开发人员中心的[快速入门：读取和写入文件](http://go.microsoft.com/fwlink/p/?LinkId=243072)。  
  
## <a name="io-and-security"></a>I/O 和安全性  
 在使用 <xref:System.IO?displayProperty=fullName> 命名空间中的类时，你必须遵循操作系统安全性要求（如访问控制列表 (ACL)）来控制对文件和目录的访问。 此要求是在所有 <xref:System.Security.Permissions.FileIOPermission> 要求之外的要求。 可以用编程方式管理 ACL。 有关详细信息，请参阅[如何：添加或移除访问控制列表项](../../../docs/standard/io/how-to-add-or-remove-access-control-list-entries.md)。  
  
 默认安全策略将阻止 Internet 或 Intranet 应用程序访问用户计算机上的文件。 因此，在编写将通过 Internet 或 Intranet 下载的代码时，请不要使用需要物理文件路径的 I/O 类。 请转而将[独立存储](../../../docs/standard/io/isolated-storage.md)用于传统 .NET Framework 应用程序，或将[应用程序数据](http://go.microsoft.com/fwlink/?LinkId=229175)用于 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 应用。  
  
 仅在构造流时执行安全性检查。 因此，请不要打开流并将其传递给受信程度较低的代码或应用程序域。  
  
## <a name="related-topics"></a>相关主题  
  
-   [通用 I/O 任务](../../../docs/standard/io/common-i-o-tasks.md)  
  
 提供与文件、目录和流关联的 I/O 任务的列表以及指向每个任务的相关内容和示例的链接。  
  
-   [异步文件 I/O](../../../docs/standard/io/asynchronous-file-i-o.md)  
  
 描述异步 I/O 的性能优势和基本操作。  
  
-   [独立存储](../../../docs/standard/io/isolated-storage.md)  
  
 描述一种数据存储机制，该机制通过定义标准的代码与保存数据的关联方式来提供隔离和安全性。  
  
-   [管道](../../../docs/standard/io/pipe-operations.md)  
  
 描述 .NET Framework 中的匿名和命名管道操作。  
  
-   [内存映射文件](../../../docs/standard/io/memory-mapped-files.md)  
  
 描述内存映射文件，这些文件包含虚拟内存中磁盘上文件的内容。 可以使用内存映射文件编辑非常大的文件和创建共享内存以进行进程间通信。

