---
title: "参数“Life”不能为零 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrFinancial_LifeNEZero"
ms.assetid: c402da97-a2b2-4219-a83a-0cebbfdffef2
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# 参数“Life”不能为零
`Life` 的参数（必须为指定资产的使用年限的长度的 `Double`）无效。  
  
### 更正此错误  
  
-   检查表达式中参数的拼写是否正确。 拼写错误的变量名可能会隐式创建一个初始化为零的数值变量。  
  
-   检查之前对表达式中的变量进行的操作，尤其是那些从其他过程作为参数传递给该过程的操作。  
  
## 请参阅  
 [不在生成中：DDB 函数](http://msdn.microsoft.com/zh-cn/c7cf8929-d158-4399-b3cb-31d897d12556)   
 [不在生成中：SYD 函数](http://msdn.microsoft.com/zh-cn/23c25672-f5dd-49ac-9893-4faa82634181)   
 [不在生成中：SLN 函数](http://msdn.microsoft.com/zh-cn/8e06130a-056e-4266-a8a9-1592b86f58d2)   
 [通过值和通过引用传递参数](../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)