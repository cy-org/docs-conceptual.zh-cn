---
title: "输入超出文件尾 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID62"
dev_langs: 
  - "VB"
ms.assetid: 65292704-6e7d-4622-9f50-eb655a59b016
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 输入超出文件尾
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

`Input` 语句正在读取的文件为空或其中的所有数据都已使用，或者对为进行二进制访问而打开的文件使用了 `EOF` 函数。  
  
### 更正此错误  
  
1.  紧靠 `Input` 语句之前使用 `EOF` 函数以检测文件的结尾。  
  
2.  如果文件是为进行二进制访问而打开的，则使用 `Seek` 和 `Loc`。  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.FileSystem.Input%2A>   
 <xref:Microsoft.VisualBasic.FileSystem.EOF%2A>   
 <xref:Microsoft.VisualBasic.FileSystem.Seek%2A>   
 <xref:Microsoft.VisualBasic.FileSystem.Loc%2A>