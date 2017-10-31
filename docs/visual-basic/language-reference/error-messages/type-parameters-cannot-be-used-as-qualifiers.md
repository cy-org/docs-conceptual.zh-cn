---
title: "类型参数不能用作限定符 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc32098"
  - "bc32098"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32098"
ms.assetid: bab05325-dde8-4621-a5f6-368b5b7b2d76
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 类型参数不能用作限定符
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

使用包括类型参数的限定字符串限定了编程元素。  
  
 类型参数代表要在构造泛型类型时提供的类型的要求。  它不代表具体的已定义类型。  限定字符串必须只包括在编译时定义的元素。  
  
 以下语句可能会产生此错误。  
  
```  
Public Function checkText(Of c As System.Windows.Forms.Control)(  
    ByVal badText As String) As Boolean  
  
    Dim saveText As c.Text  
    ' Insert code to look for badText within saveText.  
End Function  
```  
  
 **错误 ID：**BC32098  
  
### 更正此错误  
  
1.  从限定字符串中移除类型参数，或将其替换为某个已定义类型。  
  
2.  如果需要使用构造的类型来定位所限定的编程元素，您必须使用附加程序逻辑。  
  
## 请参阅  
 [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [类型列表](../../../visual-basic/language-reference/statements/type-list.md)