---
title: "参数“Period”必须小于或等于参数“Life” | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrFinancial_PeriodLELife"
ms.assetid: dc575d41-b376-4b05-bbbe-6de1e98385f1
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 参数“Period”必须小于或等于参数“Life”
`Period` 参数的值（指定计算资产折旧的时期）大于 `Life` 参数的值。  
  
### 更正此错误  
  
-   确保 `Life` 和 `Period` 参数以相同的单位表示。 例如，如果 `Life` 以月为单位，则 `Period` 也应以月为单位。  
  
## 请参阅  
 [不在生成中：DDB 函数](http://msdn.microsoft.com/zh-cn/c7cf8929-d158-4399-b3cb-31d897d12556)   
 [不在生成中：SYD 函数](http://msdn.microsoft.com/zh-cn/23c25672-f5dd-49ac-9893-4faa82634181)   
 [通过值和通过引用传递参数](../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)