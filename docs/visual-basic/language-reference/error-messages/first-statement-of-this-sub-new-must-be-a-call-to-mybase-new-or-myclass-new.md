---
title: "该“Sub New”的第一个语句必须是对“MyBase.New”或“MyClass.New”的调用（没有不带参数的可访问构造函数） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30148"
  - "vbc30148"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30148"
ms.assetid: 4426e8fc-cb39-4eb8-ba95-503cd32fcc89
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 该“Sub New”的第一个语句必须是对“MyBase.New”或“MyClass.New”的调用（没有不带参数的可访问构造函数）
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

“\<derivedname\>”的基类“\<basename\>”没有不使用参数就可以调用的可访问“Sub New”，因此该“Sub New”的第一个语句必须是对“MyBase.New”或“MyClass.New”的调用。  
  
 在派生类中，每个构造函数必须调用基类构造函数 \(`MyBase.New`\)。  如果该基类有一个可由派生类访问的不带参数的构造函数，则可以自动调用 `MyBase.New`。  否则，基类构造函数必须带参数调用，而这无法自动执行。  在此情况下，每个派生类构造函数的第一个语句必须调用基类上的一个参数化构造函数，或在调用基类构造函数的派生类中调用另一个构造函数。  
  
 **错误 ID：**BC30148  
  
### 更正此错误  
  
-   调用提供所需参数的 `MyBase.New`，或调用执行此类调用的对等构造函数。  
  
     例如，因此，如果基类具有声明为 `Public Sub New(ByVal index as Integer)`的构造函数，在派生类构造函数的第一个语句可能是 `MyBase.New(100)`。  
  
## 请参阅  
 [继承的基础知识](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)