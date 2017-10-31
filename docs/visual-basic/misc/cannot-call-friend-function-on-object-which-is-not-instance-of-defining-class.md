---
title: "在不是定义类的实例的对象上不能调用友元函数 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID97"
ms.assetid: b9d821f0-8565-4f15-bb35-184789c69662
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 在不是定义类的实例的对象上不能调用友元函数
尝试调用某个类的 `Friend` 过程，或者尝试跨进程或跨线程访问 `Friend` 属性或方法。`Friend` 过程可从类外部的模块中调用，但该模块是在其中定义该类的项目的一部分。  
  
### 更正此错误  
  
-   确保从模块中调用或访问该过程，此模块是在其中定义该类的项目的一部分。  
  
## 请参阅  
 [Friend](../../visual-basic/language-reference/modifiers/friend.md)