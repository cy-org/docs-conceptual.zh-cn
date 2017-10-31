---
title: "除数为零（Visual Basic 运行时错误） | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID11"
ms.assetid: 5b9bc5d6-792e-48bc-a974-012e07ad95f3
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 除数为零（Visual Basic 运行时错误）
用作除数的表达式有一个值为零。  
  
### 更正此错误  
  
1.  检查表达式中变量的拼写是否正确。 拼写错误的变量名可能会隐式创建一个初始化为零的数值变量。  
  
2.  检查之前对表达式中的变量进行的操作，尤其是那些从其他过程作为参数传递给该过程的操作。  
  
## 请参阅  
 [通过值和通过引用传递参数](../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Parameter Passing Mechanism Changes in Visual Basic](http://msdn.microsoft.com/zh-cn/0fa2b0dc-aa1c-4797-bbd6-aa13c611cab2)