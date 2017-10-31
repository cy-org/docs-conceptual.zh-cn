---
title: "/platform (Visual Basic 中) |Microsoft 文档"
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
- platform compiler option [Visual Basic]
- /platform compiler option [Visual Basic]
- -platform compiler option [Visual Basic]
ms.assetid: f9bc61e6-e854-4ae1-87b9-d6244de23fd1
caps.latest.revision: 34
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
ms.openlocfilehash: 6216ee056bc9dd8dd7dfd95b9d5a031880209370
ms.lasthandoff: 03/13/2017

---
# <a name="platform-visual-basic"></a>/platform (Visual Basic)
指定公共语言运行时 (CLR) 的哪个平台版本可以运行输出文件。  
  
## <a name="syntax"></a>语法  
  
```  
/platform:{ x86 | x64 | Itanium | arm | anycpu | anycpu32bitpreferred }  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`x86`|将程序集编译成可由 32 位、x86 可兼容 CLR 运行。|  
|`x64`|将程序集编译成可由支持 AMD64 或 EM64T 指令集的计算机上的 64 位 CLR 运行。|  
|`Itanium`|将程序集编译成可由配有 Itanium 处理器的计算机上的 64 位 CLR 运行。|  
|`arm`|将程序集编译成可在配有高级 RISC 计算机 (ARM) 处理器的计算机上运行。|  
|`anycpu`|将程序集编译成可在任意平台上运行。 应用程序将作为 32 位应用程序在 Windows 的 32 位版本上运行，作为 64 位应用程序在 Windows 的 64 位版本上运行。 此标志为默认值。|  
|`anycpu32bitpreferred`|将程序集编译成可在任意平台上运行。 应用程序将作为 32 位 应用程序在 Windows 的 32 位版本和 64 位版本上运行。 此标志仅对可执行文件 (.EXE) 有效且需要 [!INCLUDE[net_v45](../../../csharp/language-reference/compiler-options/includes/net_v45_md.md)]。|  
  
## <a name="remarks"></a>备注  
 使用 `/platform` 选项来指定输出文件所面向的处理器类型。  
  
 通常，无论平台如何，Visual Basic 内编写的 .NET Framework 程序集将运行相同内容。 但是，存在一些不同平台行为不同的情况。 这些常见的情况是：  
  
-   结构中包含大小随平台而改变的成员，如任何指针类型。  
  
-   指针算术包含固定大小。  
  
-   不正确的平台调用或 COM 声明将`Integer`句柄而不是<xref:System.IntPtr>。</xref:System.IntPtr>  
  
-   强制转换<xref:System.IntPtr>到`Integer`。</xref:System.IntPtr>  
  
-   将平台调用或 COM 互操作与不存在于任何平台的组件一起使用。  
  
 **/Platform**选项将会减少一些问题，如果您知道您的代码将在运行的体系结构做出判定。 尤其是在下列情况下：  
  
-   如果你针对 64 位平台且应用程序在 32 位计算机上运行，则相对于不使用此开关而出现的错误，此错误消息更早出现且更加针对问题。  
  
-   如果你在选项上设置 `x86` 标志且之后应用程序在 64 位计算机上运行，则应用程序将在 WOW 子系统中运行而不是在本机上运行。  
  
 在 64 位 Windows 操作系统上：  
  
-   用 `/platform:x86` 编译的程序集将在 WOW64 下运行的 32 位 CLR 上执行。  
  
-   用 `/platform:anycpu` 编译的可执行文件将在 64 位 CLR 上执行。  
  
-   用 `/platform:anycpu` 编译的 DLL 将在加载它的进程所在的同一 CLR 上执行。  
  
-   用 `/platform:anycpu32bitpreferred` 编译的可执行文件将在 32 位 CLR 上执行。  
  
 有关如何开发 64 位版本的 Windows 上运行的应用程序的详细信息，请参阅[64 位应用程序](https://msdn.microsoft.com/library/ms241064)。  
  
### <a name="to-set-platform-in-the-visual-studio-ide"></a>若要在 Visual Studio IDE 中设置 /platform  
  
1.  在**解决方案资源管理器**，选择项目，打开**项目**菜单，然后再单击**属性**。  
  
     有关详细信息，请参阅[NIB︰ 使用项目设计器管理项目属性](http://msdn.microsoft.com/en-us/983f3c18-832f-4666-afec-74b716ff3e0e)。  
  
2.  在**编译**选项卡上，选中或清除**首选 32 位**复选框，或者，在**目标 CPU**列表中，选择一个值。  
  
     有关详细信息，请参阅[编译页，项目设计器 (Visual Basic 中)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic)。  
  
## <a name="example"></a>示例  
 下例阐释使用 `/platform` 编译器选项的方式。  
  
```  
vbc /platform:x86 myFile.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [/target (Visual Basic)](target.md)   
 [Visual Basic 命令行编译器](index.md)   
 [示例编译命令行](sample-compilation-command-lines.md)
