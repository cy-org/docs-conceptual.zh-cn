---
title: "如何：生成多文件程序集"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- assemblies [.NET Framework], multifile
- entry point for assembly
- compiling assemblies
- Al.exe
- command-line compilers
- assembly manifest, multifile assemblies
- assemblies [.NET Framework], compiling
- Assembly Linker
- code modules
- multifile assemblies
ms.assetid: 261c5583-8a76-412d-bda7-9b8ee3b131e5
caps.latest.revision: 15
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 5dd9de26f083209a0e8da79562f914023e008251
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-build-a-multifile-assembly"></a>如何：生成多文件程序集
本文章介绍如何创建多文件程序集，并提供用于说明过程中每个步骤的代码。  
  
> [!NOTE]
>  适用于 C# 和 Visual Basic 的 Visual Studio IDE 只能用于创建单文件程序集。 如果要创建多文件程序集，则必须使用命令行编译器或带有 Visual C++ 的 Visual Studio。  
  
### <a name="to-create-a-multifile-assembly"></a>创建多文件程序集  
  
1.  将包含程序集中其他模块引用的命名空间的所有文件编译成代码模块。 代码模块的默认扩展名为 .netmodule。  
  
     例如，假定 `Stringer` 文件具有一个名为 `myStringer` 的命名空间，其中包括一个名为 `Stringer` 的类。 `Stringer` 类包含名为 `StringerMethod` 的方法，此方法将单独一行写入控制台。  
  
     [!code-cpp[Conceptual.Assembly.Multifile#1](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.assembly.multifile/cpp/stringer.cpp#1)]  [!code-csharp[Conceptual.Assembly.Multifile#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.assembly.multifile/cs/stringer.cs#1)]  [!code-vb[Conceptual.Assembly.Multifile#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.assembly.multifile/vb/stringer.vb#1)]  
  
     使用下面的命令编译此代码：  
  
     [!code-cpp[Conceptual.Assembly.Multifile#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.assembly.multifile/cpp/stringer.cpp#2)]  [!code-csharp[Conceptual.Assembly.Multifile#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.assembly.multifile/cs/stringer.cs#2)]  [!code-vb[Conceptual.Assembly.Multifile#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.assembly.multifile/vb/stringer.vb#2)]  
  
     使用 **/t:** 编译器选项指定 *module* 参数，表明文件应作为模块（而不是作为程序集）编译。 编译器生成一个名为 `Stringer.netmodule` 的模块，可将其添加到程序集中。  
  
2.  编译所有其他模块，使用必要的编译器选项来表明代码中引用的其他模块。 此步骤使用 /addmodule 编译器选项。  
  
     在下面的示例中，名为 `Client` 的代码模块具有一个入口点 `Main` 方法，此方法引用步骤 1 中创建的 `Stringer.dll` 模块中的方法。  
  
     [!code-cpp[Conceptual.Assembly.Multifile#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.assembly.multifile/cpp/client.cpp#3)]  [!code-csharp[Conceptual.Assembly.Multifile#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.assembly.multifile/cs/client.cs#3)]  [!code-vb[Conceptual.Assembly.Multifile#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.assembly.multifile/vb/client.vb#3)]  
  
     使用下面的命令编译此代码：  
  
     [!code-cpp[Conceptual.Assembly.Multifile#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.assembly.multifile/cpp/client.cpp#4)]  [!code-csharp[Conceptual.Assembly.Multifile#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.assembly.multifile/cs/client.cs#4)]  [!code-vb[Conceptual.Assembly.Multifile#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.assembly.multifile/vb/client.vb#4)]  
  
     指定 /t:module 选项，因为此模块将在以后的步骤中添加到程序集。 指定 /addmodule 选项，因为 `Client` 中的代码引用 `Stringer.netmodule` 中的代码创建的命名空间。 编译器生成一个名为 `Client.netmodule` 的模块，其中包含对另一个模块 `Stringer.netmodule` 的引用。  
  
    > [!NOTE]
    >  C# 和 Visual Basic 编译器支持使用以下两种不同语法直接创建多文件程序集。  
    >   
    >  -   两次编译创建出一个双文件程序集：  
    >   
    >      [!code-cpp[Conceptual.Assembly.Multifile#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.assembly.multifile/cpp/client.cpp#5)]  [!code-csharp[Conceptual.Assembly.Multifile#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.assembly.multifile/cs/client.cs#5)]  [!code-vb[Conceptual.Assembly.Multifile#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.assembly.multifile/vb/client.vb#5)]  
    > -   一次编译创建出一个双文件程序集：  
    >   
    >      [!code-cpp[Conceptual.Assembly.Multifile#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.assembly.multifile/cpp/client.cpp#6)]   [!code-csharp[Conceptual.Assembly.Multifile#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.assembly.multifile/cs/client.cs#6)]   [!code-vb[Conceptual.Assembly.Multifile#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.assembly.multifile/vb/client.vb#6)]  
  
3.  使用[程序集链接器 (Al.exe)](../../../docs/framework/tools/al-exe-assembly-linker.md) 来创建包含程序集清单的输出文件。 此文件包含作为程序集组成部分的所有模块或资源的参考信息。  
  
     在命令提示符处，键入下列命令：  
  
     al \<module name> \<module name> … /main:\<method name> /out:\<file name> /target:\<assembly file type>  
  
     在此命令中，“module name”参数指定程序集要包含的各模块的名称。 /main: 选项指定作为程序集入口点的方法名称。 /out: 选项指定输出文件的名称，它包含程序集元数据。 /target: 选项指定程序集是控制台应用程序可执行文件 (.exe)、Windows 可执行文件 (.win) 还是库文件 (.lib)。  
  
     在下面的示例中，Al.exe 创建一个程序集，该程序集是一个控制台应用程序可执行文件，名为 `myAssembly.exe`。 该应用程序由名为 `Client.netmodule` 和 `Stringer.netmodule` 的两个模块以及名为 `myAssembly.exe,`（其中只包含程序集元数据）的可执行文件组成。 程序集的入口点是位于 `Main` 中的 `MainClientApp` 类中的 `Client.dll` 方法。  
  
    ```  
    al Client.netmodule Stringer.netmodule /main:MainClientApp.Main /out:myAssembly.exe /target:exe   
    ```  
  
     可以使用 [MSIL 反汇编程序 (Ildasm.exe)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) 来检查程序集的内容，或者确定文件是程序集还是模块。  
  
## <a name="see-also"></a>另请参阅  
 [创建程序集](../../../docs/framework/app-domains/create-assemblies.md)   
 [如何：查看程序集内容](../../../docs/framework/app-domains/how-to-view-assembly-contents.md)   
 [运行时如何定位程序集](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [多文件程序集](../../../docs/framework/app-domains/multifile-assemblies.md)

