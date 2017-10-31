---
title: "声明为结构成员的数组不能用初始大小声明 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc31043"
  - "bc31043"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31043"
ms.assetid: 5bd90c71-1b78-444b-91e1-4789451ef085
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 声明为结构成员的数组不能用初始大小声明
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

使用初始大小声明结构中的数组。  您不能初始化任何结构元素，而声明数组大小就是一种初始化形式。  
  
 **错误 ID：**BC31043  
  
### 更正此错误  
  
1.  将结构中的数组定义为动态数组（不是初始大小）。  
  
2.  如果需要特定大小的数组，可以在代码运行时使用 [ReDim 语句](../../../visual-basic/language-reference/statements/redim-statement.md) 重新设置动态数组的维数。  下面的示例阐释了这一点。  
  
    ```  
    Structure demoStruct  
        Public demoArray() As Integer  
    End Structure  
    Sub useStruct()  
        Dim struct As demoStruct  
        ReDim struct.demoArray(9)  
        Struct.demoArray(2) = 777  
    End Sub  
    ```  
  
## 请参阅  
 [数组](../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [如何：声明结构](../../../visual-basic/programming-guide/language-features/data-types/how-to-declare-a-structure.md)