---
title: "属性“&lt;属性名&gt;”的“Set”访问器不可访问 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc31102"
  - "bc31102"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31102"
ms.assetid: 6f7b31b7-3656-4ae1-8851-90f5f4c6950a
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 属性“&lt;属性名&gt;”的“Set”访问器不可访问
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

语句尝试在无权访问某个属性的 `Set` 过程时存储该属性的值。  
  
 如果 [Set 语句](../../../visual-basic/language-reference/statements/set-statement.md) 标记有限制性比其 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md) 更强的访问级别，在以下情况中，尝试设置属性值的操作可能会失败：  
  
-   `Set` 语句被标记为 [Private](../../../visual-basic/language-reference/modifiers/private.md)，并且调用代码位于其中定义了属性的类或结构的外部。  
  
-   `Set` 语句被标记为 [Protected](../../../visual-basic/language-reference/modifiers/protected.md)，并且调用代码既不在其中定义了属性的类或结构中，也不在派生类中。  
  
-   `Set` 语句被标记为 [Friend](../../../visual-basic/language-reference/modifiers/friend.md)，并且调用代码所在的程序集与其中定义了属性的程序集不同。  
  
 **错误 ID：**BC31102  
  
### 更正此错误  
  
-   如果能够控制定义属性的源代码，请考虑使用与属性本身相同的访问级别声明 `Set` 过程。  
  
-   如果无法控制定义属性的源代码，或者必须使 `Set` 过程访问级别的限制性比属性本身更强，请尝试将设置属性值的语句移到可更好地访问属性的代码区域中。  
  
## 请参阅  
 [Property 过程](../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [如何：声明具有混合访问级别的属性](../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)