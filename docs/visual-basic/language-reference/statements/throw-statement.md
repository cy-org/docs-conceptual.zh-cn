---
title: "Throw 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Throw"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "异常处理, throw 语句"
  - "异常处理, 无结构的"
  - "On Error 语句, 引发异常"
  - "结构化异常处理, throw 语句"
  - "throw 语句"
  - "throw 语句, 关于 throw 语句"
  - "引发异常"
  - "引发异常, throw 语句"
  - "try-catch 异常处理, throw 语句"
ms.assetid: a6e07406-5c8a-4498-87a2-8339f3651d62
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Throw 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

在过程中引发异常。  
  
## 语法  
  
```  
Throw [ expression ]  
```  
  
## 组成部分  
 `expression`  
 提供有关将引发的异常的信息。  当位于 `Catch` 语句中时为可选项，否则为必选项。  
  
## 备注  
 `Throw` 语句引发一个异常，您可以利用结构化的异常处理代码 \(`Try`...`Catch`...`Finally`\) 或非结构化的异常处理代码 \(`On Error GoTo`\) 来处理此异常。  可以在代码中使用 `Throw` 语句来捕获错误，因为 Visual Basic 将在调用堆栈中上移直到找到对应的异常处理代码。  
  
 无表达式的 `Throw` 语句只能用在 `Catch` 语句中。在此情况下，该语句会再次引发当前正由 `Catch` 语句处理的异常。  
  
 `Throw` 语句重置 `expression` 异常的调用堆栈。  如果不提供 `expression`，则不更改调用堆栈。  您可以通过 <xref:System.Exception.StackTrace%2A> 属性来访问该异常的调用堆栈。  
  
## 示例  
 以下代码使用 `Throw` 语句来引发异常：  
  
 [!code-vb[VbVbalrStatements#84](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/throw-statement_1.vb)]  
  
## 要求  
 **命名空间：** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **模块：** `Interaction`  
  
 **程序集：**Visual Basic 运行库（位于 Microsoft.VisualBasic.dll 中）  
  
## 请参阅  
 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [On Error 语句](../../../visual-basic/language-reference/statements/on-error-statement.md)