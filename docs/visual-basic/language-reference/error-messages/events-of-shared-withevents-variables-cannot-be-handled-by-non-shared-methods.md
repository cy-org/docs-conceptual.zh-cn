---
title: "共享 WithEvents 变量的事件不能由非共享方法处理 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30594"
  - "vbc30594"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30594"
ms.assetid: 5b9fceb4-ab11-41bb-ad3b-6f1a9da8ae7e
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 共享 WithEvents 变量的事件不能由非共享方法处理
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

用 `Shared` 修饰符声明的变量为共享变量。  共享变量精确标识一个存储位置。  以 `WithEvents` 修饰符声明的变量断言变量所属的类型要处理变量引发的事件集。  在为变量赋值后，由 `WithEvents` 声明所创建的属性与任何现有事件处理程序解除挂钩，并通过 `Add` 方法与新的事件处理程序挂钩。  
  
 **错误 ID：**BC30594  
  
### 更正此错误  
  
-   将事件处理程序声明为 `Shared`。  
  
## 请参阅  
 [Shared](../../../visual-basic/language-reference/modifiers/shared.md)   
 [WithEvents](../../../visual-basic/language-reference/modifiers/withevents.md)