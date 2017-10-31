---
title: "文件已打开 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID55"
dev_langs: 
  - "VB"
ms.assetid: d674a0fb-ef16-4cc2-9da7-709a8a07dbea
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# 文件已打开
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

有时必须在另一个 `FileOpen` 或其他操作开始前，关闭文件。  该错误可能的原因包括：  
  
-   为已打开的文件执行了顺序输出模式 `FileOpen`  
  
-   某个语句引用了一个已打开的文件。  
  
### 更正此错误  
  
1.  执行该语句之前，先关闭文件。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileSystem.FileOpen%2A>