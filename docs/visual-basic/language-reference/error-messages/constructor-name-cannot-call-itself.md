---
title: "构造函数“&lt;名称&gt;”不能调用自身 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30298"
  - "vbc30298"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30298"
ms.assetid: 2d77b7f4-0640-4f89-9c65-f101fd2847c0
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 构造函数“&lt;名称&gt;”不能调用自身
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

类或结构中的 `Sub New` 过程调用自身。  
  
 构造函数的用途是：在首次创建类或结构时初始化该类或结构的实例。  类或结构可以有多个构造函数，前提是这些构造函数都具有不同的参数列表。  允许构造函数调用其他构造函数来执行它自己功能以外的功能。  但是，构造函数调用自身是没有意义的，实际上，如果允许调用自身，将导致无限递归。  
  
 **错误 ID：**BC30298  
  
### 更正此错误  
  
1.  检查正被调用构造函数的参数列表。  该列表应该与执行调用的构造函数的参数列表不同。  
  
2.  如果不打算调用其他构造函数，请完全移除 `Sub New` 调用。  
  
## 请参阅  
 [对象生存期：如何创建和销毁对象](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)