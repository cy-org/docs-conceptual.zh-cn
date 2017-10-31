---
title: "如何：访问被派生类隐藏的变量 (Visual Basic) | Microsoft Docs"
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
  - "基类, 访问元素"
  - "已声明的元素, 引用"
  - "元素名称, 限定"
  - "限定, 元素名称"
  - "引用, 已声明的元素"
  - "变量 [Visual Basic], 访问隐藏"
ms.assetid: ae21a8ac-9cd4-4fba-a3ec-ecc4321ef93c
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# 如何：访问被派生类隐藏的变量 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

如果派生类的代码访问变量，编译器通常将引用解析到最近的可访问版本，即从访问类向上，派生步骤最少的可访问版本。  如果变量是在该派生类中定义的，则代码通常访问该定义。  
  
 如果该派生类变量隐藏了基类的某个变量，则它隐藏了基类版本。  但是，通过使用 `MyBase` 关键字限定基类变量，可以访问该基类变量。  
  
### 访问被派生类隐藏的基类变量  
  
-   在表达式或赋值语句中，在变量名称前面加 `MyBase` 关键字和一个句点 \(`.`\)。  
  
     编译器将引用解析到该变量的基类版本。  
  
     下面的示例阐释了如何通过继承进行隐藏。  这里有两个引用，一个访问隐藏变量，另一个绕开隐藏。  
  
    ```  
    Public Class shadowBaseClass  
        Public shadowString As String = "This is the base class string."  
    End Class  
    Public Class shadowDerivedClass  
        Inherits shadowBaseClass  
        Public Shadows shadowString As String = "This is the derived class string."  
        Public Sub showStrings()  
            Dim s As String = "Unqualified shadowString: " & shadowString &  
                vbCrLf & "MyBase.shadowString: " & MyBase.shadowString  
            MsgBox(s)  
        End Sub  
    End Class  
    ```  
  
     上一个示例在基类中声明变量 `shadowString`，而在派生类中隐藏该变量。  当名称 `shadowString` 没有限定时，派生类中的过程 `showStrings` 显示字符串的隐藏版本。  如果 `shadowString` 由 `MyBase`  关键字限定，则显示被隐藏的版本。  
  
## 可靠编程  
 要降低引用被隐藏变量的意外版本的风险，可以完全限定对被隐藏变量的所有引用。  隐藏使用同一名称引入了变量的多个版本。  如果代码语句引用该变量名，则编译器将引用解析到的版本取决于代码语句的位置以及是否存在限定字符串等因素。  这会增加引用错误变量版本的风险。  
  
## 请参阅  
 [对已声明元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Visual Basic 中的隐藏](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)   
 [隐藏和重写之间的差异](../../../../visual-basic/programming-guide/language-features/declared-elements/differences-between-shadowing-and-overriding.md)   
 [如何：隐藏与您的变量同名的变量](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-a-variable-with-the-same-name-as-your-variable.md)   
 [如何：隐藏继承的变量](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-an-inherited-variable.md)   
 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md)   
 [Overrides](../../../../visual-basic/language-reference/modifiers/overrides.md)   
 [Me、My、MyBase 和 MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)   
 [继承的基础知识](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)