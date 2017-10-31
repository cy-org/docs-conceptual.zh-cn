---
title: "如何：控制变量的可用性 (Visual Basic) | Microsoft Docs"
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
  - "访问级别, 已声明的元素"
  - "访问级别, 变量"
  - "已声明的元素, 访问级别"
  - "Friend 关键字, 访问变量"
  - "Private 关键字, 访问变量"
  - "Protected 关键字, 访问变量"
  - "Public 关键字, 访问变量"
  - "变量 [Visual Basic], 访问级别"
ms.assetid: eaf4f073-7922-43ce-ae1e-90ff376ae947
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# 如何：控制变量的可用性 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

可通过指定变量的*“访问级别”*来控制变量的可用性。  访问级别决定什么样的代码有权读或写变量。  
  
-   *“成员变量”*（在模块级别上并且在任何过程外部定义）默认为公共访问，即任何可以看见变量的代码都可以访问变量。  可通过指定访问修饰符来改变此设置。  
  
-   *“局部变量”*（在过程内部定义）名义上具有公共可访问性，但只有局部变量所在的过程内的代码可以访问局部变量。  您不能更改局部变量的访问级别，但可以更改包含局部变量的过程的访问级别。  
  
 有关更多信息，请参见 [Visual Basic 中的访问级别](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
## 专用访问和公共访问  
  
#### 使变量只能从它的模块、类或结构内被访问  
  
1.  在模块、类或结构内，但在任何过程外部放置变量的 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md)。  
  
2.  将 [Private](../../../../visual-basic/language-reference/modifiers/private.md) 关键字包含在 `Dim` 语句中。  
  
     然后就可以从模块、类或结构内的任何位置（而不能从外部）读或写该变量。  
  
#### 使变量可由任何可以看见它的代码访问  
  
1.  对于成员变量，在模块、类或结构内，但在任何过程外部放置变量的 `Dim` 语句。  
  
2.  将 [Public](../../../../visual-basic/language-reference/modifiers/public.md) 关键字包含在 `Dim` 语句中。  
  
     然后就可以从任何与您的程序集交互的代码读或写该变量。  
  
 \- 或 \-  
  
1.  对于局部变量，在过程内放置变量的 `Dim` 语句。  
  
2.  不要将 `Public` 关键字包含在 `Dim` 语句中。  
  
     然后就可以从该过程内的任何位置（而不能从该过程外）读或写该变量。  
  
## 受保护访问与友元访问  
 可以将变量的访问级别限定为该变量的类或任何派生类的级别，或者限定为该变量的程序集的级别。  也可以指定这些限制的并集，以允许从任何派生类中的代码或同一程序集中的任何其他位置的代码访问该变量。  可以通过在同一声明中组合 `Protected` 和 `Friend` 关键字来指定此并集。  
  
#### 使变量只能从它的类或任何派生类内被访问  
  
1.  在类的内部，但在任何过程外部放置变量的 `Dim` 语句。  
  
2.  将 [Protected](../../../../visual-basic/language-reference/modifiers/protected.md) 关键字包含在 `Dim` 语句中。  
  
     然后就可以从类内的任何位置以及从任何派生类的内部（而不能从派生链中的任何类的外部）读或写该变量。  
  
#### 使变量只能从同一程序集内被访问  
  
1.  在模块、类或结构的内部，但在任何过程外部放置变量的 `Dim` 语句。  
  
2.  将 [Friend](../../../../visual-basic/language-reference/modifiers/friend.md) 关键字包含在 `Dim` 语句中。  
  
     然后就可以从模块、类或结构内的任何位置，以及从同一程序集中的任何代码（而不能从程序集外部）读或写该变量。  
  
## 示例  
 下面的示例显示了具有 `Public`、`Protected`、`Friend`、`Protected Friend` 和 `Private` 访问级别的变量的声明。  注意，当 `Dim` 语句指定访问级别时，不需要包括 `Dim` 关键字。  
  
```  
Public Class classForEverybody  
Protected Class classForMyHeirs  
Friend stringForThisProject As String  
Protected Friend stringForProjectAndHeirs As String  
Private numberForMeOnly As Integer  
```  
  
## .NET Framework 安全性  
 变量的访问级别越严格，恶意代码可以不正当使用该变量的机会就越小。  
  
## 请参阅  
 [Visual Basic 中的访问级别](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md)   
 [Public](../../../../visual-basic/language-reference/modifiers/public.md)   
 [Protected](../../../../visual-basic/language-reference/modifiers/protected.md)   
 [Friend](../../../../visual-basic/language-reference/modifiers/friend.md)   
 [Private](../../../../visual-basic/language-reference/modifiers/private.md)