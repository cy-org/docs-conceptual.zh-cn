---
title: "“&lt;成员名&gt;”在继承接口“&lt;接口名 1&gt;”和“&lt;接口名 2&gt;”之间不明确 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30685"
  - "bc30685"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30685"
ms.assetid: 756add7a-23d5-4b4f-a48d-8297d6459c73
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# “&lt;成员名&gt;”在继承接口“&lt;接口名 1&gt;”和“&lt;接口名 2&gt;”之间不明确
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

此接口从多个接口继承了两个或多个同名的成员。  
  
 **错误 ID：**BC30685  
  
### 更正此错误  
  
-   将值转换为要使用的基接口；例如：  
  
    ```  
    Interface Left  
        Sub MySub()  
    End Interface  
  
    Interface Right  
        Sub MySub()  
    End Interface  
  
    Interface LeftRight  
        Inherits Left, Right  
    End Interface  
  
    Module test  
        Sub Main()  
            Dim x As LeftRight  
            ' x.MySub()  'x is ambiguous.  
            CType(x, Left).MySub() ' Cast to base type.  
            CType(x, Right).MySub() ' Call the other base type.  
        End Sub  
    End Module  
    ```  
  
## 请参阅  
 [接口](../../../visual-basic/programming-guide/language-features/interfaces/index.md)