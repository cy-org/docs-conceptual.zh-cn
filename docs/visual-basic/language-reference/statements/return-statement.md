---
title: "Return 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Return"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "控制流, 将控件返回到表达式"
  - "表达式 [Visual Basic], 将控件返回到"
  - "Return 语句"
  - "Return 语句, 语法"
ms.assetid: ac86e7f0-5a67-42c3-9834-0e0381efa3ec
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Return 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

将控制返回给调用 `Function`、`Sub`、`Get`、`Set` 或 `Operator` 过程的代码。  
  
## 语法  
  
```  
Return  
-or-  
Return expression  
```  
  
## 组成部分  
 `expression`  
 在 `Function`、`Get` 或 `Operator` 过程中为必选项。  表达式，表示要返回给调用代码的值。  
  
## 备注  
 在 `Sub` 或 `Set` 过程中，`Return` 语句等效于 `Exit Sub` 或 `Exit Property` 语句，并且不得提供 `expression`。  
  
 在 `Function`、`Get` 或 `Operator` 过程中，`Return` 语句必须包括 `expression`，并且 `expression` 的计算结果必须是可转换为过程返回类型的数据类型。  在 `Function` 或 `Get` 过程中，您还可以使用另一种方法：将表达式赋给过程名称以充当返回值，然后执行 `Exit Function` 或 `Exit Property` 语句。  在 `Operator` 过程中，必须使用 `Return` `expression`。  
  
 可以根据需要在同一过程中包括任意多个 `Return` 语句。  
  
> [!NOTE]
>  `Finally` 块中的代码运行的条件是：在 `Try` 或 `Catch` 块中遇到了 `Return` 语句之后，但在该 `Return` 语句尚未执行之前。  `Return` 语句在 `Finally` 不能包含块。  
  
## 示例  
 下面的示例多次使用 `Return` 语句，以在过程无需执行任何其他操作时返回到调用代码。  
  
 [!code-vb[VbVbalrStatements#53](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/return-statement_1.vb)]  
  
## 请参阅  
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Get 语句](../../../visual-basic/language-reference/statements/get-statement.md)   
 [Set 语句](../../../visual-basic/language-reference/statements/set-statement.md)   
 [Operator 语句](../../../visual-basic/language-reference/statements/operator-statement.md)   
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Exit 语句](../../../visual-basic/language-reference/statements/exit-statement.md)   
 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)