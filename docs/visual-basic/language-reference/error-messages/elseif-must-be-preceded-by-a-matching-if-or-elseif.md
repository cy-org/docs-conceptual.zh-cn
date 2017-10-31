---
title: "“#ElseIf”前面必须是匹配的“#If”或“#ElseIf” | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30014"
  - "bc30014"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30014"
ms.assetid: 5215585e-2efa-485a-9efe-9833a1cc83a0
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# “#ElseIf”前面必须是匹配的“#If”或“#ElseIf”
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

`#ElseIf` 是条件编译指令。  `#ElseIf` 子句前面必须是匹配的 `#If` 或 `#ElseIf` 子句。  
  
 **错误 ID：**BC30014  
  
### 更正此错误  
  
1.  请检查：插入的条件编译块或放置有误的 `#End If` 尚未将前面的 `#If`  或 `#ElseIf` 与此 `#ElseIf` 分隔开。  
  
2.  如果 `#ElseIf` 在 `#Else` 指令的后面，请移除 `#Else` 或将其更改为 `#ElseIf`。  
  
3.  如果其他所有内容的顺序都正确，请在条件编译块的开始处添加一个 `#If` 指令。  
  
## 请参阅  
 [\#If...Then...\#Else 指令](../../../visual-basic/language-reference/directives/if-then-else-directives.md)