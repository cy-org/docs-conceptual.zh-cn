---
title: "How to: Create Pre-Computed Tasks | Microsoft Docs"
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
  - "tasks, creating pre-computed"
ms.assetid: a73eafa2-1f49-4106-a19e-997186029b58
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# How to: Create Pre-Computed Tasks
该文档描述如何使用 <xref:System.Threading.Tasks.Task.FromResult%2A?displayProperty=fullName> 方法去检索缓存中包含的异步下载运算结果。  <xref:System.Threading.Tasks.Task.FromResult%2A> 方法返回将提供的值作为其 <xref:System.Threading.Tasks.Task%601.Result%2A> 属性的已完成的<xref:System.Threading.Tasks.Task%601> 对象。  执行返回 <xref:System.Threading.Tasks.Task%601> 对象的异步运算，且已计算该 <xref:System.Threading.Tasks.Task%601> 对象的结果时，此方法将十分有用。  
  
## 示例  
 下面的示例从 Web下载的字符串。  它定义了 `DownloadStringAsync` 方法。  此方法从 Web 上异步下载字符串。  此示例还使用 <xref:System.Collections.Concurrent.ConcurrentDictionary%602> 对象缓存先前操作的结果。  如果输入地址已缓存，`DownloadStringAsync` 使用 <xref:System.Threading.Tasks.Task.FromResult%2A> 方法在该地址产生包含其内容的<xref:System.Threading.Tasks.Task%601> 对象。  否则，`DownloadStringAsync` 从 Web 下载文件并将结果添加到缓存。  
  
 [!code-csharp[TPL_CachedDownloads#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_cacheddownloads/cs/cacheddownloads.cs#1)]
 [!code-vb[TPL_CachedDownloads#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_cacheddownloads/vb/cacheddownloads.vb#1)]  
  
 此示例计算下载多个字符两次需要的时间。  因为结果已在缓存中，第二组下载操作应比第一次用了较少的时间。  <xref:System.Threading.Tasks.Task.FromResult%2A> 方法允许 `DownloadStringAsync` 方法创建包含之前这些计算结果的 <xref:System.Threading.Tasks.Task%601> 对象。  
  
## 编译代码  
 复制该代码示例，并将其粘贴到 Visual Studio项目中或名为  `CachedDownloads.cs` \(`CachedDownloads.vb` for [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) 的文件中，然后在Visual Studio命令提示符窗口中运行以下命令。  
  
 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)]  
  
 **csc.exe CachedDownloads.cs**  
  
 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]  
  
 **vbc.exe CachedDownloads.vb**  
  
## 可靠编程  
  
## 请参阅  
 [Task Parallelism](../../../docs/standard/parallel-programming/task-based-asynchronous-programming.md)