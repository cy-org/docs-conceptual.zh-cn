---
title: "“#Region”和“#End Region”语句在方法体/多行 lambda 内无效 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc32025"
  - "vbc32025"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32025"
ms.assetid: 43707bf1-1c6b-4d82-b081-e5a17dca51c1
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# “#Region”和“#End Region”语句在方法体/多行 lambda 内无效
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

必须在类、模块或命名空间级声明 `#Region` 块。  可折叠区域可以包含一个或多个过程，但它不能在过程内开始或结束。  
  
 **错误 ID：**BC32025  
  
### 更正此错误  
  
1.  确保已用 `End Function` 或 `End Sub` 语句正确终止前置过程。  
  
2.  确保 `#Region` 和 `#End Region` 指令在同一代码块中。  
  
## 请参阅  
 [\#Region 指令](../../../visual-basic/language-reference/directives/region-directive.md)