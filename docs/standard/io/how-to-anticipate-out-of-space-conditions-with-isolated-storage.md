---
title: "如何：预见独立存储中的空间不足条件 | Microsoft Docs"
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
  - "数据存储区，配额"
  - "独立存储，配额"
  - "使用的独立存储的数量"
  - "对使用的独立存储的限制"
  - "存储，配额"
  - "存储，空间用尽状况"
  - "使用独立存储的数据存储，配额"
  - "使用独立存储来存储数据，配额"
  - "独立存储中的剩余空间"
  - "数据存储，空间用尽状况"
  - "使用独立存储来存储数据，区空间用尽状况"
  - "独立存储的配额"
  - "独立存储，空间用尽状况"
  - "使用独立存储的数据存储，区空间用尽状况"
ms.assetid: e35d4535-3732-421e-b1a3-37412e036145
caps.latest.revision: 17
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：预见独立存储中的空间不足条件
使用独立存储的代码受[配额](../../../docs/standard/io/isolated-storage.md#quotas)的限制，该配额指定独立存储文件和目录所在的数据隔离舱的最大大小。  该限额由安全策略确定，管理员可以对其进行配置。  如果尝试写入数据时超过了所允许的最大大小，将引发 <xref:System.IO.IsolatedStorage.IsolatedStorageException>异常并使操作失败。  这有助于防止恶意的拒绝服务攻击，此类攻击会导致应用程序因数据存储区被填满而拒绝请求。  
  
 为了帮助您确定给定的写入尝试是否会因此原因而失败，<xref:System.IO.IsolatedStorage.IsolatedStorage> 类提供了三种只读属性：<xref:System.IO.IsolatedStorage.IsolatedStorage.AvailableFreeSpace%2A>、<xref:System.IO.IsolatedStorage.IsolatedStorage.UsedSize%2A> 和 <xref:System.IO.IsolatedStorage.IsolatedStorage.Quota%2A>。  这些属性可用于确定写入存储区是否将导致超过存储区所允许的最大大小。  记住独立存储可能被同时访问；因此，如果当计算剩余存储量时，则该存储空间可能在您尝试写入存储区时已被使用。  但是，这可以使用存储区的最大大小来确定是否将达到可用存储的上限。  
  
 <xref:System.IO.IsolatedStorage.IsolatedStorage.Quota%2A> 属性依赖程序集中的证据来确保正常工作。  因此，只应在使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForAssembly%2A>、 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetUserStoreForDomain%2A> 或 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetStore%2A> 方法创建的 <xref:System.IO.IsolatedStorage.IsolatedStorageFile> 对象上检索此属性。  以其他任何方式创建的 <xref:System.IO.IsolatedStorage.IsolatedStorageFile> 对象（例如从 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A> 方法返回的对象）将无法返回准确的最大大小值。  
  
## 示例  
 下面的代码示例获取独立存储、创建几个文件并检索 <xref:System.IO.IsolatedStorage.IsolatedStorage.AvailableFreeSpace%2A> 属性。  以字节数报告剩余的空间。  
  
 [!code-cpp[Conceptual.IsolatedStorage#8](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.isolatedstorage/cpp/source7.cpp#8)]
 [!code-csharp[Conceptual.IsolatedStorage#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source7.cs#8)]
 [!code-vb[Conceptual.IsolatedStorage#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source7.vb#8)]  
  
## 请参阅  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile>   
 [独立存储](../../../docs/standard/io/isolated-storage.md)   
 [如何：获取独立存储的存储区](../../../docs/standard/io/how-to-obtain-stores-for-isolated-storage.md)