---
title: "如何︰ 创建签名的友元程序集 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: f2afd83d-b044-484b-a56d-56d0a8a40647
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
ms.openlocfilehash: 1a69f7e833800ec7417bc35fad763f1001b3e7f9
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-signed-friend-assemblies-visual-basic"></a>如何︰ 创建签名的友元程序集 (Visual Basic)
此示例演示如何对具有强名称的程序集使用友元程序集。 两个程序集必须具有强名称。 尽管在此示例中两个程序集使用相同的密钥，但您可以为两个程序集使用不同的密钥。  
  
### <a name="to-create-a-signed-assembly-and-a-friend-assembly"></a>若要创建签名的程序集和友元程序集  
  
1.  打开命令提示。  
  
2.  下面的命令序列使用强名称工具，以生成密钥文件并显示其公钥。 有关详细信息，请参阅 [Sn.exe （强名称工具）](https://msdn.microsoft.com/library/k5b5tt23)。  
  
    1.  生成此示例的强名称密钥，并将其存储在文件 FriendAssemblies.snk:  
  
         `sn -k FriendAssemblies.snk`  
  
    2.  从 FriendAssemblies.snk 中提取公钥并将其放入 FriendAssemblies.publickey:  
  
         `sn -p FriendAssemblies.snk FriendAssemblies.publickey`  
  
    3.  此时会显示在文件 FriendAssemblies.publickey 中存储的公钥︰  
  
         `sn -tp FriendAssemblies.publickey`  
  
3.  创建一个名为 Visual Basic 文件`friend_signed_A`，其中包含下面的代码。 该代码使用<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>属性声明为友元程序集的 friend_signed_B。</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>  
  
     每次运行时，强名称工具会生成新的公钥。 因此，您必须将下面的代码中的公钥替换只是生成的公钥如下面的示例中所示。  
  
    ```vb  
    ' friend_signed_A.vb  
    ' Compile with:   
    ' Vbc /target:library /keyfile:FriendAssemblies.snk friend_signed_A.vb  
    Imports System.Runtime.CompilerServices  
  
    <Assembly: InternalsVisibleTo("friend_signed_B, PublicKey=0024000004800000940000000602000000240000525341310004000001000100e3aedce99b7e10823920206f8e46cd5558b4ec7345bd1a5b201ffe71660625dcb8f9a08687d881c8f65a0dcf042f81475d2e88f3e3e273c8311ee40f952db306c02fbfc5d8bc6ee1e924e6ec8fe8c01932e0648a0d3e5695134af3bb7fab370d3012d083fa6b83179dd3d031053f72fc1f7da8459140b0af5afc4d2804deccb6")>   
    Public Class Class1  
        Public Sub Test()  
            System.Console.WriteLine("Class1.Test")  
            System.Console.ReadLine()  
        End Sub  
    End Class  
    ```  
  
4.  编译并通过使用以下命令来签署 friend_signed_A。  
  
    ```vb  
    Vbc /target:library /keyfile:FriendAssemblies.snk friend_signed_A.vb  
    ```  
  
5.  创建名为的 Visual Basic 文件`friend_signed_B`，并包含以下代码。 由于 friend_signed_A 指定 friend_signed_B 作为友元程序集，所以 friend_signed_B 中的代码可以访问`Friend`类型和从 friend_signed_A 的成员。 该文件包含下面的代码。  
  
    ```vb  
    ' friend_signed_B.vb  
    ' Compile with:   
    ' Vbc /keyfile:FriendAssemblies.snk /r:friend_signed_A.dll friend_signed_B.vb  
    Module Sample  
        Public Sub Main()  
            Dim inst As New Class1  
            inst.Test()  
        End Sub  
    End Module  
    ```  
  
6.  编译并通过使用以下命令来签署 friend_signed_B。  
  
    ```vb  
    Vbc /keyfile:FriendAssemblies.snk /r:friend_signed_A.dll friend_signed_B.vb  
    ```  
  
     由编译器生成的程序集名称必须与匹配的友元程序集名称传递给<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>属性。</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 通过使用可以显式设置该程序集`/out`编译器选项。 有关详细信息，请参阅[/输出 (Visual Basic 中)](../../../../visual-basic/reference/command-line-compiler/out.md)。  
  
7.  运行 friend_signed_B.exe 文件。  
  
     此程序将输出字符串"Class1.Test"。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>属性和<xref:System.Security.Permissions.StrongNameIdentityPermission>类</xref:System.Security.Permissions.StrongNameIdentityPermission></xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>之间有相似之处 主要区别在于<xref:System.Security.Permissions.StrongNameIdentityPermission>可要求安全权限才能运行的代码中，某个特定部分，而<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>属性控制的可见性`Friend`类型和成员。</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> </xref:System.Security.Permissions.StrongNameIdentityPermission>  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute></xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>   
 [程序集和全局程序集缓存 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [友元程序集 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/friend-assemblies.md)   
 [如何︰ 创建未签名友元程序集 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/how-to-create-unsigned-friend-assemblies.md)   
 [/keyfile](../../../../visual-basic/reference/command-line-compiler/keyfile.md)   
 [Sn.exe （强名称工具）](https://msdn.microsoft.com/library/k5b5tt23)   
 [创建和使用具有强名称程序集](https://msdn.microsoft.com/library/xwb8f617)   
 [编程概念](../../../../visual-basic/programming-guide/concepts/index.md)
