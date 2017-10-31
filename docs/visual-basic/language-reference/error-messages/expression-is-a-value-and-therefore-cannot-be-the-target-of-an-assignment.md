---
title: "表达式是一个值，因此不能作为赋值目标 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30068"
  - "vbc30068"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30068"
ms.assetid: d65141e1-f31e-4ac5-a3b8-0b2e02a71ebf
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# 表达式是一个值，因此不能作为赋值目标
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

某个语句尝试为表达式赋值。  在运行时只能对可写的变量、属性或数组元素赋值。  下面的示例阐释此错误是如何发生的。  
  
```  
Dim yesterday As Integer  
ReadOnly maximum As Integer = 45  
yesterday + 1 = DatePart(DateInterval.Day, Now)  
' The preceding line is an ERROR because of an expression on the left.  
maximum = 50  
' The preceding line is an ERROR because maximum is declared ReadOnly.  
```  
  
 类似示例可能适用于属性和数组元素。  
  
 **间接访问。**通过值类型的间接访问也可能会生成此错误。  请考虑下面的代码示例，这段代码尝试通过 <xref:System.Windows.Forms.Control.Location%2A> 间接访问 <xref:System.Drawing.Point> 来设置它的值。  
  
```  
' Assume this code runs inside Form1.  
Dim exitButton As New System.Windows.Forms.Button()  
exitButton.Text = "Exit this form"  
exitButton.Location.X = 140  
' The preceding line is an ERROR because of no storage for Location.  
```  
  
 以上示例的最后一条语句失败，因为它仅为 <xref:System.Windows.Forms.Control.Location%2A> 属性返回的 <xref:System.Drawing.Point> 结构提供了临时的分配。  这是一个值类型的结构，该语句运行后不保留临时结构。  解决该问题的方法是：声明并使用 <xref:System.Windows.Forms.Control.Location%2A> 的变量，从而为 <xref:System.Drawing.Point> 结构创建更为永久的分配。  下面的示例演示的代码可用于替换以上示例的最后一条语句。  
  
```  
Dim exitLocation as New System.Drawing.Point(140, exitButton.Location.Y)  
exitButton.Location = exitLocation  
```  
  
 **错误 ID：**BC30068  
  
### 更正此错误  
  
-   如果相应语句为某个表达式赋值，请用一个可写的变量、属性或数组元素替换该表达式。  
  
-   如果相应语句通过值类型（通常为结构）进行间接访问，请创建一个变量来保存值类型。  
  
-   将相应的结构（或其他值类型）赋给变量。  
  
-   使用变量来访问属性，以便为该变量赋值。  
  
## 请参阅  
 [运算符和表达式](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [语句](../../../visual-basic/programming-guide/language-features/statements.md)   
 [过程疑难解答](../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)