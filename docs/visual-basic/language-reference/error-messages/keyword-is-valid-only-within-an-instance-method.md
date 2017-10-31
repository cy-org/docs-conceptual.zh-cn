---
title: "“&lt;关键字&gt;”只在实例方法中有效 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30043"
  - "vbc30043"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30043"
ms.assetid: 7973aa82-a681-440c-9bca-242627d7ba86
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# “&lt;关键字&gt;”只在实例方法中有效
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

`Me`、`MyClass` 和 `MyBase` 关键字引用特定的类实例。  不能将其用在共享的 `Function` 或 `Sub` 过程中。  
  
 **错误 ID：**BC30043  
  
### 更正此错误  
  
-   从过程中移除相应的关键字，或从过程声明中移除 `Shared` 关键字。  
  
## 请参阅  
 [对象变量赋值](../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)   
 [Me、My、MyBase 和 MyClass](../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)   
 [继承的基础知识](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)