---
title: "“&lt;事件名&gt;”是事件，不能直接调用 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc32022"
  - "vbc32022"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32022"
ms.assetid: 4dcfcb8d-a9fa-46a7-a034-29d9ff3a59b3
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# “&lt;事件名&gt;”是事件，不能直接调用
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

“\<`eventname`\>”是事件，不能直接调用。  请使用 `RaiseEvent` 语句引发事件。  
  
 过程调用将事件指定为过程名称。  事件处理程序是一个过程，但事件本身是信号设备，需要进行触发并处理。  
  
 **错误 ID：**BC32022  
  
### 更正此错误  
  
1.  使用 `RaiseEvent` 语句触发事件并调用处理它的一个或多个过程。  
  
## 请参阅  
 [RaiseEvent 语句](../../../visual-basic/language-reference/statements/raiseevent-statement.md)