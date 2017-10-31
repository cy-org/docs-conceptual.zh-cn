---
title: "嵌套函数没有与委托“&lt;委托名&gt;”兼容的签名。 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc36532"
  - "bc36532"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36532"
ms.assetid: 493f292c-d81e-40ef-8b47-61f020571829
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# 嵌套函数没有与委托“&lt;委托名&gt;”兼容的签名。
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

已将 lambda 表达式分配给具有不兼容签名的委托。  例如，在下面的代码中，委托 `Del` 具有两个整数参数。  
  
```vb#  
Delegate Function Del(ByVal p As Integer, ByVal q As Integer) As Integer  
```  
  
 如果将具有一个参数的 lambda 表达式声明为 `Del` 类型，则将引发错误：  
  
```vb#  
' Neither of these is valid.   
' Dim lambda1 As Del = Function(n As Integer) n + 1  
' Dim lambda2 As Del = Function(n) n + 1  
```  
  
 **错误 ID：**BC36532  
  
### 更正此错误  
  
-   调整委托定义或分配的 lambda 表达式，以便签名兼容。  
  
## 请参阅  
 [宽松委托转换](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)   
 [lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)