---
title: "需要对象 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID424"
dev_langs: 
  - "VB"
ms.assetid: afdc660b-81a5-4c92-ac7e-9c3a3105fc16
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 需要对象 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

对属性和方法的引用通常需要显式的对象限定符。  该错误属于这种情况。  
  
### 更正此错误  
  
1.  检查对对象属性或方法的引用是否具有有效的对象限定符。  如果没有提供对象限定符，请指定一个。  
  
2.  检查对象限定符的拼写，并确保在引用它的程序部分中对象是可见的。  
  
3.  如果要为宿主应用程序的 **File Open** 命令提供路径，请检查其中的参数是否正确。  
  
4.  检查对象的文档并确保操作有效。  
  
## 请参阅  
 [错误类型](../../../visual-basic/programming-guide/language-features/error-types.md)