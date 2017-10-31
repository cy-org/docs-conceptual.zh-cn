---
title: "Visual Basic 中的 Main 过程 | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Main"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "主函数"
  - "Main 方法 [Visual Basic]"
  - "Main 过程"
ms.assetid: f0db283e-f283-4464-b521-b90858cc1b44
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Visual Basic 中的 Main 过程
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

每个 Visual Basic 应用程序均必须包含一个称为 `Main` 的过程。  该过程为应用程序的起始点并为应用程序提供总体控制。  .NET Framework 在已加载应用程序并准备将控制传递给它时，将调用 `Main` 过程。  除非您要创建 Windows 窗体应用程序，否则就必须为自运行的应用程序编写 `Main` 过程。  
  
 `Main` 中包含首先运行的代码。  在 `Main` 中，可以确定在程序启动时首先加载的窗体，确定系统上是否已在运行您的应用程序副本，为应用程序建立一组变量，或者打开应用程序需要的数据库。  
  
## Main 过程的要求  
 独立运行的文件（扩展名通常为 .exe）必须包含 `Main` 过程。  库（例如，扩展名为 .dll）不独立运行，因而不需要 `Main` 过程。  可以创建的不同类型的项目的要求如下：  
  
-   控制台应用程序可以独立运行，而且您必须提供至少一个 `Main` 过程。  .  
  
-   Windows 窗体应用程序可以独立运行。  但是，Visual Basic 编译器会在此类应用程序中自动生成一个 `Main` 过程，因而您不需要编写此过程。  
  
-   类库不需要 `Main` 过程。  这些类库包括 Windows 控件库和 Web 控件库。  作为类库部署 Web 应用程序。  
  
## 声明 Main 过程  
 有四种方法可以声明 `Main` 过程。  它可以使用参数或不使用参数，可以返回值或不返回值。  
  
> [!NOTE]
>  如果在类中声明 `Main` 过程，则必须使用 `Shared` 关键字。  在模块中，`Main` 不必是 `Shared`。  
  
-   最简单的方法是声明一个不使用参数或不返回值的 `Sub` 过程。  
  
    ```  
    Module mainModule  
        Sub Main()  
            MsgBox("The Main procedure is starting the application.")  
            ' Insert call to appropriate starting place in your code.  
            MsgBox("The application is terminating.")  
        End Sub  
    End Module  
    ```  
  
-   `Main` 还可以返回一个 `Integer` 值，操作系统将其作为程序的退出代码。  其他程序可以通过检查 Windows ERRORLEVEL 值来测试该代码。  若要返回退出代码，必须将 `Main` 过程声明为 `Function` 过程而不是 `Sub` 过程。  
  
    ```  
    Module mainModule  
        Function Main() As Integer  
            MsgBox("The Main procedure is starting the application.")  
            Dim returnValue As Integer = 0  
            ' Insert call to appropriate starting place in your code.  
            ' On return, assign appropriate value to returnValue.  
            ' 0 usually means successful completion.  
            MsgBox("The application is terminating with error level " &  
                 CStr(returnValue) & ".")  
            Return returnValue  
        End Function  
    End Module  
    ```  
  
-   `Main` 还可以采用一个 `String` 数组作为参数。  数组中的每个字符串均包含一个用于调用程序的命令行参数。  您可以根据它们的值采取不同的操作。  
  
    ```  
    Module mainModule  
        Function Main(ByVal cmdArgs() As String) As Integer  
            MsgBox("The Main procedure is starting the application.")  
            Dim returnValue As Integer = 0  
            ' See if there are any arguments.  
            If cmdArgs.Length > 0 Then  
                For argNum As Integer = 0 To UBound(cmdArgs, 1)  
                    ' Insert code to examine cmdArgs(argNum) and take  
                    ' appropriate action based on its value.  
                Next argNum  
            End If  
            ' Insert call to appropriate starting place in your code.  
            ' On return, assign appropriate value to returnValue.  
            ' 0 usually means successful completion.  
            MsgBox("The application is terminating with error level " &  
                 CStr(returnValue) & ".")  
            Return returnValue  
        End Function  
    End Module  
    ```  
  
-   可以声明 `Main` 来检查命令行参数而不返回退出代码，如下所示。  
  
    ```  
    Module mainModule  
        Sub Main(ByVal cmdArgs() As String)  
            MsgBox("The Main procedure is starting the application.")  
            Dim returnValue As Integer = 0  
            ' See if there are any arguments.  
            If cmdArgs.Length > 0 Then  
                For argNum As Integer = 0 To UBound(cmdArgs, 1)  
                    ' Insert code to examine cmdArgs(argNum) and take  
                    ' appropriate action based on its value.  
                Next argNum  
            End If  
            ' Insert call to appropriate starting place in your code.  
            MsgBox("The application is terminating.")  
        End Sub  
    End Module  
    ```  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>   
 <xref:System.Array.Length%2A>   
 <xref:Microsoft.VisualBasic.Information.UBound%2A>   
 [Visual Basic 程序的结构](../../../visual-basic/programming-guide/program-structure/structure-of-a-visual-basic-program.md)   
 [“Hello, World”的 Visual Basic 版本](http://msdn.microsoft.com/zh-cn/9d030b60-e148-4366-a462-69532f02294c)   
 [\/main](../../../visual-basic/reference/command-line-compiler/main.md)   
 [Shared](../../../visual-basic/language-reference/modifiers/shared.md)   
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Integer 数据类型](../../../visual-basic/language-reference/data-types/integer-data-type.md)   
 [String 数据类型](../../../visual-basic/language-reference/data-types/string-data-type.md)