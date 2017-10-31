---
title: "如何：隐藏继承的变量 (Visual Basic) | Microsoft Docs"
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
  - "声明语句, 已声明的元素"
  - "已声明的元素, 关于声明的元素"
  - "已声明的元素, 引用"
  - "元素名称, 限定"
  - "限定, 元素名称"
  - "引用, 已声明的元素"
  - "引用已声明的元素"
  - "变量 [Visual Basic], 隐藏继承的"
ms.assetid: 765728d9-7351-4a30-999d-b5f34f024412
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# 如何：隐藏继承的变量 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

派生类继承其基类的所有定义。  如果要定义与某一基类元素同名的变量，则可以在定义派生类变量时*“隐藏”*该基类元素。  如果这样做，则除非派生类的代码显式跳过隐藏机制，否则它就会访问您定义的变量。  
  
 隐藏被继承变量的另一个原因是为了防止基类修订。  基类的更改可能会改变要继承的元素。  如果发生这种情况，则 `Shadows` 修饰符会将来自派生类的引用强制解析为您定义的变量，而不是基类元素。  
  
### 隐藏被继承变量  
  
1.  确保要隐藏的变量是在类级别（任何过程之外）声明的。  否则不需要将其隐藏。  
  
2.  在派生类中，编写 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md) 声明您的变量。  使用与被继承变量相同的名称。  
  
3.  将 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md) 关键字包含在声明中。  
  
     当派生类中的代码引用变量名时，编译器会将该引用解析为您的变量。  
  
     下面的示例演示如何隐藏被继承变量。  
  
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
  
     上一个示例在基类中声明变量 `shadowString`，而在派生类中隐藏该变量。  当名称 `shadowString` 没有限定时，派生类中的过程 `showStrings` 显示字符串的隐藏版本。  当 `shadowString` 由 `MyBase` 关键字限定时，则显示被隐藏的版本。  
  
## 可靠编程  
 隐藏使用同一名称引入了变量的多个版本。  如果代码语句引用该变量名，则编译器将引用解析到的版本取决于代码语句的位置以及是否存在限定字符串等因素。  这可能会增加引用被隐藏变量的非预期版本的危险。  可以通过完全限定对被隐藏变量的所有引用来降低这种风险。  
  
## 请参阅  
 [对已声明元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Visual Basic 中的隐藏](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)   
 [隐藏和重写之间的差异](../../../../visual-basic/programming-guide/language-features/declared-elements/differences-between-shadowing-and-overriding.md)   
 [如何：隐藏与您的变量同名的变量](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-a-variable-with-the-same-name-as-your-variable.md)   
 [如何：访问被派生类隐藏的变量](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-access-a-variable-hidden-by-a-derived-class.md)   
 [Overrides](../../../../visual-basic/language-reference/modifiers/overrides.md)   
 [Me、My、MyBase 和 MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)   
 [继承的基础知识](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)