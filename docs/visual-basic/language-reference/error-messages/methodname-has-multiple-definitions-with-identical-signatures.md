---
title: "“&lt;方法名&gt;”具有多个带有相同签名的定义 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30269"
  - "bc30269"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30269"
ms.assetid: 39489621-6617-4e5c-9b24-c2faf8273891
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# “&lt;方法名&gt;”具有多个带有相同签名的定义
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

`Function` 或 `Sub` 过程声明使用的过程名和参数列表与以前的声明相同。  一个可能的原因是尝试重载原始过程。  重载过程必须具有不同的参数列表。  
  
 **错误 ID：**BC30269  
  
### 更正此错误  
  
-   更改过程名或参数列表，或移除重复声明。  
  
## 请参阅  
 [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [重载过程注意事项](../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md)