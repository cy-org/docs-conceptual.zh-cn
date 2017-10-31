---
title: "参数“NPer”必须大于零 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrRate_NPerMustBeGTZero"
ms.assetid: d49242df-dbd1-4b26-bd8c-ed56d24fdfcd
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 参数“NPer”必须大于零
返回一个指定基于定期固定付款和固定利率的年金的期间数的 `Double` 的 `NPer` 函数要求一个大于零的参数。  
  
### 更正此错误  
  
-   检查表达式中参数的拼写是否正确。 拼写错误的变量名可能会隐式创建一个初始化为零的数值变量。  
  
-   检查之前对表达式中的变量进行的操作，尤其是那些从其他过程作为参数传递给该过程的操作。  
  
## 请参阅  
 [不在生成中：NPer 函数](http://msdn.microsoft.com/zh-cn/56567d16-29f7-4928-b05f-b4cd56d4fd42)   
 [通过值和通过引用传递参数](../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)