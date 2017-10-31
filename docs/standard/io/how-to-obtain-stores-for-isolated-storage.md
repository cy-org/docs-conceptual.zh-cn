---
title: "如何：获取独立存储的存储区 | Microsoft Docs"
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
  - "存储区，获取"
  - "使用独立存储来存储数据，获取存储区"
  - "独立存储，获取存储区"
  - "数据存储区，获取"
  - "使用独立存储的数据存储，获取存储区"
ms.assetid: fcb6b178-d526-47c4-b029-e946f880f9db
caps.latest.revision: 19
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 19
---
# 如何：获取独立存储的存储区
隔离存储区公开数据隔离舱中的虚拟文件系统。  <xref:System.IO.IsolatedStorage.IsolatedStorageFile> 类提供许多与独立存储区交互的方法。  为了创建和检索存储区，<xref:System.IO.IsolatedStorage.IsolatedStorageFile> 提供了三种静态方法。  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForAssembly%2A>返回按用户和程序集隔离的存储区。  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForDomain%2A> 可返回按域和程序集隔离的存储区。  
  
     这两种方法检索属于代码块（是从该代码块中调用这两种方法的）的存储区。  
  
-   静态方法 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> 返回通过传入范围参数组合指定的独立存储区。  
  
 下面的代码示例返回按用户、程序集和域隔离的存储区。  
  
 [!code-cpp[Conceptual.IsolatedStorage#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source6.cpp#6)]
 [!code-csharp[Conceptual.IsolatedStorage#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source6.cs#6)]
 [!code-vb[Conceptual.IsolatedStorage#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source6.vb#6)]  
  
 可以使用<xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A>方法来指定存储区应该和漫游用户配置文件一起漫游。  有关如何设置这个的详细信息，请参见 [隔离的类型](../../../docs/standard/io/types-of-isolation.md)。  
  
 默认情况下，从不同的程序集中获得的独立存储区是不同的。  通过在<xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> 方法的参数中的程序集或域证据传递，可以访问不同程序集或域的存储区。  这需要访问按应用程序域标识隔离的独立存储的权限。  有关更多信息，请参见 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> 方法重载。  
  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForAssembly%2A>, <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForDomain%2A>，和<xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A>方法返回一个<xref:System.IO.IsolatedStorage.IsolatedStorageFile>对象。  要帮助您确定哪种隔离类型最适合您的情况，请参见[隔离的类型](../../../docs/standard/io/types-of-isolation.md)。  当具有了独立存储文件对象之后，便可以使用独立存储方法来读取、写入、创建和删除文件及文件目录了。  
  
 没有一种机制可用来防止代码向没有足够访问权限来自己获取存储区的代码传递 <xref:System.IO.IsolatedStorage.IsolatedStorageFile>对象。  只有当获得对 <xref:System.IO.IsolatedStorage.IsolatedStorage> 对象的引用时（通常是在 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForAssembly%2A>、<xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForDomain%2A> 或 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> 方法中），才检查域和程序集标识及独立存储权限。  因此，使用这些引用的代码应该负责保护对 <xref:System.IO.IsolatedStorage.IsolatedStorageFile> 对象的引用。  
  
## 示例  
 下面的代码提供了是一个非常简单的包含按用户和程序集隔离的存储区类的示例。  通过向<xref:System.IO.IsolatedStorage.IsolatedStorageScope?displayProperty=fullName>方法传递添加 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A>方法传递的参数，此代码可更改为检索按用户、域和程序集隔离的存储区。  
  
 运行代码之后，您可以通过在命令行中键入 **StoreAdm \/LIST** 来确认已创建了存储区。  这将运行[Isolated Storage tool \(Storeadm.exe\)](../../../docs/framework/tools/storeadm-exe-isolated-storage-tool.md)并列出用户当前所有的独立存储区。  
  
 [!code-cpp[Conceptual.IsolatedStorage#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source6.cpp#7)]
 [!code-csharp[Conceptual.IsolatedStorage#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source6.cs#7)]
 [!code-vb[Conceptual.IsolatedStorage#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source6.vb#7)]  
  
## 请参阅  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile>   
 <xref:System.IO.IsolatedStorage.IsolatedStorageScope>   
 [独立存储](../../../docs/standard/io/isolated-storage.md)   
 [隔离的类型](../../../docs/standard/io/types-of-isolation.md)   
 [公共语言运行时中的程序集](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)