---
title: "标识符太长 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30033"
  - "vbc30033"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30033"
ms.assetid: 3d07f6d0-9a2f-49ca-94e8-1e354932e855
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 标识符太长
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

每个编程元素的名称或标识符限制为 1023 个字符。  此外，完全限定名不能超过 1023 个字符。  这意味着，整个标识符字符串 \(`<namespace>.<...>.<namespace>.<class>.<element>`\) 的长度不能超过 1023 个字符，包括成员访问运算符 \(`.`\) 字符。  
  
 **错误 ID：**BC30033  
  
### 更正此错误  
  
-   减小标识符的长度。  
  
## 请参阅  
 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)