---
title: "需要“Optional” | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30202"
  - "vbc30202"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30202"
ms.assetid: 6f75060c-2db4-4a79-b5d1-5780c09a74cd
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 需要“Optional”
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

过程声明中某个可选参数后面有一个必选参数。  可选参数后面的每个参数也都必须是可选的。  
  
 **错误 ID：**BC30202  
  
### 更正此错误  
  
1.  如果此参数是作为必选的参数提供，则将其移到参数列表中第一个可选参数的前面。  
  
2.  如果此参数是作为可选参数提供的，则使用 `Optional` 关键字。  
  
## 请参阅  
 [可选参数](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md)