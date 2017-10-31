---
title: "如何︰ 创建和使用程序集使用命令行 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 229ff9fb-1bd1-403b-946b-526104864c60
caps.latest.revision: 6
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 363bca806736e5540165ea96e9b4fe60d0968098
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-and-use-assemblies-using-the-command-line-visual-basic"></a>如何︰ 创建和使用程序集使用命令行 (Visual Basic)
在运行时，程序集或动态链接库 (DLL) 到您的程序链接。 为了说明如何生成和使用 DLL，请考虑以下方案︰  
  
-   `MathLibrary.DLL`︰ 包含要在运行时调用的方法的库文件。 在此示例中，该 DLL 包含两个方法，`Add`和`Multiply`。  
  
-   `Add`︰ 包含的方法在源文件`Add`。 它返回其参数的总和。 此类`AddClass`，其中包含该方法`Add`是命名空间的成员`UtilityMethods`。  
  
-   `Mult`︰ 包含的方法源代码`Multiply`。 它返回其参数的乘积。 此类`MultiplyClass`，其中包含该方法`Multiply`也是命名空间的成员`UtilityMethods`。  
  
-   `TestCode`︰ 该文件包含`Main`方法。 它使用 DLL 文件中的方法来计算 sum 和运行时参数的乘积。  
  
## <a name="example"></a>示例  
  
```vb  
' File: Add.vb   
Namespace UtilityMethods  
    Public Class AddClass  
        Public Shared Function Add(ByVal i As Long, ByVal j As Long) As Long  
            Return i + j  
        End Function  
    End Class  
End Namespace  
```  
  
```vb  
' File: Mult.vb  
Namespace UtilityMethods  
    Public Class MultiplyClass  
        Public Shared Function Multiply(ByVal x As Long, ByVal y As Long) As Long  
            Return x * y  
        End Function  
    End Class  
End Namespace  
```  
  
```vb  
' File: TestCode.vb  
  
Imports UtilityMethods  
  
Module Test  
  
    Sub Main(ByVal args As String())  
  
        System.Console.WriteLine("Calling methods from MathLibrary.DLL:")  
  
        If args.Length <> 2 Then  
            System.Console.WriteLine("Usage: TestCode <num1> <num2>")  
            Return  
        End If  
  
        Dim num1 As Long = Long.Parse(args(0))  
        Dim num2 As Long = Long.Parse(args(1))  
  
        Dim sum As Long = AddClass.Add(num1, num2)  
        Dim product As Long = MultiplyClass.Multiply(num1, num2)  
  
        System.Console.WriteLine("{0} + {1} = {2}", num1, num2, sum)  
        System.Console.WriteLine("{0} * {1} = {2}", num1, num2, product)  
  
    End Sub  
  
End Module  
  
' Output (assuming 1234 and 5678 are entered as command-line arguments):  
' Calling methods from MathLibrary.DLL:  
' 1234 + 5678 = 6912  
' 1234 * 5678 = 7006652  
```  
  
 此文件包含使用 DLL 的方法，该算法`Add`和`Multiply`。 它首先分析命令行中输入的参数`num1`和`num2`。 然后它通过使用计算总和`Add`方法`AddClass`类，并且通过使用产品`Multiply`方法`MultiplyClass`类。  
  
 请注意，`Imports`语句开头的文件使您能够使用非限定的类名来引用 DLL 方法在编译时，如下所示︰  
  
```vb  
MultiplyClass.Multiply(num1, num2)  
```  
  
 否则，您必须使用完全限定的名，如下所示︰  
  
```vb  
UtilityMethods.MultiplyClass.Multiply(num1, num2)  
```  
  
## <a name="execution"></a>执行  
 若要运行该程序，请输入跟两个数字，如下所示的 EXE 文件的名称︰  
  
 `TestCode 1234 5678`  
  
## <a name="compiling-the-code"></a>编译代码  
 若要生成文件`MathLibrary.DLL`，编译两个文件`Add`和`Mult`通过使用下面的命令行。  
  
```vb  
vbc /target:library /out:MathLibrary.DLL Add.vb Mult.vb  
```  
  
 [/Target (Visual Basic 中)](../../../../visual-basic/reference/command-line-compiler/target.md)编译器选项指示编译器将输出 DLL 而不是 EXE 文件。 [/输出 (Visual Basic 中)](../../../../visual-basic/reference/command-line-compiler/out.md)跟文件的名称的编译器选项用于指定 DLL 文件的名称。 否则，编译器将使用第一个文件 (`Add.vb`) 作为 DLL 的名称。  
  
 若要生成可执行文件， `TestCode.exe`，使用下面的命令行︰  
  
```vb  
vbc /out:TestCode.exe /reference:MathLibrary.DLL TestCode.vb  
```  
  
 **/Out**编译器选项会告知编译器输出的 EXE 文件，并指定输出文件的名称 (`TestCode.exe`)。 此编译器选项是可选的。 [/Reference (Visual Basic 中)](../../../../visual-basic/reference/command-line-compiler/reference.md)编译器选项指定的 DLL 文件或该程序使用的文件。  
  
 有关从命令行生成的详细信息，请参阅和[从命令行生成](../../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)。  
  
## <a name="see-also"></a>另请参阅  
 [编程概念](../../../../visual-basic/programming-guide/concepts/index.md)   
 [程序集和全局程序集缓存 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [创建用于容纳 DLL 函数的类](http://msdn.microsoft.com/library/e08e4c34-0223-45f7-aa55-a3d8dd979b0f)
