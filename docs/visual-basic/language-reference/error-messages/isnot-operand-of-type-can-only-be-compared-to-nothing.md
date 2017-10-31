---
title: "类型“typename”的操作数“IsNot”只能与“Nothing”比较，因为“typename”是一个可以为 null 的类型 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc32128"
  - "vbc32128"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32128"
ms.assetid: 1155b23a-ad75-4bab-b9da-73f35c767a36
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# 类型“typename”的操作数“IsNot”只能与“Nothing”比较，因为“typename”是一个可以为 null 的类型
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

使用 `IsNot` 运算符对声明为可以为 null 的变量与非 `Nothing` 的表达式进行了比较。  
  
 **错误 ID：**BC32128  
  
### 更正此错误  
  
1.  若要使用 `IsNot` 运算符对可以为 null 的类型与非 `Nothing` 的表达式进行比较，请对可以为 null 的类型调用 `GetType` 方法，并将结果与表达式进行比较，如下面的示例所示。  
  
    ```vb#  
    Dim number? As Integer = 5  
  
    If number IsNot Nothing Then  
      If number.GetType() IsNot Type.GetType("System.Int32") Then   
  
      End If  
    End If  
    ```  
  
## 请参阅  
 [可以为 Null 的值类型](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)   
 [IsNot 运算符](../../../visual-basic/language-reference/operators/isnot-operator.md)