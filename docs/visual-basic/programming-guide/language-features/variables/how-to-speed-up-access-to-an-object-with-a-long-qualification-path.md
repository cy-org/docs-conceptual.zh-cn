---
title: "如何：加速访问具有长限定路径的对象 (Visual Basic) | Microsoft Docs"
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
  - "对象变量, 访问"
  - "变量 [Visual Basic], 访问"
  - "变量 [Visual Basic], 对象"
  - "With 块"
  - "With 语句"
ms.assetid: 3eb7657f-c9fe-4e05-8bc3-4bb14d5ae585
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 如何：加速访问具有长限定路径的对象 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

如果经常访问某个对象，并且该对象需要一个包含多个方法和属性的限定路径，则可以不必重复该限定路径，从而加快代码运行。  
  
 有两种方法可避免重复限定路径。  可以将该对象分配给一个变量，也可以在 `With`...`End With` 块中使用该对象。  
  
### 将超长限定对象分配给变量以加速访问该对象  
  
1.  声明一个变量，类型为要经常访问的对象的类型。  在声明的初始化部分指定限定路径。  
  
    ```  
    Dim ctrlActv As Control = someForm.ActiveForm.ActiveControl  
    ```  
  
2.  使用该变量访问对象的成员。  
  
    ```  
    ctrlActv.Text = "Test"  
    ctrlActv.Location = New Point(100, 100)  
    ctrlActv.Show()  
    ```  
  
### 使用 With...End With 块加速访问超长限定对象  
  
1.  将限定路径放在 `With` 语句内。  
  
    ```  
    With someForm.ActiveForm.ActiveControl  
    ```  
  
2.  在 `End With` 语句之前，在 `With` 块内访问该对象的成员。  
  
    ```  
        .Text = "Test"  
        .Location = New Point(100, 100)  
        .Show()  
    End With  
    ```  
  
## 请参阅  
 [对象变量](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [With...End With 语句](../../../../visual-basic/language-reference/statements/with-end-with-statement.md)