---
title: "可选参数必须指定默认值 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30812"
  - "bc30812"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30812"
ms.assetid: 5091a250-be66-413b-98a3-2a9974c4d600
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 可选参数必须指定默认值
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

可选参数必须提供默认值，以便调用过程未提供参数时可使用此默认值。  
  
 **错误 ID：**BC30812  
  
### 更正此错误  
  
-   为可选参数指定默认值；例如：  
  
    ```  
    Sub Proc1(ByVal X As Integer,   
          Optional ByVal Y As String = "Default Value")  
       MsgBox("Default argument is: " & Y)  
    End Sub  
    ```  
  
## 请参阅  
 [Optional](../../../visual-basic/language-reference/modifiers/optional.md)