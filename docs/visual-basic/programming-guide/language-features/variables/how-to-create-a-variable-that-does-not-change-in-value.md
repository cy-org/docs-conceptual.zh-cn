---
title: "如何：创建固定值变量 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "变量 [Visual Basic], 常量值"
  - "变量 [Visual Basic], 只读"
ms.assetid: 86b59266-25df-4635-ae15-9b59c411d036
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# 如何：创建固定值变量 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

固定值变量的概念看起来有点矛盾。  但在某些情况下，常数不够灵活，需要使用一个具有固定值的变量。  此时，可以使用 [ReadOnly](../../../../visual-basic/language-reference/modifiers/readonly.md) 关键字来定义一个成员变量。  
  
 在以下情况下，不能使用 [Const 语句](../../../../visual-basic/language-reference/statements/const-statement.md) 声明和分配常数值：  
  
-   `Const` 语句不接受要使用的数据类型  
  
-   在编译时不知道值  
  
-   不能在编译时计算常数值  
  
### 创建固定值变量  
  
1.  在模块级别，使用 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md) 声明一个成员变量，并包含 [ReadOnly](../../../../visual-basic/language-reference/modifiers/readonly.md) 关键字。  
  
    ```  
  
    Dim ReadOnly timeStarted  
    ```  
  
     只能对成员变量指定 `ReadOnly`。  这意味着必须在模块级别、所有过程之外定义该变量。  
  
2.  如果可以在编译时计算单条语句的值，则在 `Dim` 语句中使用初始化子句。  [As](../../../../visual-basic/language-reference/statements/as-clause.md) 子句后接等号 \(`=`\)，后面为表达式。  确保编译器将此表达式计算为一个常数值。  
  
    ```  
    Dim ReadOnly timeStarted As Date = Now  
    ```  
  
     只能对 `ReadOnly` 变量赋一次值。  一旦赋值，任何代码都不能更改其值。  
  
     如果在编译时不知道值或不能在编译时用单条语句计算值，还可以在运行时在构造函数中为它赋值。  为此，必须在类或结构级别声明 `ReadOnly` 变量。  在类或结构的构造函数中，计算变量的固定值，并在从构造函数返回之前将它赋给变量。  
  
## 请参阅  
 [WriteOnly](../../../../visual-basic/language-reference/modifiers/writeonly.md)   
 [Const 语句](../../../../visual-basic/language-reference/statements/const-statement.md)