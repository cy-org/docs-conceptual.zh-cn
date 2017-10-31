---
title: "如何：控制变量的范围 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "已声明的元素, 范围"
  - "已声明的元素, 可见性"
  - "范围, 已声明的元素"
  - "范围, 变量"
  - "范围, Visual Basic"
  - "变量 [Visual Basic], 范围"
  - "变量 [Visual Basic], 可见性"
  - "可见性, 已声明的元素"
  - "可见性, 变量"
ms.assetid: 44b7f62a-cb5c-4d50-bce9-60ae68f87072
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# 如何：控制变量的范围 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

通常，在声明变量的整个区域内，变量都在*“范围”*内，或对于引用是可见的。  在某些情况下，变量的*“访问级别”*可影响其范围。  
  
 有关更多信息，请参见 [Visual Basic 中的范围](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)。  
  
## 块级别或过程级别的范围  
  
#### 使变量仅在块内可见  
  
-   将变量的 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md) 放置在块的起始和终止声明语句之间，例如在 `For` 循环的 `For` 和 `Next` 语句之间。  
  
     该变量只能在块内引用。  
  
#### 使变量仅在过程内可见  
  
-   将变量的 `Dim` 语句放置在过程内部，所有块（如 `With`...`End With` 块）的外部。  
  
     该变量只能在该过程（包括过程内包含的所有块）内引用。  
  
## 模块级别或命名空间级别上的范围  
 为方便起见，单个术语*“模块级别”*同等地应用于模块、类和结构。  模块级别变量的访问级别确定其范围。  包含模块、类或结构的命名空间也会影响范围。  
  
#### 使变量在整个模块、类或结构内可见  
  
1.  将变量的 `Dim` 语句放置在模块、类或结构的内部，所有过程的外部。  
  
2.  将 [Private](../../../../visual-basic/language-reference/modifiers/private.md) 关键字包含在 `Dim` 语句中。  
  
3.  从模块、类或结构内部的任何位置都可以引用该变量，但是不能从外部引用。  
  
#### 使变量在整个命名空间内可见  
  
1.  将变量的 `Dim` 语句放置在模块、类或结构的内部，所有过程的外部。  
  
2.  将 [Friend](../../../../visual-basic/language-reference/modifiers/friend.md) 或 [Public](../../../../visual-basic/language-reference/modifiers/public.md) 关键字包含在 `Dim` 语句中。  
  
3.  从包含该模块、类或结构的命名空间中的任何位置都可以引用该变量。  
  
## 示例  
 下面的示例在模块级别声明一个变量，并限制其可见性，只有模块中的代码才能访问。  
  
```  
Module demonstrateScope  
    Private strMsg As String  
    Sub initializePrivateVariable()  
        strMsg = "This variable cannot be used outside this module."  
    End Sub  
    Sub usePrivateVariable()  
        MsgBox(strMsg)  
    End Sub  
End Module  
```  
  
 在前面的示例中，在模块 `demonstrateScope` 中定义的所有过程都可以引用 `String` 变量 `strMsg`。  调用 `usePrivateVariable` 过程时，在对话框中显示字符串变量 `strMsg` 的内容。  
  
 对上述示例进行如下更改后，字符串变量 `strMsg` 可由它的声明命名空间内任意位置的代码引用。  
  
```  
Public strMsg As String  
```  
  
## 可靠编程  
 变量的范围越窄，引用另一个同名变量时不小心引用到该变量的机会就越少。  也可以将引用匹配的问题减至最少。  
  
## .NET Framework 安全性  
 变量的范围越窄，恶意代码非正当使用该变量的机会就越少。  
  
## 请参阅  
 [Visual Basic 中的范围](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)   
 [Visual Basic 中的生存期](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)   
 [Visual Basic 中的访问级别](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [变量](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md)