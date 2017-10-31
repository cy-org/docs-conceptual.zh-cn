---
title: "Call 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Call"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Call 语句"
  - "过程, Call 语句"
  - "过程, 调用"
ms.assetid: e5b31571-6867-406f-b8e7-a3f9aae4723a
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# Call 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

将控制传送到 `Function`、`Sub` 或动态链接库 \(DLL\) 过程。  
  
## 语法  
  
```  
[ Call ] procedureName [ (argumentList) ]  
```  
  
## 部件  
 `procedureName`  
 必选。  要调用的过程名。  
  
 `argumentList`  
 可选。  变量和表达式列表，表示当调用过程时传递给该过程的参数。  多个参数以逗号分隔。  如果包括 `argumentList`，则必须将它放在括号内。  
  
## 备注  
 ，在调用过程时，可以使用 `Call` 关键字。  对于大多数过程调用，则不需要使用此关键字。  
  
 ，在调用的表达式不从标识符时，开始通常使用 `Call` 关键字。  对于其他使用建议不要对 `Call` 关键字的用法。  
  
 如果该过程返回值，`Call` 语句将放弃该值。  
  
## 示例  
 以下代码显示了两个示例 `Call` 关键字的位置需要调用过程。  在两个示例中，被调用的表达式不从标识符开头。  
  
 [!code-vb[VbVbalrStatements#97](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/call-statement_1.vb)]  
  
## 请参阅  
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [lambda 表达式](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)