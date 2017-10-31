---
title: "错误的文件模式 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID54"
dev_langs: 
  - "VB"
ms.assetid: 74891e96-884b-4c8d-872d-cd11ae272372
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 错误的文件模式
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

操作文件内容时所使用的语句必须适合于文件打开的模式。  可能的原因包括：  
  
-   `FilePutObject` 或 `FileGetObject` 语句指定了一个顺序文件。  
  
-   `Print` 语句指定了一个以 `Output` 或 `Append` 之外的访问模式打开的文件。  
  
-   `Input` 语句指定了一个以 `Input` 之外的访问模式打开的文件  
  
-   尝试写入只读文件。  
  
### 更正此错误  
  
-   确保 `FilePutObject` 和 `FileGetObject` 只引用以 `Random` 或 `Binary` 访问模式打开的文件。  
  
-   确保 `Print` 指定一个以 `Output` 或 `Append` 访问模式打开的文件。  如果不是，请使用其他语句将数据放在文件中，或以适当模式重新打开文件。  
  
-   确保 `Input` 指定一个以 `Input` 模式打开的文件。  如果不是，请使用其他语句将数据放在文件中或以适当模式重新打开文件。  
  
-   如果要写入只读文件，请更改文件的读\/写状态或不尝试写入文件。  
  
-   使用 `My.Computer.FileSystem` 对象中的可用功能。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileSystem>   
 [疑难解答：读取和写入文本文件](../../../visual-basic/developing-apps/programming/drives-directories-files/troubleshooting-reading-from-and-writing-to-text-files.md)