---
title: "#Const 指令 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.#Const"
  - "#vb.Const"
  - "#Const"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "#Const 指令"
  - "条件编译, 指令"
  - "Const 指令 (#Const)"
  - "Const 语句 [Visual Basic], 指令 (#Const)"
  - "常量, 常量指令"
  - "常量, 声明"
  - "声明常量, #const 指令"
  - "Visual Basic 编译器, 编译器指令"
ms.assetid: 707669e5-23f9-4f17-8622-a0d534429386
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# #Const 指令
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

为 Visual Basic 定义条件编译器常数。  
  
## 语法  
  
```  
#Const constname = expression  
```  
  
## 部件  
 `constname`  
 必选。  要定义的常量的名称。  
  
 `expression`  
 必选。  文本、其他条件编译器常数或包含除 `Is` 外的任何或所有算术或逻辑运算符的任意组合。  
  
## 备注  
 条件编译器常数在其出现的文件中总是为 private。  不能使用 `#Const` 指令创建 Public 编译器常数，只能在用户界面中或使用 `/define` 编译器选项创建它们。  
  
 在 `expression` 中只能使用条件编译器常数和文本。  使用用 `Const` 定义的标准常数将导致错误。  相反，只能将使用 `#Const` 关键字定义的常数用于条件编译。  常数也可以是未定义的，这种情况下常数的值为 `Nothing`。  
  
## 示例  
 本示例使用 `#Const` 指令。  
  
 [!code-vb[VbVbalrConditionalComp#3](../../../visual-basic/language-reference/directives/codesnippet/VisualBasic/const-directive_1.vb)]  
  
## 请参阅  
 [\/define](../../../visual-basic/reference/command-line-compiler/define.md)   
 [\#If...Then...\#Else 指令](../../../visual-basic/language-reference/directives/if-then-else-directives.md)   
 [Const 语句](../../../visual-basic/language-reference/statements/const-statement.md)   
 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)   
 [If...Then...Else 语句](../../../visual-basic/language-reference/statements/if-then-else-statement.md)