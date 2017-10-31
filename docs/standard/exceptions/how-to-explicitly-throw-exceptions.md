---
title: "如何：显式引发异常 | Microsoft Docs"
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
  - "异常, 引发"
  - "异常, try/catch 块"
  - "FileNotFoundException 类"
  - "隐式引发异常"
  - "try/catch 块"
ms.assetid: 72bdd157-caa9-4478-9ee3-cb4500b84528
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：显式引发异常
可以使用 `throw` 语句显式引发异常。  还可以使用 `throw` 语句再次引发捕获的异常。  较好的编码做法是，向再次引发的异常添加信息以在调试时提供更多信息。  
  
 下面的代码示例使用 try\/catch 块捕获可能的 <xref:System.IO.FileNotFoundException>。  try 块后面是 catch 块，catch 块捕获 <xref:System.IO.FileNotFoundException>，如果找不到数据文件，则向控制台写入消息。  下一条语句是 throw 语句，该语句引发新的 <xref:System.IO.FileNotFoundException> 并向该异常添加文本信息。  
  
## 示例  
 [!code-csharp[Exception.Throwing#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Exception.Throwing/CS/throw.cs#1)]
 [!code-vb[Exception.Throwing#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Exception.Throwing/VB/throw.vb#1)]  
  
## 请参阅  
 [如何：使用 Try\/Catch 块捕捉异常](../../../docs/standard/exceptions/how-to-use-the-try-catch-block-to-catch-exceptions.md)   
 [如何：在 Catch 块中使用特定异常](../../../docs/standard/exceptions/how-to-use-specific-exceptions-in-a-catch-block.md)   
 [如何：使用 Finally 块](../../../docs/standard/exceptions/how-to-use-finally-blocks.md)   
 [异常处理基础知识](../../../docs/standard/exceptions/exception-handling-fundamentals.md)