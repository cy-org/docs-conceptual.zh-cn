---
title: "友元程序集 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 9b3d5716-e6e4-47a7-a3e9-084d7fba5c28
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
ms.openlocfilehash: c6e01ae91b9d5d875bb618993cd9eda82db59399
ms.lasthandoff: 03/13/2017

---
# <a name="friend-assemblies-visual-basic"></a>友元程序集 (Visual Basic)
一个*友元程序集*是可以访问其他程序集的程序集[朋友](../../../../visual-basic/language-reference/modifiers/friend.md)类型和成员。 如果您发现一个程序集作为友元程序集，您不再需要标记类型和成员为公共，以使其可由其他程序集访问。 这是在以下方案中特别方便︰  
  
-   在单元测试，测试代码在运行时单独的程序集，但需要访问所测试程序集中的成员标记为`Friend`。  
  
-   当您正在开发类库和库的新增功能包含在单独的程序集，但需要访问的成员的现有程序集中标记为`Friend`。  
  
## <a name="remarks"></a>备注  
 您可以使用<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>属性来标识给定程序集的一个或多个友元程序集。</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 下面的示例使用<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>属性集 A 中，指定程序集`AssemblyB`作为友元程序集。</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 这样，程序集`AssemblyB`访问所有类型和成员的程序集标记为`Friend`。  
  
> [!NOTE]
>  当编译的程序集 (程序集`AssemblyB`)，将访问内部类型或内部成员的另一个程序集 (程序集*A*)，您必须显式指定输出文件 （.exe 或.dll） 的名称，通过使用**/out**编译器选项。 这是必需的因为编译器不生成在它所绑定到外部引用时生成的程序集的名称。 有关详细信息，请参阅[/输出 (Visual Basic 中)](../../../../visual-basic/reference/command-line-compiler/out.md)。  
  
```vb  
Imports System.Runtime.CompilerServices  
Imports System  
<Assembly: InternalsVisibleTo("AssemblyB")>   
  
' Friend class.  
Friend Class FriendClass  
    Public Sub Test()  
        Console.WriteLine("Sample Class")  
    End Sub  
End Class  
  
' Public class with a Friend method.  
Public Class ClassWithFriendMethod  
    Friend Sub Test()  
        Console.WriteLine("Sample Method")  
    End Sub  
End Class  
  
```  
  
 只有您显式指定与朋友可以访问的程序集`Friend`类型和成员。 例如，如果程序集 B 的友元程序集 A 和程序集 C 引用程序集 B，C 没有对访问`Friend`A.中的类型  
  
 编译器执行的友元程序集名称传递给一些基本验证<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>属性。</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 如果程序集*A*声明*B*作为友元程序集的验证规则是，如下所示︰  
  
-   如果程序集*A*具有强名称程序集*B*还必须具有强名称。 传递给特性的友元程序集名称必须包含程序集名称和用于程序集签名的强名称密钥的公钥*B*。  
  
     友元程序集名称传递给<xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>属性不能是程序集的强名称*B*︰ 不包括程序集版本、 区域性、 体系结构或公钥标记。</xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>  
  
-   如果程序集*A*不具有强名称，友元程序集名称应仅包含程序集名称。 有关详细信息，请参阅[如何︰ 创建未签名友元程序集 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/how-to-create-unsigned-friend-assemblies.md)。  
  
-   如果程序集*B*具有强名称，必须指定程序集的强名称密钥*B*通过项目设置或命令行`/keyfile`编译器选项。 有关详细信息，请参阅[如何︰ 创建签名的友元程序集 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/how-to-create-signed-friend-assemblies.md)。  
  
 <xref:System.Security.Permissions.StrongNameIdentityPermission>类还提供了共享类型，具有以下差异的能力︰</xref:System.Security.Permissions.StrongNameIdentityPermission>  
  
-   <xref:System.Security.Permissions.StrongNameIdentityPermission>应用于单个类型，而友元程序集应用于整个程序集。</xref:System.Security.Permissions.StrongNameIdentityPermission>  
  
-   如果有数百个程序集中的类型*A*想要与程序集共享*B*，您必须添加<xref:System.Security.Permissions.StrongNameIdentityPermission>访问所有这些。</xref:System.Security.Permissions.StrongNameIdentityPermission> 如果您使用友元程序集，只需一次声明友元关系。  
  
-   如果您使用<xref:System.Security.Permissions.StrongNameIdentityPermission>，您想要共享的类型必须声明为公共。</xref:System.Security.Permissions.StrongNameIdentityPermission> 如果您使用友元程序集，共享的类型被声明为`Friend`。  
  
 有关如何访问程序集的信息`Friend`类型和方法从模块文件 （扩展名为.netmodule 文件），请参阅[/moduleassemblyname (Visual Basic 中)](../../../../visual-basic/reference/command-line-compiler/moduleassemblyname.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute></xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>   
 <xref:System.Security.Permissions.StrongNameIdentityPermission></xref:System.Security.Permissions.StrongNameIdentityPermission>   
 [如何︰ 创建未签名友元程序集 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/how-to-create-unsigned-friend-assemblies.md)   
 [如何︰ 创建签名的友元程序集 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/how-to-create-signed-friend-assemblies.md)   
 [程序集和全局程序集缓存 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [编程概念](../../../../visual-basic/programming-guide/concepts/index.md)
