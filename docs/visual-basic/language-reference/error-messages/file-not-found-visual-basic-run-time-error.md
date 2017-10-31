---
title: "找不到文件（Visual Basic 运行时错误） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID53"
dev_langs: 
  - "VB"
ms.assetid: 57addb16-6f9a-444d-8af8-dda52431daca
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 找不到文件（Visual Basic 运行时错误）
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定的位置找不到该文件。  此错误可能的原因包括：  
  
-   某个语句引用的文件不存在。  
  
-   尝试调用动态链接库 \(DLL\) 中的过程，但无法找到 `Declare` 语句的 `Lib` 子句中指定的库。  
  
-   尝试打开的项目或尝试加载的文本文件不存在。  
  
### 更正此错误  
  
1.  检查文件名和路径规格的拼写是否正确。  
  
## 请参阅  
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)