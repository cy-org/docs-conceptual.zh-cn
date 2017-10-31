---
title: "REM 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.'"
  - "vb.Rem"
  - "Rem"
  - "'"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "' 注释标记字符 [Visual Basic]"
  - "代码注释, Visual Basic"
  - "注释, Visual Basic 代码"
  - "REM 语句"
  - "Visual Basic 代码, 注释"
ms.assetid: 34126d7f-e0f9-476d-91e6-b31b398615dc
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# REM 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

用于将解释性备注包括在程序的源代码中。  
  
## 语法  
  
```  
REM comment  
' comment  
```  
  
## 部件  
 `comment`  
 可选。  希望包含的任何注释文本。  所需之间的空间`REM`关键字和`comment`。  
  
## 备注  
 可以将 `REM` 语句单独放在一行，也可以将之放在另一语句后的行上。  `REM` 语句必须是该行上最后的语句。  如果它跟在另一语句后面，则 `REM` 与该语句间必须有一个空格。  
  
 可以使用单引号 \(`'`\) 替代 `REM`。  无论注释是跟在同一行上的另一语句后面还是单独在一行，都可以这样做。  
  
> [!NOTE]
>  不能使用行继续符序列 \(`_`\) 来延续 `REM` 语句。  注释开始后，编译器将不检查字符是否具有特殊含义。  对于多行注释，请在每行上使用另一个 `REM` 语句或者使用一个注释符号 \(`'`\)。  
  
## 示例  
 下面的示例阐释 `REM` 语句，该语句用于包含程序中的解释性备注。  它还演示了另一种方案，即使用单引号字符 \(`'`\) 替代 `REM`。  
  
 [!code-vb[VbVbalrStatements#6](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/rem-statement_1.vb)]  
  
## 请参阅  
 [代码中的注释](../../../visual-basic/programming-guide/program-structure/comments-in-code.md)   
 [如何：在代码中拆分和合并语句](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)