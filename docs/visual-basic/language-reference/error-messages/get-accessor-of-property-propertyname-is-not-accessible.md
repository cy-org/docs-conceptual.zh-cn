---
title: "属性“&lt;属性名&gt;”的“Get”访问器不可访问 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc31103"
  - "bc31103"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31103"
ms.assetid: 3c346c32-7669-4b04-841d-7a9df9cb703e
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 属性“&lt;属性名&gt;”的“Get”访问器不可访问
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

尝试检索属性值的语句没有属性的 `Get` 过程的访问权限。  
  
 如果 [Get 语句](../../../visual-basic/language-reference/statements/get-statement.md) 的访问级别比其 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md) 的访问级别严格，在以下情况下尝试读取属性值可能会失败：  
  
-   `Get` 语句标记为 [Private](../../../visual-basic/language-reference/modifiers/private.md)，而调用代码位于定义属性的类或结构之外。  
  
-   `Get` 语句标记为 [Protected](../../../visual-basic/language-reference/modifiers/protected.md)，而调用代码不在定义属性的类或结构中，也不在派生类中。  
  
-   `Get` 语句标记为 [Friend](../../../visual-basic/language-reference/modifiers/friend.md)，而调用代码不在定义属性的程序集中。  
  
 **错误 ID：**BC31103  
  
### 更正此错误  
  
-   如果能够控制定义属性的源代码，请考虑为属性和 `Get` 过程声明相同的访问级别。  
  
-   如果不能控制定义属性的源代码，或必须为 `Get` 声明比属性更为严格的访问级别，可尝试将读取属性值的语句移到具有更高属性访问权限的代码区域中。  
  
## 请参阅  
 [Property 过程](../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [如何：声明具有混合访问级别的属性](../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)