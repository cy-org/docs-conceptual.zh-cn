---
title: "如何︰ 创建未签名友元程序集 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 5735eb79-9729-4c46-ac1f-537ada3acaa7
caps.latest.revision: 4
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ceddb35c306f72c8927deda326d9fcca6c75d786
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-unsigned-friend-assemblies-visual-basic"></a>如何︰ 创建未签名友元程序集 (Visual Basic)
此示例演示如何对未签名的程序集使用友元程序集。  
  
### <a name="to-create-an-assembly-and-a-friend-assembly"></a>若要创建程序集和友元程序集  
  
1.  打开命令提示。  
  
2.  创建一个名为 Visual Basic 文件`friend_signed_A.`，其中包含下面的代码。 该代码使用<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>属性声明为友元程序集的 friend_signed_B。</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>  
  
    ```vb  
    ' friend_unsigned_A.vb  
    ' Compile with:   
    ' Vbc /target:library friend_unsigned_A.vb  
    Imports System.Runtime.CompilerServices  
    Imports System  
  
    <Assembly: InternalsVisibleTo("friend_unsigned_B")>   
  
    ' Friend type.  
    Friend Class Class1  
        Public Sub Test()  
            Console.WriteLine("Class1.Test")  
        End Sub  
    End Class  
  
    ' Public type with Friend member.  
    Public Class Class2  
        Friend Sub Test()  
            Console.WriteLine("Class2.Test")  
        End Sub  
    End Class  
    ```  
  
3.  编译并通过使用以下命令来签署 friend_signed_A。  
  
    ```vb  
    Vbc /target:library friend_unsigned_A.vb  
    ```  
  
4.  创建一个名为 Visual Basic 文件`friend_unsigned_B`，其中包含下面的代码。 由于 friend_unsigned_A 指定 friend_unsigned_B 作为友元程序集，所以 friend_unsigned_B 中的代码可以访问`Friend`类型和从 friend_unsigned_A 的成员。  
  
    ```vb  
    ' friend_unsigned_B.vb  
    ' Compile with:   
    ' Vbc /r:friend_unsigned_A.dll friend_unsigned_B.vb  
    Module Module1  
        Sub Main()  
            ' Access a Friend type.  
            Dim inst1 As New Class1()  
            inst1.Test()  
  
            Dim inst2 As New Class2()  
            ' Access a Friend member of a public type.  
            inst2.Test()  
  
            System.Console.ReadLine()  
        End Sub  
    End Module  
    ```  
  
5.  通过使用下面的命令编译 friend_signed_B。  
  
    ```vb  
    Vbc /r:friend_unsigned_A.dll friend_unsigned_B.vb  
    ```  
  
     由编译器生成的程序集的名称必须与传递到的友元程序集名称<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>属性。</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 通过使用可以显式设置该程序集`/out`编译器选项。  
  
6.  运行 friend_signed_B.exe 文件。  
  
     此程序将输出两个字符串:"Class1.Test"和"Class2.Test"。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>属性和<xref:System.Security.Permissions.StrongNameIdentityPermission>类</xref:System.Security.Permissions.StrongNameIdentityPermission></xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>之间有相似之处 主要区别在于<xref:System.Security.Permissions.StrongNameIdentityPermission>可要求安全权限才能运行的代码中，某个特定部分，而<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>属性控制的可见性`Friend`类型和成员。</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> </xref:System.Security.Permissions.StrongNameIdentityPermission>  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute></xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>   
 [程序集和全局程序集缓存 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [友元程序集 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/friend-assemblies.md)   
 [如何︰ 创建签名的友元程序集 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/how-to-create-signed-friend-assemblies.md)   
 [编程指南概念](../../../../visual-basic/programming-guide/concepts/index.md)
