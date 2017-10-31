---
title: "错误的 DLL 调用约定 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrID49"
dev_langs: 
  - "VB"
ms.assetid: 7c7def45-b0ab-450f-ad3f-4383dfd9aed7
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# 错误的 DLL 调用约定
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

传递给动态链接库 \(DLL\) 的参数必须与例程的要求完全匹配。  调用约定处理参数的数量、类型和顺序。  调用 DLL 例程时，所传递的参数类型或个数可能不正确。  
  
### 更正此错误  
  
1.  确保所有的参数类型与所调用的例程的声明中指定的类型一致。  
  
2.  确保参数个数与所调用的例程的声明中指定的个数一致。  
  
3.  如果 DLL 例程需要按值提供参数，请确保在例程声明中为这些参数指定了 `ByVal`。  
  
## 请参阅  
 [错误类型](../../../visual-basic/programming-guide/language-features/error-types.md)   
 [Call 语句](../../../visual-basic/language-reference/statements/call-statement.md)   
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)