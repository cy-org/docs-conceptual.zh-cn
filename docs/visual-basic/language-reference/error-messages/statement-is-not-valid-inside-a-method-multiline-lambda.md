---
title: "语句在方法/多行 lambda 内无效 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30024"
  - "bc30024"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30024"
ms.assetid: 758e7a8f-429b-42c1-9a78-778e5b480e04
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 语句在方法/多行 lambda 内无效
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

该语句在 `Sub`、`Function`、属性 `Get` 或属性 `Set` 过程中无效。  某些语句可以出现在类或模块级。  其他语句（例如 `Option Strict`）必须位于命名空间级并在其他所有声明的前面。  
  
 **错误 ID：**BC30024  
  
### 更正此错误  
  
-   从过程中移除该语句。  
  
## 请参阅  
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Get 语句](../../../visual-basic/language-reference/statements/get-statement.md)   
 [Set 语句](../../../visual-basic/language-reference/statements/set-statement.md)