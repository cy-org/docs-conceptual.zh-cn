---
title: "索引数超过索引数组的维数 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30106"
  - "vbc30106"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30106"
ms.assetid: 2c5363e1-62c2-4f5a-b675-c7337aeb363d
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 索引数超过索引数组的维数
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

用于访问数组元素的索引数必须与该数组的秩（即为该数组声明的维数）完全相同。  
  
 **错误 ID：**BC30106  
  
### 更正此错误  
  
-   减少数组引用下标，直到下标总数等于数组的秩为止。  例如：  
  
    ```  
    [Visual Basic]  
    Dim gameBoard(3, 3) As String  
  
    ' Incorrect code. The array has two dimensions.  
    gameBoard(1, 1, 1) = "X"  
    gameBoard(2, 1, 1) = "O"  
  
    ' Correct code.  
    gameBoard(0, 0) = "X"  
    gameBoard(1, 0) = "O"  
    ```  
  
## 请参阅  
 [数组](../../../visual-basic/programming-guide/language-features/arrays/index.md)