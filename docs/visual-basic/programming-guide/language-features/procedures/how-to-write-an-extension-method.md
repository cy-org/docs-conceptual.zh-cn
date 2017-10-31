---
title: "如何：编写扩展方法 (Visual Basic) | Microsoft Docs"
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
  - "扩展数据类型"
  - "扩展方法 [Visual Basic]"
  - "编写扩展方法"
ms.assetid: fb2739cc-958d-4ef4-a38b-214a74c93413
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 如何：编写扩展方法 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

通过使用扩展方法，可以将方法添加到现有类中。  可将扩展方法当作该类的实例来调用。  
  
### 定义扩展方法  
  
1.  在 Visual Studio 中打开新的或现有的 Visual Basic 应用程序。  
  
2.  在想要在其中定义扩展方法的文件的顶部，添加以下导入语句：  
  
    ```  
    Imports System.Runtime.CompilerServices  
    ```  
  
3.  在新应用程序或现有应用程序的模块内，从扩展特性开始进行方法定义：  
  
    ```  
    <Extension()>  
    ```  
  
4.  以普通方式声明方法，除非第一个参数的类型必须为想要扩展的数据类型。  
  
    ```  
    <Extension()>   
    Public Sub subName (ByVal para1 As ExtendedType, <other parameters>)  
         ' < Body of the method >  
    End Sub  
    ```  
  
## 示例  
 下面的示例在模块 `StringExtensions` 中声明扩展方法。  第二个模块 `Module1` 导入 `StringExtensions` 并调用此方法。  调用扩展方法时，该方法必须在范围内。  扩展方法 `PrintAndPunctuate` 使用一个显示字符串实例（后跟一个以参数形式传入的标点符号字符串）的方法扩展 <xref:System.String> 类。  
  
```vb#  
' Declarations will typically be in a separate module.  
Imports System.Runtime.CompilerServices  
  
Module StringExtensions  
    <Extension()>   
    Public Sub PrintAndPunctuate(ByVal aString As String,   
                                 ByVal punc As String)  
        Console.WriteLine(aString & punc)  
    End Sub  
  
End Module  
```  
  
```vb#  
' Import the module that holds the extension method you want to use,   
' and call it.  
  
Imports ConsoleApplication2.StringExtensions  
  
Module Module1  
  
    Sub Main()  
        Dim example = "Hello"  
        example.PrintAndPunctuate("?")  
        example.PrintAndPunctuate("!!!!")  
    End Sub  
  
End Module  
  
```  
  
 请注意，该方法是用两个参数定义的，但只使用其中一个参数对其进行调用。  方法定义中的第一个参数 `aString` 被绑定到 `example`（调用方法的 `String` 的实例）。  该示例的输出如下所示：  
  
 `Hello?`  
  
 `Hello!!!!`  
  
## 请参阅  
 <xref:System.Runtime.CompilerServices.ExtensionAttribute>   
 [扩展方法](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)   
 [Module 语句](../../../../visual-basic/language-reference/statements/module-statement.md)   
 [过程参数和自变量](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Visual Basic 中的范围](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)