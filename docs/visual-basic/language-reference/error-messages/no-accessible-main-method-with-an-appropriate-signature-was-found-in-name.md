---
title: "在“&lt;名称&gt;”中找不到任何具有合适签名的可访问“Main”方法 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30737"
  - "vbc30737"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30737"
ms.assetid: 3f40bacd-3fac-4741-b204-852f693d4340
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 在“&lt;名称&gt;”中找不到任何具有合适签名的可访问“Main”方法
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

命令行应用程序必须定义 `Sub Main`。  如果 `Main` 是在类中定义的，则它必须声明为 `Public Shared`，或者它是在模块中定义的，则必须声明为 `Public`。  
  
 有关 `Main` 的更多信息，请参见 [“Hello, World”的 Visual Basic 版本](http://msdn.microsoft.com/zh-cn/9d030b60-e148-4366-a462-69532f02294c)。  
  
 **错误 ID：**BC30737  
  
### 更正此错误  
  
-   为项目定义 `Public Sub Main` 过程。  当且仅当在类中定义此过程时，才将其声明为 `Shared`。  
  
## 请参阅  
 [“Hello, World”的 Visual Basic 版本](http://msdn.microsoft.com/zh-cn/9d030b60-e148-4366-a462-69532f02294c)   
 [Visual Basic 程序的结构](../../../visual-basic/programming-guide/program-structure/structure-of-a-visual-basic-program.md)   
 [过程](../../../visual-basic/programming-guide/language-features/procedures/index.md)