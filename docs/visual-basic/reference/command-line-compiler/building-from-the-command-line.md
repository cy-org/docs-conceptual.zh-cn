---
title: "从命令行 (Visual Basic 中) 生成 |Microsoft 文档"
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
- builds [Visual Basic], command-line
- Visual Basic compiler, about Visual Basic compiler
- command line [Visual Basic], compilers
- command line [Visual Basic], building from
- command line [Visual Basic], builds
- compilers, invoking from command line
- command-line builds
- compiling source code
- command-line compilers, Visual Basic
- command line [Visual Basic], Visual Basic
ms.assetid: e61947e9-a42e-4717-a699-5f70a98cdd03
caps.latest.revision: 13
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
ms.openlocfilehash: 49f84c221e18457ab46534ca46da7c4764a8ee40
ms.lasthandoff: 03/13/2017

---
# <a name="building-from-the-command-line-visual-basic"></a>从命令行生成 (Visual Basic)
一个[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]项目由一个或多个单独的源代码文件组成。 在称为编译过程中，这些文件被集中到一个包，可以为应用程序运行的单个可执行文件。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]作为从编译的程序的替代方法提供命令行编译器[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]集成的开发环境 (IDE)。 命令行编译器设计为不需要的 IDE 功能的完整一套情况 — 例如，当在使用或编写使用有限的系统内存或存储空间的计算机。  
  
 当从命令行编译时，必须显式引用 Microsoft[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]通过运行时库`/reference`编译器选项。  
  
 若要编译源文件中的[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]IDE 中，选择**生成**命令**生成**菜单。  
  
> [!TIP]
>  通过使用 Visual Studio IDE 生成项目文件时，可以显示有关关联信息**vbc**命令，并在输出窗口中的开关。 若要显示此信息，请打开[选项对话框、 项目和解决方案、 生成和运行](https://docs.microsoft.com/visualstudio/ide/reference/options-dialog-box-projects-and-solutions-build-and-run)，然后设置**MSBuild 项目生成输出详细程度**到**正常**或更高版本的详细程度级别。 有关详细信息，请参阅[如何：查看、保存和配置生成日志文件](http://msdn.microsoft.com/library/75d38b76-26d6-4f43-bbe7-cbacd7cc81e7)。  
  
 您可以使用 MSBuild 来编译项目 (.vbproj) 文件在命令提示符。 有关详细信息，请参阅[命令行参考](https://docs.microsoft.com/visualstudio/msbuild/msbuild-command-line-reference)和[演练︰ 使用 MSBuild](http://msdn.microsoft.com/library/b8a8b866-bb07-4abf-b9ec-0b40d281c310)。  
  
## <a name="in-this-section"></a>本节内容  
 [如何：调用命令行编译器](../../../visual-basic/reference/command-line-compiler/how-to-invoke-the-command-line-compiler.md)  
 介绍如何调用命令行编译器在 MS-DOS 提示符处或从特定的子目录。  
  
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 列出您可以修改用于您自己的示例命令行。  
  
## <a name="related-sections"></a>相关章节  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)  
 列出的编译器选项，按字母顺序还是按目的组织。  
  
 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)  
 描述如何编译特定的代码节。  
  
 [在 Visual Studio 中生成和清理项目和解决方案](https://docs.microsoft.com/visualstudio/ide/building-and-cleaning-projects-and-solutions-in-visual-studio)  
 描述如何组织内容将包含在不同版本中，请选择项目属性并确保项目按正确的顺序生成。
