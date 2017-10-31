---
title: "程序集和全局程序集缓存 (Visual Basic)"
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
ms.assetid: fcf78ff1-f1ab-4a5d-b6d8-00d2046b6c80
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c5a1a3a651fc7d2b42f8ac55ab6f2d832f258bb0
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="assemblies-and-the-global-assembly-cache-visual-basic"></a>程序集和全局程序集缓存 (Visual Basic)
程序集构成了 .NET 应用程序的部署、版本控制、重用、激活范围和安全权限的基本单元。 作为 .NET Framework 的构建基块，程序集采用可执行文件 (.exe) 或动态链接库文件 (.dll) 的形式。 它们向公共语言运行时提供了注意类型实现代码所需的信息。 可以将程序集视为一组构成功能逻辑单元并旨在配合使用的类型和资源。  
  
 程序集可以包含一个或多个模块。 例如，可以将大型项目规划为，由多个开发者单独开发各个模块，最后将所有这些模块整合成一个程序集。 有关模块的详细信息，请参阅主题[如何：生成多文件程序集](https://msdn.microsoft.com/library/226t7yxe)。  
  
 程序集具有以下属性：  
  
-   程序集以 .exe 或 .dll 文件的形式实现。  
  
-   可以将程序集放入全局程序集缓存，以便在应用程序之间共用程序集。 必须先为程序集命名强名称，然后才能将其添加到全局程序集缓存中。 有关详细信息，请参阅[具有强名称的程序集](https://msdn.microsoft.com/library/wd40t7ad)。  
  
-   只有在需要使用时才会将程序集加载到内存中。 如果不使用，就不会加载程序集。 也就是说，使用程序集，可以在大型项目中高效管理资源。  
  
-   可以使用反射，以编程方式获取程序集的相关信息。 有关详细信息，请参阅[反射 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md)。  
  
-   如果想加载一个程序集以仅对其进行检查，请使用如 <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A> 之类的方法。  
  
## <a name="assembly-manifest"></a>程序集清单  
 每个程序集中都有*程序集清单*。 与目录类似，程序集清单包含以下内容：  
  
-   程序集的标识（名称和版本）。  
  
-   文件表，描述构成程序集的其他所有文件（例如，.exe 或 .dll 文件依赖的其他任何程序集、位图或自述文件）。  
  
-   *程序集引用列表*，列出了应用程序需要的可能由其他人创建的所有外部依赖项（.dll 或其他文件）。 程序集既可以引用全局对象，也可以引用私有对象。 全局对象驻留在全局程序集缓存中，此区域对其他应用程序也可用，类似于 System32 目录。 <xref:Microsoft.VisualBasic?displayProperty=fullName> 命名空间是全局程序集缓存中的程序集示例。 私有对象必须位于级别不高于应用程序安装目录的目录中。  
  
 由于程序集包含内容、版本控制和依赖项的相关信息，因此使用 Visual Basic 创建的应用程序并不依赖 Windows 注册表值才能正常运行。 程序集减少了 .dll 冲突，让应用程序变得更可靠、更易于部署。 在许多情况下，只需将 .NET 应用程序的文件复制到目标计算机，即可进行安装。  
  
 有关详细信息，请参阅[程序集清单](https://msdn.microsoft.com/library/1w45z383)。  
  
## <a name="adding-a-reference-to-an-assembly"></a>添加对程序集的引用  
 必须添加对程序集的引用，才能使用程序集。 接下来，使用 [Imports 语句](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)选择要使用的项的命名空间。 引用并导入程序集后，所有可访问的类、属性、方法和命名空间的其他成员都可供应用程序使用，就像其代码属于源文件一样。  
  
## <a name="creating-an-assembly"></a>创建程序集  
 使用命令行编译器通过命令行生成应用程序，从而编译应用程序。 若要详细了解如何通过命令行生成程序集，请参阅[通过命令行生成](../../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)。  
  
> [!NOTE]
>  若要在 Visual Studio 中生成程序集，请选择“生成”菜单上的“生成”。  
  
## <a name="see-also"></a>另请参阅  
 [公共语言运行时中的程序集](https://msdn.microsoft.com/library/k3677y81)   
 [友元程序集 (Visual Basic)](friend-assemblies.md)   
 [如何：与其他应用程序共享程序集 (Visual Basic)](how-to-share-an-assembly-with-other-applications.md)   
 [如何：加载和卸载程序集 (Visual Basic)](how-to-load-and-unload-assemblies.md)   
 [如何：确定文件是否为程序集 (Visual Basic)](how-to-determine-if-a-file-is-an-assembly.md)   
 [如何：使用命令行创建和使用程序集 (Visual Basic)](how-to-create-and-use-assemblies-using-the-command-line.md)   
 [演练：在 Visual Studio 中嵌入托管程序集中的类型 (Visual Basic)](walkthrough-embedding-types-from-managed-assemblies-in-vs.md)   
 [演练：在 Visual Studio 中嵌入 Microsoft Office 程序集中的类型信息 (Visual Basic)](walkthrough-embedding-type-information-from-microsoft-office-assemblies-in-vs.md)

