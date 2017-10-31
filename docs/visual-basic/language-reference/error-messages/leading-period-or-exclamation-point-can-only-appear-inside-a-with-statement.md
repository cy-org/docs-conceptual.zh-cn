---
title: "前导“.”或“!”只能出现在“With”语句内 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30157"
  - "bc30157"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30157"
ms.assetid: 70daaee1-14f9-45b7-9f30-53794310b95e
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 前导“.”或“!”只能出现在“With”语句内
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

句点 \(.\) 或感叹号 \(\!\) 不在 `With` 块内，并且其左边没有表达式。  成员访问 \(`.`\) 和字典成员访问 \(`!`\) 要求用一个表达式来指定包含成员的元素。  该表达式必须紧靠在访问器的左边或作为包含成员访问的 `With` 块的目标。  
  
 **错误 ID：**BC30157  
  
### 更正此错误  
  
1.  确保此 `With` 块的格式正确。  
  
2.  如果没有 `With` 块，则在访问器的左边添加一个计算为包含成员的定义元素的表达式。  
  
## 请参阅  
 [代码中的特殊字符](../../../visual-basic/programming-guide/program-structure/special-characters-in-code.md)   
 [With...End With 语句](../../../visual-basic/language-reference/statements/with-end-with-statement.md)