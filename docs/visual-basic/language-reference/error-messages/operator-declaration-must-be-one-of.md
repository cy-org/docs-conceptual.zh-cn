---
title: "运算符声明必须是以下符号之一：+、-、*、\、/、^、&amp;、Like、Mod、And、Or、Xor、Not、&lt;&lt;、&gt;&gt;、=、&lt;&gt;、&lt;、&lt;=、&gt;、&gt;=、CType、IsTrue、IsFalse | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc33000"
  - "vbc33000"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC33000"
ms.assetid: 15c5d8eb-3a8c-4141-8f41-33151afabf97
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 运算符声明必须是以下符号之一：+、-、*、\、/、^、&amp;、Like、Mod、And、Or、Xor、Not、&lt;&lt;、&gt;&gt;、=、&lt;&gt;、&lt;、&lt;=、&gt;、&gt;=、CType、IsTrue、IsFalse
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

您只能声明适合重载的运算符。  下表列出了您可以声明的运算符。  
  
|类型|运算符|  
|--------|---------|  
|一元|`+`, `-`, `IsFalse`, `IsTrue`, `Not`|  
|Binary|`+`, `-`, `*`, `/`, `\`, `&`, `^`, `>>`, `<<`, `=`, `<>`, `>`, `>=`, `<`, `<=`, `And`, `Like`, `Mod`, `Or`, `Xor`|  
|转换（一元）|`CType`|  
  
 请注意，二元列表中的 `=` 运算符是比较运算符，而不是赋值运算符。  
  
 **错误 ID：**BC33000  
  
### 更正此错误  
  
1.  从可重载的运算符的集合中选择一个运算符。  
  
2.  如果需要能重载一个无法直接重载的运算符的功能，则创建一个 `Function` 过程，该过程获取适当的参数并返回适当的值。  
  
## 请参阅  
 [Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md)   
 [运算符过程](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [如何：定义运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [如何：定义转换运算符](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)