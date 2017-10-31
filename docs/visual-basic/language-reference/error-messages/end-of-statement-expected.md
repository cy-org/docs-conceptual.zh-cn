---
title: "需要语句结束 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30205"
  - "vbc30205"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30205"
ms.assetid: 53c7f825-a737-4b76-a1fa-f67745b8bd40
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 需要语句结束
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

语句的语法完整，但在语句结束的元素后面有一个附加编程元素。  每个语句的末尾都必须有一个行结束符。  
  
 行结束符部件 Visual Basic 源文件的字符为行。  行结束符的示例是 Unicode 回车符 \(&HD\)，Unicode 换行符 \(&HA\)，并且，Unicode Unicode 换行符后面的字符回车符。  有关行结束符的更多信息，请参见 [Visual Basic 语言规范](../../../visual-basic/reference/language-specification.md)。  
  
 **错误 ID：**BC30205  
  
### 更正此错误  
  
1.  检查是否在同一行中不慎放入了两个不同的语句。  
  
2.  在语句结束的元素后面插入一个行结束符。  
  
## 请参阅  
 [如何：在代码中拆分和合并语句](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)