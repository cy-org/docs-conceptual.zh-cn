---
title: "如何︰ 调用命令行编译器 (Visual Basic 中) |Microsoft 文档"
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
- command-line arguments
- vbc.exe
- Visual Basic compiler, starting
- command line, arguments
ms.assetid: 0fd9a8f6-f34e-4c35-a49d-9b9bbd8da4a9
caps.latest.revision: 28
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
ms.openlocfilehash: 69c95289f91f712bd3fda03a7f582d879141591a
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-invoke-the-command-line-compiler-visual-basic"></a>如何：调用命令行编译器 (Visual Basic)
可以通过命令行中，也称为 MS-DOS 提示符中键入可执行文件的名称来调用命令行编译器。 如果从默认 Windows 命令提示符下进行编译，您必须键入的可执行文件的完全限定的路径。 若要覆盖此默认行为，您可以使用[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]命令提示符，或修改 PATH 环境变量。 同时，可以从任何目录编译通过只需键入编译器的名称。  
  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
### <a name="to-invoke-the-compiler-using-the-visual-studio-command-prompt"></a>若要使用 Visual Studio 命令提示编译器调用  
  
1.  打开 Microsoft Visual Studio 程序组中的 Visual Studio Tools 程序文件夹。  
  
2.  您可以使用[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]命令提示符下，若要从您的计算机上的任何目录访问编译器，如果安装 Visual Studio。  
  
3.  调用[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]命令提示符。  
  
4.  在命令行中，键入`vbc.exe` *sourceFileName*然后按 enter 键。  
  
     例如，如果您在一个名为目录中存储您的源代码`SourceFiles`，您应打开命令提示符并键入`cd SourceFiles`以更改到此目录。 如果该目录包含一个名为的源代码文件`Source.vb`，您可以通过键入来对其进行编译`vbc.exe Source.vb`。  
  
### <a name="to-set-the-path-environment-variable-to-the-compiler-for-the-windows-command-prompt"></a>将 PATH 环境变量设置为编译器的 Windows 命令提示符  
  
1.  使用 Windows 搜索功能在您的本地磁盘上查找 Vbc.exe。  
  
     编译器所在的目录的确切名称取决于 Windows 目录的位置和版本的[!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)]安装。 如果您有多个版本的[!INCLUDE[Compact](../../../visual-basic/reference/command-line-compiler/includes/compact_md.md)]安装，您必须确定要使用 （通常使用最新版本） 的版本。  
  
2.  从您**启动**菜单上，用鼠标右键单击**我的电脑**，然后单击**属性**从快捷菜单。  
  
3.  单击**高级**选项卡上，然后单击**环境变量**。  
  
4.  在**系统**变量窗格，选择**路径**从该列表，然后单击**编辑**。  
  
5.  在**编辑系统**变量对话框中，插入点移到中的字符串的末尾**变量值**字段中，键入以分号 （;） 后跟在步骤 1 中找到完整的目录名称。  
  
6.  单击**确定**以确认所做的编辑，然后关闭对话框。  
  
     更改 PATH 环境变量后，您可以运行[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器在 Windows 命令提示符从任何计算机上的目录。  
  
### <a name="to-invoke-the-compiler-using-the-windows-command-prompt"></a>若要使用 Windows 命令提示符编译器调用  
  
1.  从**启动**菜单上单击**附件**文件夹，然后再打开**Windows 命令提示符下**。  
  
2.  在命令行中，键入`vbc.exe` *sourceFileName*然后按 enter 键。  
  
     例如，如果您在一个名为目录中存储您的源代码`SourceFiles`，您应打开命令提示符并键入`cd SourceFiles`以更改到此目录。 如果该目录包含一个名为的源代码文件`Source.vb`，您可以通过键入来对其进行编译`vbc.exe Source.vb`。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)
