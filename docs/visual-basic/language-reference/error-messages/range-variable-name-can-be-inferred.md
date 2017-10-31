---
title: "只能根据不带参数的简单名称或限定名称推断范围变量名称 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc36599"
  - "bc36599"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36599"
ms.assetid: 17763dbe-f74f-4ccb-8086-cb7e45ec4d12
caps.latest.revision: 6
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 6
---
# 只能根据不带参数的简单名称或限定名称推断范围变量名称
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

带有一个或多个参数的编程元素包括在 LINQ 查询中。  编译器无法从该编程元素推断范围变量。  
  
 **错误 ID：**BC36599  
  
### 更正此错误  
  
1.  为编程元素提供一个显式变量名称，如下面的代码所示：  
  
```  
Dim query = From var1 In collection1   
            Select VariableAlias = SampleFunction(var1), var1  
```  
  
## 请参阅  
 [Visual Basic 中的 LINQ 简介](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Select 子句](../../../visual-basic/language-reference/queries/select-clause.md)