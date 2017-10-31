---
title: "此数组被固定或临时锁定 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID10"
dev_langs: 
  - "VB"
ms.assetid: de6713a6-51d7-4edb-8515-d5fb544e2091
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 此数组被固定或临时锁定 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

此错误有以下可能的原因：  
  
-   使用 `ReDim` 更改固定大小数组的元素个数。  
  
-   重新定义模块级动态数组的尺寸，而其中的一个元素已作为参数传递给过程。  如果元素已传递，数组将被锁定，以防止为过程内的引用参数释放内存。  
  
-   尝试将值赋给包含数组的 `Variant` 变量，但是 `Variant` 当前被锁定。  
  
### 更正此错误  
  
1.  使用 `ReDim` 重新声明原来的数组（如果该数组在过程内声明），或声明该数组但不指定元素个数（如果数组在模块级声明），以确保该数组是动态的而非固定的。  
  
2.  确定是否真的需要传递元素，因为该元素可以在模块的所有过程中内可见。  
  
3.  确定锁定 `Variant` 的源并更正它。  
  
## 请参阅  
 [数组](../../../visual-basic/programming-guide/language-features/arrays/index.md)