---
title: "结构“&lt;结构名&gt;”至少必须包含一个实例成员变量或至少必须包含一个未标记为“Custom”的实例事件声明 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30941"
  - "vbc30941"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30941"
ms.assetid: 7054cc1e-bac3-4c3d-82f3-35772bd8dd3b
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 结构“&lt;结构名&gt;”至少必须包含一个实例成员变量或至少必须包含一个未标记为“Custom”的实例事件声明
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

结构定义不包含任何非共享变量或非共享的非自定义事件。  
  
 每个结构必须有一个变量或事件，该变量或事件应用于各个特定实例（非共享），而不是整体应用于所有实例 \([Shared](../../../visual-basic/language-reference/modifiers/shared.md)\)。  非共享的常数、属性和过程不能满足此要求。  此外，如果没有共享变量并且只有一个非共享事件，则该事件不能是 `Custom` 事件。  
  
 **错误 ID：**BC30941  
  
### 更正此错误  
  
-   定义至少一个不是 `Shared` 的变量或事件。  如果只定义一个事件，则它必须是非自定义的且非共享的。  
  
## 请参阅  
 [结构](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [如何：声明结构](../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)   
 [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md)