---
title: "如何：隐藏与您的变量同名的变量 (Visual Basic) | Microsoft Docs"
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
  - "声明, 元素"
  - "已声明的元素, 关于声明的元素"
  - "已声明的元素, 引用"
  - "声明元素"
  - "元素名称, 限定"
  - "限定, 元素名称"
  - "引用, 已声明的元素"
  - "引用已声明的元素"
ms.assetid: e39c0752-f19f-4d2e-a453-00df1b5fc7ee
caps.latest.revision: 25
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 25
---
# 如何：隐藏与您的变量同名的变量 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

可通过*“隐藏”*操作来隐藏变量，即用同名的变量重新定义要隐藏的变量。  可以用两种方式隐藏希望隐藏的变量：  
  
-   **通过范围隐藏。**可以通过范围隐藏变量，方法是：在包含您希望隐藏的变量的区域的子区域内重新声明变量。  
  
-   **通过继承隐藏。**如果您希望隐藏的变量是在类级别上定义的，可以通过继承隐藏该变量，用 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md) 关键字在派生类中重新声明该变量。  
  
## 隐藏变量的两种方式  
  
#### 通过范围隐藏来隐藏变量  
  
1.  确定定义您希望隐藏的变量的区域，然后确定一个子区域，在其中用您的变量重新定义该变量。  
  
    |变量的区域|允许用于重新定义变量的子区域|  
    |-----------|--------------------|  
    |模块|模块中的类|  
    |类|类中的子类<br /><br /> 类中的过程|  
  
     在该过程内的块中（例如在 `If`...`End If` 构造或 `For` 循环中）不能重新定义过程变量。  
  
2.  如果子区域尚不存在，创建子区域。  
  
3.  在子区域内，编写一个 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md) 来声明隐藏变量。  
  
     当子区域内的代码引用变量名时，编译器会将该引用解析为隐藏变量。  
  
     下面的示例阐释了通过范围进行的隐藏以及绕开隐藏的引用。  
  
    ```  
    Module shadowByScope  
        ' The following statement declares num as a module-level variable.  
        Public num As Integer  
        Sub show()  
            ' The following statement declares num as a local variable.  
            Dim num As Integer  
            ' The following statement sets the value of the local variable.  
            num = 2  
            ' The following statement displays the module-level variable.  
            MsgBox(CStr(shadowByScope.num))  
        End Sub  
        Sub useModuleLevelNum()  
            ' The following statement sets the value of the module-level variable.  
            num = 1  
            show()  
        End Sub  
    End Module  
    ```  
  
     上面的示例在模块级别和过程级别上声明变量 `num`（在过程 `show` 中）。  局部变量 `num` 在 `show` 内隐藏模块级变量 `num`，因此该局部变量设置为 2。  而在 `useModuleLevelNum` 过程中，没有局部变量隐藏 `num`。  因此，`useModuleLevelNum` 将模块级变量的值设置为 1。  
  
     `show` 内的 `MsgBox` 调用通过用模块名限定 `num` 绕开了隐藏机制。  因此，它显示的是模块级变量而不是局部变量。  
  
#### 通过继承隐藏来隐藏变量  
  
1.  确保在类中和类级别上声明您希望隐藏的变量（在任何过程外部）。  否则就不能通过继承来隐藏变量。  
  
2.  定义一个从变量的类派生的类（如果不存在这样的类）。  
  
3.  在派生类的内部，编写一个 `Dim` 语句来声明您的变量。  将 [Shadows](../../../../visual-basic/language-reference/modifiers/shadows.md) 关键字包含在声明中。  
  
     当派生类中的代码引用变量名时，编译器会将该引用解析为您的变量。  
  
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
  
     上一个示例在基类中声明变量 `shadowString`，而在派生类中隐藏该变量。  当名称 `shadowString` 没有限定时，派生类中的过程 `showStrings` 显示字符串的隐藏版本。  当 `shadowString` 由 `MyBase` 关键字限定时，则显示被隐藏的版本。  
  
## 可靠编程  
 隐藏使用同一名称引入了变量的多个版本。  如果代码语句引用该变量名，则编译器将引用解析到的版本取决于代码语句的位置以及是否存在限定字符串等因素。  这可能会增加引用被隐藏变量的非预期版本的危险。  可以通过完全限定对被隐藏变量的所有引用来降低这种风险。  
  
## 请参阅  
 [对已声明元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Visual Basic 中的隐藏](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)   
 [隐藏和重写之间的差异](../../../../visual-basic/programming-guide/language-features/declared-elements/differences-between-shadowing-and-overriding.md)   
 [如何：隐藏继承的变量](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-hide-an-inherited-variable.md)   
 [如何：访问被派生类隐藏的变量](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-access-a-variable-hidden-by-a-derived-class.md)   
 [Overrides](../../../../visual-basic/language-reference/modifiers/overrides.md)   
 [Me、My、MyBase 和 MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)   
 [继承的基础知识](../../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)