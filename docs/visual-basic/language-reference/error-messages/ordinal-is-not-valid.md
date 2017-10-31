---
title: "序号无效 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID452"
dev_langs: 
  - "VB"
ms.assetid: 7459562b-cd4f-4590-95e0-6126ae3589a5
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 序号无效
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

通过使用 `#num` 语法，标明调用动态链接库 \(DLL\) 应使用数字而不是过程名称。  此错误有以下可能的原因：  
  
-   尝试将 `#num` 表达式转换为序号失败。  
  
-   指定的 `#num` 不指定 DLL 中的任何函数。  
  
-   类型库中有一个无效声明，导致内部使用了一个无效的序号。  
  
### 更正此错误  
  
1.  确保表达式表示的数字有效，或者按名称调用过程。  
  
2.  确保 `#num` 标识了 DLL 中的一个有效函数。  
  
3.  通过注释代码，将导致问题的过程调用隔离。  编写过程的 `Declare` 语句，并将问题报告给类型库供应商。  
  
## 请参阅  
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)