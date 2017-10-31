---
title: "变量“&lt;变量名&gt;”在封闭块中隐藏变量 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30616"
  - "bc30616"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30616"
ms.assetid: e7658ebc-da45-451b-a409-a0f8915f0beb
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 变量“&lt;变量名&gt;”在封闭块中隐藏变量
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

块中包含的一个变量与另一个局部变量同名。  
  
 **错误 ID：**BC30616  
  
### 更正此错误  
  
-   重命名封闭块中的变量，使其名称不同于其他任何局部变量。  例如：  
  
    ```  
    Dim a, b, x As Integer  
    If a = b Then  
       Dim y As Integer = 20 ' Uniquely named block variable.  
    End If  
    ```  
  
-   此错误的常见原因是在事件处理程序内使用 `Catch e As Exception`。  如果的确如此，请将 `Catch` 块变量命名为 `ex` 而不是 `e`。  
  
-   此错误的另一个常见来源是尝试在单独的 `Catch` 块中访问在 `Try` 块内声明的局部变量。  若要更正这一错误，请在 `Try...Catch...Finally` 结构之外声明该变量。  
  
## 请参阅  
 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [变量声明](../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)