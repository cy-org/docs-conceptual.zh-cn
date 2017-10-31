---
title: "如何︰ 确定文件是否为程序集 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: de26f410-9bd1-4b55-a343-cc82f81684be
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
ms.openlocfilehash: 2e58363369ae4420879310bf09ed89cdd4f5b5cc
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-determine-if-a-file-is-an-assembly-visual-basic"></a>如何︰ 确定文件是否为程序集 (Visual Basic)
当且仅当它处于托管状态，并包含其元数据中的程序集条目，则文件是程序集。 程序集和元数据的详细信息，请参阅主题[程序集清单](https://msdn.microsoft.com/library/1w45z383)。  
  
## <a name="how-to-manually-determine-if-a-file-is-an-assembly"></a>如何手动确定文件是否为程序集  
  
1.  启动[Ildasm.exe （IL 反汇编程序）](https://msdn.microsoft.com/library/f7dy01k1)。  
  
2.  加载你要测试的文件。  
  
3.  如果**ILDASM**报表文件不是一个可移植可执行 (PE) 文件，则它不是程序集。 有关详细信息，请参阅主题[如何︰ 查看程序集内容](http://msdn.microsoft.com/library/fb7baaab-4c0d-47ad-8fd3-4591cf834709)。  
  
## <a name="how-to-programmatically-determine-if-a-file-is-an-assembly"></a>如何以编程方式确定文件是否为程序集  
  
1.  调用<xref:System.Reflection.AssemblyName.GetAssemblyName%2A>方法，并传递的完整文件路径和要测试的文件的名称。</xref:System.Reflection.AssemblyName.GetAssemblyName%2A>  
  
2.  如果<xref:System.BadImageFormatException>引发异常，该文件不是程序集。</xref:System.BadImageFormatException>  
  
## <a name="example"></a>示例  
 此示例测试以查看它是否为程序集 DLL。  
  
```vb  
Module Module1  
    Sub Main()  
        Try  
            Dim testAssembly As Reflection.AssemblyName =  
                                Reflection.AssemblyName.GetAssemblyName("C:\Windows\Microsoft.NET\Framework\v3.5\System.Net.dll")  
            Console.WriteLine("Yes, the file is an Assembly.")  
        Catch ex As System.IO.FileNotFoundException  
            Console.WriteLine("The file cannot be found.")  
        Catch ex As System.BadImageFormatException  
            Console.WriteLine("The file is not an Assembly.")  
        Catch ex As System.IO.FileLoadException  
            Console.WriteLine("The Assembly has already been loaded.")  
        End Try  
        Console.ReadLine()  
    End Sub  
End Module  
' Output (with .NET Framework 3.5 installed):  
'        Yes, the file is an Assembly.  
```
  
 <xref:System.Reflection.AssemblyName.GetAssemblyName%2A>方法加载测试文件，并将读取的信息之后，然后释放它。</xref:System.Reflection.AssemblyName.GetAssemblyName%2A>  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Reflection.AssemblyName></xref:System.Reflection.AssemblyName>   
 [编程概念](../../../../visual-basic/programming-guide/concepts/index.md)   
 [程序集和全局程序集缓存 (Visual Basic)](index.md)
