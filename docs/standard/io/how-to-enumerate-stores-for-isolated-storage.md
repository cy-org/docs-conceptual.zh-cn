---
title: "如何：枚举独立存储的存储区 | Microsoft Docs"
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
  - "枚举存储区"
  - "使用独立存储的数据存储，枚举存储区"
  - "使用独立存储来存储数据，枚举存储区"
  - "存储区，枚举"
  - "独立存储，枚举存储区"
  - "数据存储区，枚举"
ms.assetid: 0fcf279a-f241-48f0-8034-2e3d331f1fcb
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：枚举独立存储的存储区
您可以使用  <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A?displayProperty=fullName>静态方法来枚举当前用户的所有独立存储区。  该方法取<xref:System.IO.IsolatedStorage.IsolatedStorageScope>值并且返回<xref:System.IO.IsolatedStorage.IsolatedStorageFile>枚举数。  若要枚举存储区，您必须具有指定<xref:System.Security.Permissions.IsolatedStorageContainment> 值 AdministerIsolatedStorageByUser 的<xref:System.Security.Permissions.IsolatedStorageFilePermission>的权限。  如果调用使用 <xref:System.IO.IsolatedStorage.IsolatedStorageScope> 值的 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A> 方法，它返回一组为当前用户定义的 <xref:System.IO.IsolatedStorage.IsolatedStorageFile> 对象。  
  
## 示例  
 使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A> 方法，所以下面的代码示例获得按用户和程序集隔离的存储区，创建一些文件，并检索这些文件。  
  
 [!code-csharp[Conceptual.IsolatedStorage#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source2.cs#2)]
 [!code-vb[Conceptual.IsolatedStorage#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source2.vb#2)]  
  
## 请参阅  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile>   
 [独立存储](../../../docs/standard/io/isolated-storage.md)