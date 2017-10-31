---
title: "令映像更易于调试"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- images [.NET Framework], debugging
- executable image for debugging
- debugging [.NET Framework], executable images for
ms.assetid: 7d90ea7a-150f-4f97-98a7-f9c26541b9a3
caps.latest.revision: 13
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: e844cde5f33c1accb8addf953b5a72415f4dc301
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="making-an-image-easier-to-debug"></a>令映像更易于调试
编译非托管代码时，可以通过设置 IDE 开关或命令线选项来配置可执行映像进行调试。 例如，可以使用 Visual C++ 中的 /Zi 命令行选项，使其发出调试符号文件（文件扩展名为 .pdb）。 同样，/Od 命令行选项告知编译器禁用优化。 所产生的代码运行速度更慢，但更易于调试，这很必要。  
  
 编译 .NET Framework 托管代码时，Visual C ++、Visual Basic 和 C# 等编译器将它们的源程序编译成 Microsoft 中间语言 (MSIL)。 随后，在执行前将 MSIL 实时编译为本机代码。 与非托管代码一样，可以通过设置 IDE 开关或命令行选项来配置可执行映像进行调试。 此外，可采用大致相同的方式配置 JIT 编译进行调试。  
  
 这种 JIT 配置具有两个方面：  
  
-   可以请求 JIT 编译器生成跟踪信息。 这使调试程序能将 MSIL 链与其机器码对应项相匹配，并跟踪存储本地变量和函数参数的位置。  在 .NET Framework 2.0 版中，JIT 编译器将始终生成跟踪信息，因此无需进行请求。  
  
-   可以请求 JIT 编译器不优化生成的计算机代码。  
  
 通常，生成 MSIL 的编译器根据指定的 IDE 开关或命令行选项（例如 /Od）适当地设置这些 JIT 编译器选项。  
  
 某些情况下，可能需要更改 JIT 编译器的行为，使其生成的机器码更易于调试。 例如，可能希望为零售版本或控制优化生成实时跟踪信息。 可以使用初始化 (.ini) 文件来执行此操作。  
  
 例如，如果要调试的程序集名为 MyApp.exe，则可在 MyApp.exe 所在的文件夹创建名为 MyApp.ini 的文本文件，其中包含以下三行：  
  
```  
[.NET Framework Debugging Control]  
GenerateTrackingInfo=1  
AllowOptimize=0  
```  
  
 可将每个选项的值设置为 0 或 1，任何不存在选项默认为 0。 将 `GenerateTrackingInfo` 设为 1、`AllowOptimize` 设为 0，这可提供最简单的调试。  
  
> [!NOTE]
>  在 .NET Framework 2.0 版中，无论 `GenerateTrackingInfo` 的值为多少，JIT 编译器始终生成跟踪信息；但是，`AllowOptimize` 值仍产生影响。 如果使用 [Ngen.exe（本机映像生成器）](../../../docs/framework/tools/ngen-exe-native-image-generator.md)预编译本机映像而不进行优化，Ngen.exe 执行时 .ini 文件必须存在于 `AllowOptimize=0` 的目标文件夹。 如果已经预编译程序集而不进行优化，则必须使用 NGen.exe /uninstall 选项删除预编译的代码，才能重新运行 Ngen.exe 将代码预编译为优化。 如果文件夹中不存在 .ini 文件，则默认 Ngen.exe 将代码预编译为优化。  
  
> [!NOTE]
>  <xref:System.Diagnostics.DebuggableAttribute?displayProperty=fullName> 控制程序集的设置。 DebuggableAttribute 包括两个字段，用于记录 JIT 编译器是否应优化和/或生成跟踪信息的设置。 在 .NET Framework 2.0 版本中，JIT 编译器将始终生成跟踪信息。  
  
> [!NOTE]
>  对于零售版本，编译器不设置任何 DebuggableAttribute。 JIT 编译器的默认行为是生成最高性能最难调试的机器码。 启用实时跟踪会稍微降低性能，禁用优化会极大降低性能。  
  
> [!NOTE]
>  DebuggableAttribute 一次应用于整个程序集，而不是应用于程序集中的单个模块。 因此，开发工具必须将自定义属性附加到程序集元数据令牌，如果已经创建程序集，则附加到名为 System.Runtime.CompilerServices.AssemblyAttributesGoHere 的类。 然后，ALink 工具将这些 DebuggableAttribute 属性从每个模块提升至它们将属于的程序集。 如果存在冲突，ALink 操作将失败。  
  
> [!NOTE]
>  在 .NET Framework 1.0 版本中，当指定 /clr 和 /Zi 编译器选项时，Microsoft Visual C++ 编译器将添加 DebuggableAttribute。 在 .NET Framework 1.1 版本中，必须在代码中手动添加 DebugabbleAttribute，或者使用 /ASSEMBLYDEBUG 链接器选项。  
  
## <a name="see-also"></a>另请参阅  
 [调试、跟踪和分析](../../../docs/framework/debug-trace-profile/index.md)   
 [启用 JIT 附加调试](../../../docs/framework/debug-trace-profile/enabling-jit-attach-debugging.md)   
 [启用分析](http://msdn.microsoft.com/en-us/3b669676-f0e0-4ebf-8674-68986dd2020d)

