---
title: "如何：查看程序集内容"
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
- assembly manifest, viewing information
- Ildasm.exe
- MSIL Disassembler
- assemblies [.NET Framework], viewing contents
- viewing assembly information
- MSIL
- viewing MSIL information
ms.assetid: fb7baaab-4c0d-47ad-8fd3-4591cf834709
caps.latest.revision: 11
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 3583e69e90080eb830bb61a5e0c7b6e944f7d654
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-view-assembly-contents"></a>如何：查看程序集内容
可使用 [Ildasm.exe（IL 反汇编程序）](../../../docs/framework/tools/ildasm-exe-il-disassembler.md)查看文件中的 Microsoft 中间语言 (MSIL) 信息。 如果要检查的文件是程序集，此信息可包括程序集的属性以及对其他模块和程序集的引用。 此信息有助于确定文件是程序集还是程序集的一部分，以及文件是否具有对其他模块或程序集的引用。  
  
### <a name="to-display-the-contents-of-an-assembly-using-ildasmexe"></a>使用 Ildasm.exe 显示程序集的内容  
  
1.  在命令提示符处键入 ildasm \<assembly name>。 例如，以下命令反汇编 `Hello.exe` 程序集。  
  
    ```  
    ildasm Hello.exe  
    ```  
  
### <a name="to-view-assembly-manifest-information"></a>查看程序集清单信息  
  
1.  在“MSIL 反汇编程序”窗口双击“清单”图标。  
  
## <a name="example"></a>示例  
 下例以基本的“Hello, World”程序开始。 编译该程序后，使用 Ildasm.exe 反汇编 Hello.exe 程序集并查看程序集清单。  
  
 [!code-cpp[Conceptual.Assembly.Contents#1](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.assembly.contents/cpp/source.cpp#1)] [!code-csharp[Conceptual.Assembly.Contents#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.assembly.contents/cs/source.cs#1)] [!code-vb[Conceptual.Assembly.Contents#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.assembly.contents/vb/source.vb#1)]  
  
 在 Hello.exe 程序集上运行 ildasm.exe 命令，然后在 IL DASM 窗口中双击“清单”图标生成以下输出：  
  
```  
// Metadata version: v4.0.30319  
.assembly extern mscorlib  
{  
  .publickeytoken = (B7 7A 5C 56 19 34 E0 89 )                         // .z\V.4..  
  .ver 4:0:0:0  
}  
.assembly Hello  
{  
  .custom instance void [mscorlib]System.Runtime.CompilerServices.CompilationRelaxationsAttribute::.ctor(int32) = ( 01 00 08 00 00 00 00 00 )   
  .custom instance void [mscorlib]System.Runtime.CompilerServices.RuntimeCompatibilityAttribute::.ctor() = ( 01 00 01 00 54 02 16 57 72 61 70 4E 6F 6E 45 78   // ....T..WrapNonEx  
                                                                                                             63 65 70 74 69 6F 6E 54 68 72 6F 77 73 01 )       // ceptionThrows.  
  .hash algorithm 0x00008004  
  .ver 0:0:0:0  
}  
.module Hello.exe  
// MVID: {7C2770DB-1594-438D-BAE5-98764C39CCCA}  
.imagebase 0x00400000  
.file alignment 0x00000200  
.stackreserve 0x00100000  
.subsystem 0x0003       // WINDOWS_CUI  
.corflags 0x00000001    //  ILONLY  
// Image base: 0x00600000  
```  
  
 下表描述了本例所使用 Hello.exe 程序集的程序集清单中的各项指令。  
  
|指令|描述|  
|---------------|-----------------|  
|.assembly extern \< assembly name >|指定包含当前模块所引用项目的另一程序集（在此示例中为 `mscorlib`）。|  
|.publickeytoken \< token >|指定引用程序集的实际密钥的标记。|  
|.ver \< version number >|指定引用程序集的版本号。|  
|.assembly \< assembly name >|指定程序集名称。|  
|.hash algorithm \< int32 value >|指定使用的哈希算法。|  
|.ver \< version number >|指定程序集的版本号。|  
|.module \< file name >|指定组成程序集的模块名称。 在此示例中，程序集只包含一个文件。|  
|.subsystem \< value >|指定程序要求的应用程序环境。 在此示例中，值 3 表示该可执行文件从控制台运行。|  
|.corflags|当前是元数据中的一个保留字段。|  
  
 根据程序集的内容，程序集清单可包含许多不同的指令。 有关程序集清单中指令的详尽列表，请参阅 ECMA 文档，特别是“Partition II: Metadata Definition and Semantics”（第 2 部分：元数据定义和语义）和“Partition III: CIL Instruction Set”（第 3 部分：CIL 指令集）。 可联机获取该文档；请参阅 MSDN 上的 [ECMA C# 和公共语言基础结构标准](http://go.microsoft.com/fwlink/?LinkID=99212)和 Ecma International 网站上的[标准 ECMA-335 - 公共语言基础结构 (CLI)](http://go.microsoft.com/fwlink/?LinkID=65552)。  
  
## <a name="see-also"></a>另请参阅  
 [应用程序域和程序集](http://msdn.microsoft.com/en-us/433b04ae-4ba8-4849-9dbd-79194f240346)   
 [应用程序域和程序集用法主题](../../../docs/framework/app-domains/application-domains-and-assemblies-how-to-topics.md)   
 [Ildasm.exe（IL 反汇编程序）](../../../docs/framework/tools/ildasm-exe-il-disassembler.md)

