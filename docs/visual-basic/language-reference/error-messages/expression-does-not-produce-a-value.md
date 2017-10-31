---
title: "表达式不产生值 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30491"
  - "bc30491"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30491"
ms.assetid: 8399d7ae-bc0a-49e6-81dc-2e7229708bc9
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 表达式不产生值
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

尝试在生成值的上下文中使用不生成值的表达式，例如在需要使用 `Function` 的地方调用 `Sub`。  
  
 **错误 ID：**BC30491  
  
### 更正此错误  
  
-   将表达式更改为生成值的表达式。  
  
## 请参阅  
 [错误类型](../../../visual-basic/programming-guide/language-features/error-types.md)