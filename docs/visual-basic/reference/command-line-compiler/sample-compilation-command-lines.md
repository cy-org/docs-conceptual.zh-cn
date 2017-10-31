---
title: "示例编译命令行 (Visual Basic 中) |Microsoft 文档"
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
- command line, compilers
- compilation, command-line
- command-line compilers
- compiling source code, from command line
- Visual Basic compiler, sample command lines
ms.assetid: 5bfbb487-5f47-4267-969a-39dfb917beeb
caps.latest.revision: 14
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 918787b3377f2e5a636a6b098046ac2f455efcdd
ms.lasthandoff: 03/13/2017

---
# <a name="sample-compilation-command-lines-visual-basic"></a>示例编译命令行 (Visual Basic)
作为编译的替代方法[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]程序从[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]，您可以从命令行以生成可执行文件 (.exe) 文件或动态链接库 (.dll) 文件进行编译。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]命令行编译器支持一组完整的控制输入和输出文件、 程序集，以及调试的选项和预处理器选项。 每个选项可在两个可互换的窗体中︰`-``option`和`/``option`。 本文档仅显示`/``option`窗体。  
  
 下表列出了一些示例命令行，您可以修改供自己使用。  
  
|到|使用|  
|--------|---------|  
|编译 File.vb 并创建 File.exe|`vbc /reference:Microsoft.VisualBasic.dll File.vb`|  
|编译 File.vb 并创建 File.dll|`vbc /target:library File.vb`|  
|编译 File.vb 并创建 My.exe|`vbc /out:My.exe File.vb`|  
|将所有编译[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]上文件在当前目录中，进行了优化和`DEBUG`符号定义，从而生成 File2.exe|`vbc /define:DEBUG=1 /optimize /out:File2.exe *.vb`|  
|将所有编译[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]文件在当前目录中，不显示徽标或警告的情况下生成 File2.dll 的调试版本|`vbc /target:library /out:File2.dll /nowarn /nologo /debug *.vb`|  
|将所有编译[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Something.dll 到当前目录中的文件|`vbc /target:library /out:Something.dll *.vb`|  
  
 当从命令行编译时，必须显式引用 Microsoft[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]通过运行时库`/reference`编译器选项。  
  
> [!TIP]
>  通过使用 Visual Studio IDE 生成项目时，可以显示有关关联信息**vbc**命令，并在输出窗口中与之编译器选项。 若要显示此信息，请打开[选项对话框、 项目和解决方案、 生成和运行](https://docs.microsoft.com/visualstudio/ide/reference/options-dialog-box-projects-and-solutions-build-and-run)，然后设置**MSBuild 项目生成输出详细程度**到**正常**或更高版本的详细程度级别。 有关详细信息，请参阅[如何：查看、保存和配置生成日志文件](http://msdn.microsoft.com/library/75d38b76-26d6-4f43-bbe7-cbacd7cc81e7)。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)
