---
title: "/target (Visual Basic 中) |Microsoft 文档"
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
- target compiler options [Visual Basic]
- -target compiler options [Visual Basic]
- /target compiler options [Visual Basic]
ms.assetid: e0954147-548b-461f-9c4b-a8f88845616c
caps.latest.revision: 29
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
ms.openlocfilehash: ccdb87188b924303057d5867dccece937defe74d
ms.lasthandoff: 03/13/2017

---
# <a name="target-visual-basic"></a>/target (Visual Basic)
指定编译器输出的格式。  
  
## <a name="syntax"></a>语法  
  
```  
/target:{exe | library | module | winexe | appcontainerexe | winmdobj}  
```  
  
## <a name="remarks"></a>备注  
 下表总结了的效果`/target`选项。  
  
|**选项**|**行为**|  
|----------------|------------------|  
|`/target:exe`|使编译器创建可执行文件的控制台应用程序。<br /><br /> 这是默认选项，如果未`/target`指定选项。 扩展名为.exe 创建可执行文件。<br /><br /> 除非另行指定与`/out`选项，输出文件名采用包含的输入文件名称`Sub Main`过程。<br /><br /> 只有一个`Sub Main`过程必需的源代码文件编译到.exe 文件中。 使用`/main`编译器选项来指定哪个类包含`Sub Main`过程。|  
|`/target:library`|使编译器创建一个动态链接库 (DLL)。<br /><br /> 带有.dll 扩展创建动态链接库文件。<br /><br /> 除非另行指定与`/out`选项，输出文件的名称采用第一个输入文件的名称。<br /><br /> 在生成的 DLL 时`Sub Main`则不需要过程。|  
|`/target:module`|会导致编译器生成一个模块，可以添加到程序集。<br /><br /> 扩展名为.netmodule 创建输出文件。<br /><br /> .NET 公共语言运行时无法加载不具有程序集的文件。 但是，您可以将合并此类文件到程序集清单的程序集通过使用`/reference`。<br /><br /> 当一个模块中的代码引用另一个模块中的内部类型时，必须通过使用合并到一个程序集清单这两个模块`/reference`。<br /><br /> [/Addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)选项从模块导入元数据。|  
|`/target:winexe`|使编译器来创建基于 Windows 的应用程序可执行文件。<br /><br /> 扩展名为.exe 创建可执行文件。 基于 Windows 的应用程序是指提供了从用户界面[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]类库或 Win32 Api。<br /><br /> 除非另行指定与`/out`选项，输出文件名采用包含的输入文件名称`Sub Main`过程。<br /><br /> 只有一个`Sub Main`过程必需的源代码文件编译到.exe 文件中。 在您的代码有多个类都包含其中的情况下`Sub Main`过程，请使用`/main`编译器选项来指定哪个类包含`Sub Main`过程|  
|`/target:appcontainerexe`|使编译器创建的可执行文件的基于 Windows 的应用程序必须在应用程序容器中运行。 此设置设计用于[!INCLUDE[win8_appname_long](../../../csharp/includes/win8_appname_long_md.md)]应用程序。<br /><br /> **Appcontainerexe**设置的特性字段中设置一个位[可移植可执行](http://go.microsoft.com/fwlink/p/?LinkId=236960)文件。 此位指示应用程序，必须运行应用程序容器中。 如果当设置此位，则会出错`CreateProcess`方法尝试启动应用程序容器之外的应用程序。 除了这位的设置， **/target: appcontainerexe**等同于**/target: winexe**。<br /><br /> 扩展名为.exe 创建可执行文件。<br /><br /> 除非另行指定，否则使用`/out`选项，输出文件名采用包含的输入文件名称`Sub Main`过程。<br /><br /> 只有一个`Sub Main`过程必需的源代码文件编译到.exe 文件中。 如果您的代码将包含多个类，该类具有`Sub Main`过程，请使用`/main`编译器选项来指定哪个类包含`Sub Main`过程|  
|`/target:winmdobj`|使编译器创建的中间文件，则可以将它们转换为 Windows 运行时二进制 (.winmd) 文件。 JavaScript 和 c + + 程序，除了托管的语言程序外，可以使用该.winmd 文件。<br /><br /> .Winmdobj 扩展名为创建中间文件。<br /><br /> 除非另行指定，否则使用`/out`选项，输出文件的名称采用第一个输入文件的名称。 一个`Sub Main`过程并不是必需。<br /><br /> .Winmdobj 文件旨在以用作输入<xref:Microsoft.Build.Tasks.WinMDExp>导出工具以生成 Windows 元数据 (WinMD) 文件。</xref:Microsoft.Build.Tasks.WinMDExp> WinMD 文件扩展名为.winmd，并包含从原始的库和 WinMD 定义这两种代码，该 JavaScript、 c + + 和 Windows 运行时使用。|  
  
 除非您指定`/target:module`，`/target`导致[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]要添加到输出文件的程序集清单。  
  
 Vbc.exe 的每个实例生成，最多一个输出文件。 如果指定的编译器选项如`/out`或`/target`不止一次，最后一个编译器可处理将生效。 在编译中的所有文件的信息添加到清单。 所有输出文件的文件除外使用创建`/target:module`包含在清单中的程序集元数据。 使用[Ildasm.exe （IL 反汇编程序）](https://msdn.microsoft.com/library/f7dy01k1)输出文件中查看元数据。  
  
 缩写形式`/target`是`/t`。  
  
### <a name="to-set-target-in-the-visual-studio-ide"></a>在 Visual Studio IDE 中设置 /target  
  
1.  在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。  
  
2.  单击“应用程序” **** 选项卡。  
  
3.  在修改此值**应用程序类型**框。  
  
## <a name="example"></a>示例  
 下面的代码编译`in.vb`，则创建`in.dll`:  
  
```  
vbc /target:library in.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/main](../../../visual-basic/reference/command-line-compiler/main.md)   
 [/ 输出 (Visual Basic)](../../../visual-basic/reference/command-line-compiler/out.md)   
 [/reference (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)   
 [/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)   
 [/moduleassemblyname](../../../visual-basic/reference/command-line-compiler/moduleassemblyname.md)   
 [程序集和全局程序集缓存](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
