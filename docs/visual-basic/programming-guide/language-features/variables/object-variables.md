---
title: "Visual Basic 中的对象变量 | Microsoft Docs"
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
  - "对象变量"
  - "对象变量, 关于对象变量"
  - "对象 [Visual Basic], 访问"
  - "变量 [Visual Basic], 对象"
ms.assetid: 6169a196-2b13-4ba5-a205-154bc1b87844
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# Visual Basic 中的对象变量
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

除了直接存储值，变量还可以引用对象。  将对象分配给变量的理由与给变量赋值一样：  
  
-   变量名通常要比访问对象本身所需的方法和属性的完整路径短和容易记忆。  
  
-   与通过所需的方法或属性来重复访问对象本身相比，使用引用对象的变量更有效。  
  
-   在代码运行期间，可以更改变量以引用其他对象。  
  
## 让代码更短小  
 使用对象变量可以缩短必须键入的代码。  下面的示例使用方法和属性的完整路径来访问一个 <xref:System.Windows.Forms.Control> 对象。  
  
```  
' Assume Me is a valid Form, or replace Me with a valid Form.  
Me.ActiveForm.ActiveControl.Text = "Test"  
Me.ActiveForm.ActiveControl.Location = New Point(100, 100)  
Me.ActiveForm.ActiveControl.Show()  
```  
  
 如果将控件替换成对象变量，可以缩短此代码并加快执行速度。  应使用将要分配给对象变量的特定类（本例中为 `Control`）来声明对象变量。  将对象分配给变量后，可以像处理该变量引用的对象那样处理该变量。  可以设置或检索对象的属性或使用它的任何方法。  下面的示例使用一个对象变量来简化前一个示例的代码。  
  
```  
Dim ctrlActv As System.Windows.Forms.Control = Me.ActiveForm.ActiveControl  
ctrlActv.Text = "Test"  
ctrlActv.Location = New Point(100, 100)  
ctrlActv.Show()  
```  
  
## 请参阅  
 [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [如何：加速访问具有长限定路径的对象
](../../../../visual-basic/programming-guide/language-features/variables/how-to-speed-up-access-to-an-object-with-a-long-qualification-path.md)   
 [对象变量声明](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [对象变量赋值](../../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)   
 [对象变量值](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)