---
title: "对象变量赋值 (Visual Basic) | Microsoft Docs"
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
  - "赋值语句, 对象变量赋值"
  - "当前实例, 已定义"
  - "Me 关键字, 作为对象变量"
  - "Nothing 关键字, 对象变量赋值"
  - "对象变量, 分配"
  - "对象变量, 初始化"
  - "对象 [Visual Basic], 当前实例"
  - "变量 [Visual Basic], 分配"
  - "变量 [Visual Basic], 初始化"
  - "变量 [Visual Basic], 对象变量"
ms.assetid: 3706811d-fd40-44fe-8727-d692e8e55d6d
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 对象变量赋值 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

使用标准赋值语句将对象分配给对象变量。  您可以分配对象表达式或 [Nothing](../../../../visual-basic/language-reference/nothing.md) 关键字，如下例所示。  
  
```  
Dim thisObject As Object  
' The following statement assigns an object reference.  
thisObject = Form1  
' The following statement discontinues association with any object.  
thisObject = Nothing  
```  
  
 `Nothing` 表示当前没有对象分配给变量。  
  
## 初始化  
 当您的代码开始运行时，会将您的对象变量初始化为 `Nothing`。  其声明包含初始化的对象变量会被重新初始化为您在执行声明语句时指定的值。  
  
 您可以通过使用 [New](../../../../visual-basic/language-reference/operators/new-operator.md) 关键字在声明中包括初始化。  下面的声明语句声明对象变量 `testUri` 和 `ver` 并将特定的对象分配给它们。  每个声明语句使用适当类的其中一个重载构造函数来初始化对象。  
  
```  
Dim testUri As New System.Uri("http://www.microsoft.com")  
Dim ver As New System.Version(6, 1, 0)  
```  
  
## 取消关联  
 将对象变量设置为 `Nothing` 会中断变量同任何特定对象的关联。  这样可防止您因意外更改变量而更改对象。  还使您可以测试对象变量是否指向有效对象，如下例所示。  
  
```  
If otherObject IsNot Nothing Then  
    ' otherObject refers to a valid object, so your code can use it.  
End If  
```  
  
 如果变量引用的对象在另一个应用程序中，此测试无法确定该应用程序是已经终止对象还是只是使对象无效。  
  
 值为 `Nothing` 的对象变量也称为“空引用”。  
  
## 当前实例  
 对象的“当前实例”是代码当前正在其中执行的实例。  由于所有的代码都在过程的内部执行，因此当前实例是调用过程的实例。  
  
 `Me` 关键字作为引用当前实例的对象变量。  如果过程不是 [Shared](../../../../visual-basic/language-reference/modifiers/shared.md)，它可以使用 `Me` 关键字获得指向当前实例的指针。  共享过程不能同特定类实例关联。  
  
 将当前实例传递到另一模块中的过程时，使用 `Me` 尤其有用。  例如，假设您具有许多 XML 文档并且想要在所有这些文档中添加一些标准文本。  下面的示例定义用于实现此目的的过程。  
  
```  
Sub addStandardText(XmlDoc As System.Xml.XmlDocument)  
    XmlDoc.CreateTextNode("This text goes into every XML document.")  
End Sub  
```  
  
 然后，每个 XML 文档对象可以调用该过程并将它的当前实例作为参数传递。  下面的示例说明了这一点。  
  
```  
addStandardText(Me)  
```  
  
## 请参阅  
 [对象变量](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [对象变量声明](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [对象变量值](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)   
 [如何：在 Visual Basic 中声明对象变量并为它分配对象](../../../../visual-basic/programming-guide/language-features/variables/how-to-declare-an-object-variable-and-assign-an-object-to-it.md)   
 [如何：使对象变量不引用任何实例](../../../../visual-basic/programming-guide/language-features/variables/how-to-make-an-object-variable-not-refer-to-any-instance.md)   
 [Me、My、MyBase 和 MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)