---
title: "如何：引用对象的当前实例 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "当前实例"
  - "实例, 引用当前"
  - "对象变量"
  - "对象 [Visual Basic], 引用当前实例"
  - "变量 [Visual Basic], 对象"
ms.assetid: 7f9b2c77-03cd-428f-adc2-b18070226e7c
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# 如何：引用对象的当前实例 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

对象的*“当前实例”*是指代码当前正在其中执行的实例。  
  
 使用 `Me` 关键字可以引用当前实例。  
  
### 引用当前实例  
  
-   在通常使用对象变量名的位置使用 `Me` 关键字。  
  
    ```  
    Me.ForeColor = System.Drawing.Color.Crimson  
    Me.Close()  
    ```  
  
     尽管 `Me` 的行为与对象变量一样，但还是不能对它进行声明或向它分配任何内容。  `Me` 始终引用当前实例。  
  
## 请参阅  
 [对象变量](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [对象变量赋值](../../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)   
 [Me、My、MyBase 和 MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)