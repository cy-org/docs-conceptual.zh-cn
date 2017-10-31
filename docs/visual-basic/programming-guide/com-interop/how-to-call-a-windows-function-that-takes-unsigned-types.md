---
title: "如何︰ 调用采用无符号的类型 (Visual Basic 中) 的 Windows 函数 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Windows functions, calling
- unsigned data types
- UShort data type, using
- functions [Visual Basic], calling Windows functions
- ULong data type, using
- UInteger data type, using
- data types [Visual Basic], using
- unsigned types
- data types [Visual Basic], unsigned
- data types [Visual Basic], numeric
- unsigned types, using
ms.assetid: c2c0e712-8dc2-43b9-b4c6-345fbb02e7ce
caps.latest.revision: 18
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: fbff07f4923b0633a2bc9b4fd558d9d51f64370a
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-call-a-windows-function-that-takes-unsigned-types-visual-basic"></a>如何：调用采用无符号类型的 Windows 函数 (Visual Basic)
如果您正在使用类、 模块或具有无符号的整数类型的成员的结构，您可以访问这些成员与[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。  
  
### <a name="to-call-a-windows-function-that-takes-an-unsigned-type"></a>若要调用采用无符号的类型的 Windows 函数  
  
1.  使用[声明语句](../../../visual-basic/language-reference/statements/declare-statement.md)告诉[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]的库包含函数、 什么其名称是在库中、 其调用的顺序是什么，和如何将字符串转换调用时。  
  
2.  在`Declare`语句中，使用`UInteger`， `ULong`， `UShort`，或`Byte`为适合于无符号类型的每个参数。  
  
3.  查阅文档以获取要调用要查找的名称和值的常量，它使用的 Windows 函数。 其中许多 WinUser.h 文件中定义。  
  
4.  声明在代码中必要的常数。 许多 Windows 常量是 32 位无符号的值，并应将这些声明`As``UInteger`。  
  
5.  以正常方式调用函数。 下面的示例调用 Windows 函数`MessageBox`，它将采用一个无符号的整数参数。  
  
    ```  
    Public Class windowsMessage  
        Private Declare Auto Function mb Lib "user32.dll" Alias "MessageBox" (  
            ByVal hWnd As Integer,   
            ByVal lpText As String,   
            ByVal lpCaption As String,   
            ByVal uType As UInteger) As Integer  
        Private Const MB_OK As UInteger = 0  
        Private Const MB_ICONEXCLAMATION As UInteger = &H30  
        Private Const IDOK As UInteger = 1  
        Private Const IDCLOSE As UInteger = 8  
        Private Const c As UInteger = MB_OK Or MB_ICONEXCLAMATION  
        Public Function messageThroughWindows() As String  
            Dim r As Integer = mb(0, "Click OK if you see this!",   
                "Windows API call", c)  
            Dim s As String = "Windows API MessageBox returned " &  
                 CStr(r)& vbCrLf & "(IDOK = " & CStr(IDOK) &  
                 ", IDCLOSE = " & CStr(IDCLOSE) & ")"  
            Return s  
        End Function  
    End Class  
    ```  
  
     您可以测试该函数`messageThroughWindows`替换为以下代码。  
  
    ```  
    Public Sub consumeWindowsMessage()  
        Dim w As New windowsMessage  
        w.messageThroughWindows()  
    End Sub  
    ```  
  
    > [!CAUTION]
    >  `UInteger`， `ULong`， `UShort`，和`SByte`数据类型不属于[语言独立性和与语言无关的组件](https://msdn.microsoft.com/library/12a7a7h3)(CLS)，因此符合 cls 的代码不能使用它们使用的组件。  
  
    > [!IMPORTANT]
    >  Windows 应用程序编程接口 (API)，如在非托管代码调用公开您的代码与潜在的安全风险。  
  
    > [!IMPORTANT]
    >  调用 Windows API 要求非托管的代码的权限，这可能会影响它在部分信任的情况下执行。 有关详细信息，请参阅<xref:System.Security.Permissions.SecurityPermission>和[代码访问权限](http://msdn.microsoft.com/en-us/e5ae402f-6dda-4732-bbe8-77296630f675)。</xref:System.Security.Permissions.SecurityPermission>  
  
## <a name="see-also"></a>另请参阅  
 [数据类型](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [整数数据类型](../../../visual-basic/language-reference/data-types/integer-data-type.md)   
 [UInteger 数据类型](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)   
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [演练：调用 Windows API](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)
