---
title: "如何：调用扩展方法 (Visual Basic) | Microsoft Docs"
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
  - "调用扩展方法"
  - "扩展方法 [Visual Basic]"
ms.assetid: df07750f-40f4-4c07-a79e-1113a27cfbea
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 如何：调用扩展方法 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

通过使用扩展方法，可以将方法添加到现有类中。  声明扩展方法并将其引入范围中后，可以调用此扩展方法，就像调用它所扩展的类型的实例方法那样。  有关如何编写扩展方法的更多信息，请参见[如何：编写扩展方法](../../../../visual-basic/programming-guide/language-features/procedures/how-to-write-an-extension-method.md)。  
  
 以下说明引用扩展方法 `PrintAndPunctuate`，这将显示调用此方法的字符串实例，后接为第二个参数 `punc` 传入的任何值。  
  
```vb#  
Imports System.Runtime.CompilerServices  
  
Module StringExtensions  
    <Extension()>   
    Public Sub PrintAndPunctuate(ByVal aString As String,   
                                 ByVal punc As String)  
        Console.WriteLine(aString & punc)  
    End Sub  
  
End Module  
  
```  
  
 在调用方法时，此方法必须在范围内。  
  
### 调用扩展方法  
  
1.  声明一个具有扩展方法第一个参数的数据类型的变量。  对于 `PrintAndPunctuate`，需要 <xref:System.String> 变量：  
  
    ```  
    Dim example = "Ready"  
    ```  
  
2.  该变量将调用扩展方法，且其值会绑定到第一个参数 `aString` 上。  下列调用语句将显示 `Ready?`。  
  
    ```  
    example.PrintAndPunctuate("?")  
    ```  
  
     请注意，对此扩展方法的调用看起来就像是对需要一个参数的任一 <xref:System.String> 实例方法的调用：  
  
    ```  
    example.EndsWith("dy")  
    example.IndexOf("R")  
    ```  
  
3.  声明另一个字符串变量并再次调用此方法以查看其是否可与任何字符串一起使用。  
  
    ```  
    Dim example2 = " or not"  
    example2.PrintAndPunctuate("!!!")  
    ```  
  
     这次的结果为：`or not!!!`。  
  
## 示例  
 下列代码是创建和使用简单扩展方法的一个完整示例。  
  
```vb#  
Imports System.Runtime.CompilerServices  
Imports ConsoleApplication1.StringExtensions  
  
Module Module1  
  
    Sub Main()  
  
        Dim example = "Hello"  
        example.PrintAndPunctuate(".")  
        example.PrintAndPunctuate("!!!!")  
  
        Dim example2 = "Goodbye"  
        example2.PrintAndPunctuate("?")  
    End Sub  
  
    <Extension()>   
    Public Sub PrintAndPunctuate(ByVal aString As String,   
                                 ByVal punc As String)  
        Console.WriteLine(aString & punc)  
    End Sub  
End Module  
  
' Output:  
' Hello.  
' Hello!!!!  
' Goodbye?  
```  
  
## 请参阅  
 [如何：编写扩展方法](../../../../visual-basic/programming-guide/language-features/procedures/how-to-write-an-extension-method.md)   
 [扩展方法](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)   
 [Visual Basic 中的范围](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)