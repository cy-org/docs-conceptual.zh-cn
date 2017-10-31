---
title: "Lambda 表达式在“Select Case”语句的第一个表达式中无效 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc36635"
  - "vbc36635"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36635"
ms.assetid: 74609979-9c03-4864-bbce-f588aa2e0917
caps.latest.revision: 6
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 6
---
# Lambda 表达式在“Select Case”语句的第一个表达式中无效
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

不能在 `Select Case` 语句中使用测试表达式的 lambda 表达式。  Lambda 表达式定义返回函数，`Select Case` 语句的测试表达式必须是基本数据类型。  
  
 下面的代码导致此错误：  
  
```vb#  
' Select Case (Function(arg) arg Is Nothing)  
    ' List of the cases.  
' End Select  
```  
  
 **错误 ID：**BC36635  
  
### 更正此错误  
  
-   检查代码以确定其他条件结构（如 `If...Then...Else` 语句）对您是否有用。  
  
-   您可能故意调用该函数，如下面的代码所示：  
  
    ```vb#  
    Dim num? As Integer  
    Select Case ((Function(arg? As Integer) arg Is Nothing)(num))  
        ' List of the cases  
    End Select  
    ```  
  
## 请参阅  
 [lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)   
 [If...Then...Else 语句](../../../visual-basic/language-reference/statements/if-then-else-statement.md)   
 [Select...Case 语句](../../../visual-basic/language-reference/statements/select-case-statement.md)