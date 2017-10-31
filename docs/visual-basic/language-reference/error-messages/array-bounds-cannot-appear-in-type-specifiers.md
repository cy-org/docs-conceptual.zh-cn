---
title: "数组界限不能出现在类型说明符中 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30638"
  - "bc30638"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30638"
ms.assetid: 93b654f4-70fa-4a48-baed-ffae42075550
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 数组界限不能出现在类型说明符中
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

不能将数组大小声明为数据类型说明符的一部分。  
  
 **错误 ID：**BC30638  
  
### 更正此错误  
  
-   紧跟在变量名之后指定数组大小，而不要将其置于类型之后，如下例所示。  
  
    ```  
    Dim Array(8) As Integer   
    ```  
  
-   定义一个数组，并将其初始值设置为要求的元素个数，如下例所示。  
  
    ```  
    Dim Array2() As Integer = New Integer(8) {}  
    ```  
  
## 请参阅  
 [数组](../../../visual-basic/programming-guide/language-features/arrays/index.md)