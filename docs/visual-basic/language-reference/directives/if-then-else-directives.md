---
title: "#If...Then...#Else 指令 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.#EndIf"
  - "#End If"
  - "#Then"
  - "#ElseIf"
  - "vb.#ElseIf"
  - "vb.#Else"
  - "vb.#If"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "#Else 指令 [Visual Basic]"
  - "#End if 指令 [Visual Basic]"
  - "#If 指令 [Visual Basic]"
  - "条件编译, 指令"
  - "else 指令 (#else)"
  - "有选择的编译"
  - "Visual Basic 代码, 编译"
ms.assetid: 10bba104-e3fd-451b-b672-faa472530502
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# #If...Then...#Else 指令
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

根据条件编译选定的 Visual Basic 代码块。  
  
## 语法  
  
```  
#If expression Then  
   statements  
[ #ElseIf expression Then  
   [ statements ]  
...  
#ElseIf expression Then  
   [ statements ] ]  
[ #Else  
   [ statements ] ]  
#End If  
```  
  
## 部件  
 `expression`  
 对于 `#If` 和 `#ElseIf` 语句是必选的，在其他地方则是可选的。  计算结果为 `True` 或 `False` 的任意表达式，仅由一个或多个条件编译器常数、文本和运算符组成。  
  
 `statements`  
 对于 `#If` 语句块是必选的，在其他地方则是可选的。  如果所关联的表达式结果为 `True`，将对 Visual Basic 程序行或编译器指令进行编译。  
  
 `#End If`  
 终止 `#If` 语句块。  
  
## 备注  
 表面上，`#If...Then...#Else` 指令的行为与 `If...Then...Else` 语句的行为相同。  但是，`#If...Then...#Else` 指令计算编译器要编译的内容，而 `If...Then...Else` 语句则计算运行时的条件。  
  
 条件编译通常用来编译不同平台上的同一个程序。  也可以用来避免调试代码出现在可执行文件中。  条件编译时被排除的代码在最终的可执行文件中被完全忽略，所以不会对大小或性能有任何影响。  
  
 不管计算的结果如何，所有的表达式都使用 `Option Compare Binary` 来计算。  `Option Compare` 语句不影响 `#If` 及 `#ElseIf` 语句中的表达式。  
  
> [!NOTE]
>  不存在 `#If`、`#Else`、`#ElseIf` 和 `#End If` 指令的单行形式。  任何指令所在的同一行中不会出现其他代码。  
  
## 示例  
 本示例使用 `#If...Then...#Else` 构造来判断是否编译某些语句。  
  
 [!code-vb[VbVbalrConditionalComp#1](../../../visual-basic/language-reference/directives/codesnippet/VisualBasic/if-then-else-directives_1.vb)]  
  
## 请参阅  
 [\#Const 指令](../../../visual-basic/language-reference/directives/const-directive.md)   
 [If...Then...Else 语句](../../../visual-basic/language-reference/statements/if-then-else-statement.md)   
 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)