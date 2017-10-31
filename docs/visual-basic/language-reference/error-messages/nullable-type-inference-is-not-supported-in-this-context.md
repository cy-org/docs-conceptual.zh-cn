---
title: "该上下文中不支持可以为 null 的类型推理 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc36629"
  - "bc36629"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36629"
ms.assetid: 0a1e2dbc-d9a4-433d-9306-c5540782b81d
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# 该上下文中不支持可以为 null 的类型推理
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

可以将值类型和结构声明为可以为空。  
  
```vb#  
Dim a? As Integer  
Dim b As Integer?  
```  
  
 但是，不能将可以为 null 的声明与类型推理一起使用。  下面的示例将导致此错误。  
  
```vb#  
' Not valid.  
' Dim c? = 10  
' Dim d? = a  
```  
  
 **错误 ID：**BC36629  
  
### 更正此错误  
  
-   使用 `As` 子句将变量声明为可以为 null。  
  
## 请参阅  
 [可以为 Null 的值类型](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)   
 [局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)