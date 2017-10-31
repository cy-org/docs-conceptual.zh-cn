---
title: "只能从不带参数的简单名或限定名中推断匿名类型成员名称 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc36556"
  - "bc36556"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36556"
ms.assetid: e3ba1f33-3a71-4f03-9b04-ed5ec17de17c
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 只能从不带参数的简单名或限定名中推断匿名类型成员名称
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

无法从复杂表达式推断匿名类型成员名称。  
  
```vb#  
Dim numbers() As Integer = {1, 2, 3, 4, 5}  
' Not valid.  
' Dim instanceName1 = New With {numbers(3)}  
```  
  
 有关匿名类型能够和无法从其推断成员名称和类型的源的更多信息，请参见[如何：推断匿名类型声明中的属性名和类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)。  
  
 **错误 ID：**BC36556  
  
### 更正此错误  
  
-   将该表达式赋给某个成员名称，如下面的代码所示：  
  
    ```  
    Dim instanceName2 = New With {.number = numbers(3)}  
    ```  
  
## 请参阅  
 [匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [如何：推断匿名类型声明中的属性名和类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-infer-property-names-and-types-in-anonymous-type-declarations.md)