---
title: "不再支持“Line”语句（Visual Basic 编译器错误） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30830"
  - "vbc30830"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30830"
ms.assetid: 4734bc1d-882e-4555-b498-1f1ec0399d16
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 不再支持“Line”语句（Visual Basic 编译器错误）
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

不再支持 Line 语句。  文件 I\/O 功能可用作 `Microsoft.VisualBasic.FileSystem.LineInput`，而图形功能可用作 `System.Drawing.Graphics.DrawLine`。  
  
 **错误 ID：**BC30830  
  
### 更正此错误  
  
1.  如果执行文件访问，请使用 `Microsoft.VisualBasic.FileSystem.LineInput`。  
  
2.  如果执行图形处理，请使用 `System.Drawing.Graphics.Drawline`。  
  
## 请参阅  
 <xref:System.IO>   
 <xref:System.Drawing>   
 [使用 Visual Basic 访问文件](../../../visual-basic/developing-apps/programming/drives-directories-files/file-access.md)