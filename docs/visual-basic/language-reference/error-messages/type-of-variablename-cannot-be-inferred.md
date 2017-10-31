---
title: "无法推断“&lt;变量名&gt;”的类型，因为循环边界和步骤变量未扩大到同一类型 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30982"
  - "vbc30982"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30982"
ms.assetid: 741e85d9-a747-42ad-a1e1-a3f1928aaff5
caps.latest.revision: 30
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 30
---
# 无法推断“&lt;变量名&gt;”的类型，因为循环边界和步骤变量未扩大到同一类型
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

已经编写 `For...Next` 循环，由于存在以下情况，在该循环中编译器无法推断循环控制变量的数据类型：  
  
-   没有用 `As` 子句指定循环控制变量的数据类型。  
  
-   循环边界和步骤变量至少包含两种数据类型。  
  
-   数据类型之间不存在标准转换。  
  
 因此，编译器无法推断循环的控制变量的数据类型。  
  
 在下面的示例中，步骤变量是一个字符，循环边界都是整数。  因为字符与整数之间不存在标准转换，所以会报告此错误。  
  
```vb#  
Dim stepVar = "1"c  
Dim m = 0  
Dim n = 20  
  
' Not valid.  
' For i = 1 To 10 Step stepVar  
    ' Loop processing  
' Next  
```  
  
 **错误 ID：**BC30982  
  
### 更正此错误  
  
-   根据需要更改循环边界和步骤变量的类型，至少使其中之一为其他项所扩大成的类型。  在前面的示例中，将 `stepVar` 的类型更改为 `Integer`。  
  
    ```  
    Dim stepVar = 1  
    ```  
  
     \- 或 \-  
  
    ```  
    Dim stepVar As Integer = 1  
    ```  
  
-   使用显式转换函数以将循环边界和步骤变量转换为相应的类型。  在前面的示例中，将 `Val` 函数应用于 `stepVar`。  
  
    ```  
    For i = 1 To 10 Step Val(stepVar)  
        ' Loop processing  
    Next  
    ```  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Conversion.Val%2A>   
 [For...Next 语句](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [隐式转换和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Option Infer 语句](../../../visual-basic/language-reference/statements/option-infer-statement.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)