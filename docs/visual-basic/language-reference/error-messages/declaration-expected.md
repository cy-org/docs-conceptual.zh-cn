---
title: "需要声明 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30188"
  - "bc30188"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30188"
ms.assetid: da6b1df3-fe6b-4415-88e6-0977e5189e0b
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 需要声明
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

非声明性语句（如赋值语句或循环语句）出现在过程外。  只有声明可以位于过程外。  
  
 或者，编程元素没有用声明关键字（如 `Dim` 或 `Const`）进行声明。  
  
 **错误 ID：**BC30188  
  
### 更正此错误  
  
-   将非声明语句移到过程体内。  
  
-   用适当的声明关键字开始声明。  
  
-   确保声明关键字未拼写错误。  
  
## 请参阅  
 [过程](../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)