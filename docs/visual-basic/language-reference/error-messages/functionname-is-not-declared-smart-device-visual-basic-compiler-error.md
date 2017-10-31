---
title: "未声明“&lt;函数名&gt;”（智能设备/Visual Basic 编译器错误） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30766"
  - "vbc30766"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30766"
ms.assetid: 13918600-6087-40d7-8134-32aa9d3bfda4
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# 未声明“&lt;函数名&gt;”（智能设备/Visual Basic 编译器错误）
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

\<`functionname`\> 未声明。  通常，在 `Microsoft.VisualBasic` 命名空间中提供文件 I\/O 功能，但 .NET Compact Framework 的目标版本不支持该功能。  
  
 **错误 ID：**BC30766  
  
### 更正此错误  
  
-   使用 `System.IO` 命名空间中定义的函数来执行文件操作。  
  
## 请参阅  
 <xref:System.IO>   
 [使用 Visual Basic 访问文件](../../../visual-basic/developing-apps/programming/drives-directories-files/file-access.md)