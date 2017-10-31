---
title: "Exit 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Exit"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "代码, 退出"
  - "执行, 结束"
  - "执行, stopping"
  - "Exit 语句"
  - "文件, 关闭"
  - "程序终止"
  - "程序, 退出"
ms.assetid: 760bfb32-5c3f-4bdb-a432-9a6001c92db7
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# Exit 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

退出过程或块，并且立即将控制传送到过程调用或块定义后面的语句。  
  
## 语法  
  
```  
Exit { Do | For | Function | Property | Select | Sub | Try | While }  
```  
  
## 语句  
 `Exit Do`  
 立即退出所在的 `Do` 循环。  将继续执行 `Loop` 语句之后的语句。  只能在 `Do` 循环内使用 `Exit Do`。  当在嵌套的 `Do` 循环内使用时，`Exit Do` 将退出最内层的循环，并将控制权交给下一个较高级别的嵌套。  
  
 `Exit For`  
 立即退出所在的 `For` 循环。  将继续执行 `Next` 语句之后的语句。  只能在 `For`...`Next` 或 `For Each`...`Next` 循环内使用 `Exit For`。  当在嵌套的 `For` 循环内使用时，`Exit For` 将退出最内层的循环，并将控制权交给下一个较高级别的嵌套。  
  
 `Exit Function`  
 立即退出所在的 `Function` 过程。  将继续执行调用 `Function` 过程的语句之后的语句。  只能在 `Function` 过程内使用 `Exit Function`。  
  
 要指定一个返回值，可以在 `Exit Function` 语句的前一行将该值赋给函数名。  要在某一语句中赋予返回值并退出函数，可以转而使用[Return 语句](../../../visual-basic/language-reference/statements/return-statement.md)。  
  
 `Exit Property`  
 立即退出所在的 `Property` 过程。  将继续执行调用 `Property` 过程的语句，即，继续执行请求或设置属性值的语句。  只能在属性的 `Get` 或 `Set` 过程内使用 `Exit Property`。  
  
 要在 `Get` 过程中指定一个返回值，可以在 `Exit Property` 语句的前一行将该值赋给函数名。  要在某一语句中赋予返回值并退出 `Get` 程序，可以转而使用 `Return` 语句。  
  
 在 `Set` 过程中，`Exit Property` 语句等效于 `Return` 语句。  
  
 `Exit Select`  
 立即退出所在的 `Select Case` 块。  将继续执行 `End Select` 语句之后的语句。  只能在 `Select Case` 语句内使用 `Exit Select`。  
  
 `Exit Sub`  
 立即退出所在的 `Sub` 过程。  将继续执行调用 `Sub` 过程的语句之后的语句。  只能在 `Sub` 过程内使用 `Exit Sub`。  
  
 在 `Sub` 过程中，`Exit Sub` 语句等效于 `Return` 语句。  
  
 `Exit Try`  
 立即退出所在的 `Try` 或 `Catch` 块。  如果存在 `Finally` 块，则将继续执行该块；否则，将继续执行 `End Try` 语句之后的语句。  只能在 `Try` 或 `Catch` 块内使用 `Exit Try`，不能在 `Finally` 块内使用它。  
  
 `Exit While`  
 立即退出所在的 `While` 循环。  将继续执行 `End While` 语句之后的语句。  只能在 `While` 循环内使用 `Exit While`。  当在嵌套的 `While` 循环内使用时，`Exit While` 会将控制权交给嵌套在 `Exit While` 所在循环的上一个级别的循环。  
  
## 备注  
 不要将 `Exit` 语句和 `End` 语句混淆。  `Exit` 不定义语句的结尾。  
  
## 示例  
 在下面的示例中，当 `index` 变量大于 100 时，循环条件将停止循环。  但是，循环中的 `If` 语句在索引变量大于 10 时将导致 `Exit Do` 语句停止循环。  
  
 [!code-vb[VbVbalrStatements#133](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/exit-statement_1.vb)]  
  
## 示例  
 下面的示例将返回值赋给函数名 `myFunction`，然后使用 `Exit Function` 从该函数返回。  
  
 [!code-vb[VbVbalrStatements#23](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/exit-statement_2.vb)]  
  
## 示例  
 以下示例用 [Return 语句](../../../visual-basic/language-reference/statements/return-statement.md) 分配返回值，并退出函数。  
  
 [!code-vb[VbVbalrStatements#24](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/exit-statement_3.vb)]  
  
## 请参阅  
 [Continue 语句](../../../visual-basic/language-reference/statements/continue-statement.md)   
 [Do...Loop 语句](../../../visual-basic/language-reference/statements/do-loop-statement.md)   
 [End 语句](../../../visual-basic/language-reference/statements/end-statement.md)   
 [For Each...Next 语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [For...Next 语句](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Return 语句](../../../visual-basic/language-reference/statements/return-statement.md)   
 [Stop 语句](../../../visual-basic/language-reference/statements/stop-statement.md)   
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Try...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)