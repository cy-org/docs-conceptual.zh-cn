---
title: "Resume 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Resume"
  - "vb.ResumeNext"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Error 语句, 和 Resume 语句"
  - "错误 [Visual Basic], 继续"
  - "执行"
  - "执行, 继续"
  - "Next 语句, Resume"
  - "Resume Next 语句"
  - "Resume 语句"
  - "Resume 语句, 语法"
  - "运行时错误, 继续"
ms.assetid: e24d058b-1a5c-4274-acb9-7d295d3ea537
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Resume 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

在错误处理例程完成之后继续程序执行。  
  
 建议使用非结构化异常处理和 `On Error` 和 `Resume` 语句，您可以在代码使用结构化异常处理只要有可能，而不是。  有关更多信息，请参见 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。  
  
## 语法  
  
```  
Resume [ Next | line ]  
```  
  
## 部件  
 `Resume`  
 必选。  如果错误发生在错误处理程序所在的同一过程中，程序将由产生错误的语句处继续执行。  如果错误发生在被调用的过程中，程序将从最近过程（该过程含有错误处理例程）调用的语句处继续执行。  
  
 `Next`  
 可选。  如果错误发生在错误处理程序所在的同一过程中，程序由紧随引发错误的语句的下一条语句处继续执行。  如果错误发生在被调用的过程中，程序由紧随最近过程（该过程含有错误处理例程）调用的语句的下一条语句继续执行（或者 `On Error Resume Next` 语句）。  
  
 `line`  
 可选。  程序从必选参数 `line` 指定的代码行处继续执行。  `line` 参数是一个行标签或者行号，必须位于错误处理程序所在的同一过程中。  
  
## 备注  
  
> [!NOTE]
>  建议使用非结构化异常处理和 `On Error` 和 `Resume` 语句，您可以在代码使用结构化异常处理只要有可能，而不是。  有关更多信息，请参见 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。  
  
 如果在错误处理例程以外的任何位置使用 `Resume` 语句，将会发生错误。  
  
 `Resume` 语句不能用于包含 `Try...Catch...Finally` 语句的任何过程中。  
  
## 示例  
 此示例使用 `Resume` 语句来结束过程中的错误处理，然后继续执行导致错误的语句。  将生成错误号 55 以表明使用的是 `Resume` 语句。  
  
 [!code-vb[VbVbalrErrorHandling#16](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/resume-statement_1.vb)]  
  
## 要求  
 **命名空间：** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **程序集：**Visual Basic 运行库（位于 Microsoft.VisualBasic.dll 中）  
  
## 请参阅  
 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [Error 语句](../../../visual-basic/language-reference/statements/error-statement.md)   
 [On Error 语句](../../../visual-basic/language-reference/statements/on-error-statement.md)