---
title: "按类别列出的 C# 编译器选项"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- Visual C# compiler, options listed by category
- compiler options [C#], listed by category
- Visual C#, compiler options listed by category
ms.assetid: 96437ecc-6502-4cd3-b070-e9386a298e83
caps.latest.revision: 17
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: HT
ms.sourcegitcommit: 8e8d01587ccde967b8484b3b61916f8cf437f6c0
ms.openlocfilehash: 584d0cb249644e6b4ffe15e115c49256f5fa2716
ms.contentlocale: zh-cn
ms.lasthandoff: 08/14/2017

---
# <a name="c-compiler-options-listed-by-category"></a>按类别列出的 C# 编译器选项
下列编译器选项按类别排序。 关于按字母顺序排列的列表，请参阅[按字母顺序列出的 C# 编译器选项](../../../csharp/language-reference/compiler-options/listed-alphabetically.md)。  
  
### <a name="optimization"></a>优化  
  
|选项|目标|  
|------------|-------------|  
|[/filealign](../../../csharp/language-reference/compiler-options/filealign-compiler-option.md)|指定输出文件中各节的大小。|  
|[/optimize](../../../csharp/language-reference/compiler-options/optimize-compiler-option.md)|启用/禁用优化。|  
  
### <a name="output-files"></a>输出文件  
  
|选项|用途|  
|------------|-------------|  
|[/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)|指定要将已处理的文档注释写入到的 XML 文件。|  
|[/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md)|指定输出文件。|  
|[/pdb](../../../csharp/language-reference/compiler-options/pdb-compiler-option.md)|指定 .pdb 文件的文件名和位置。|  
|[/platform](../../../csharp/language-reference/compiler-options/platform-compiler-option.md)|指定输出平台。|  
|[/preferreduilang](../../../csharp/language-reference/compiler-options/preferreduilang-compiler-option.md)|指定编译器输出的语言。|  
|[/refout](refout-compiler-option.md)|除主程序集之外，还生成引用程序集。|  
|[/refonly](refonly-compiler-option.md)|生成引用程序集，而不生成主程序集。|  
|[/target](../../../csharp/language-reference/compiler-options/target-compiler-option.md)|使用下列五个选项之一指定输出文件的格式：[/target:appcontainerexe](../../../csharp/language-reference/compiler-options/target-appcontainerexe-compiler-option.md)、[/target:exe](../../../csharp/language-reference/compiler-options/target-exe-compiler-option.md)、[/target:library](../../../csharp/language-reference/compiler-options/target-library-compiler-option.md)、[/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md)、[/target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md) 或 [/target:winmdobj](../../../csharp/language-reference/compiler-options/target-winmdobj-compiler-option.md)。|  
|/modulename:\<string>|指定源模块的名称|  
  
### <a name="net-framework-assemblies"></a>.NET Framework 程序集  
  
|选项|目标|  
|------------|-------------|  
|[/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md)|指定一个或多个模块作为此程序集的一部分。|  
|[/delaysign](../../../csharp/language-reference/compiler-options/delaysign-compiler-option.md)|指示编译器添加公钥，但将此程序集保留为未签名状态。|  
|[/keycontainer](../../../csharp/language-reference/compiler-options/keycontainer-compiler-option.md)|指定加密密钥容器的名称。|  
|[/keyfile](../../../csharp/language-reference/compiler-options/keyfile-compiler-option.md)|指定包含加密密钥的文件名。|  
|[/lib](../../../csharp/language-reference/compiler-options/lib-compiler-option.md)|指定通过 [/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md) 的方式引用的程序集的位置。|  
|[/nostdlib](../../../csharp/language-reference/compiler-options/nostdlib-compiler-option.md)|指示编译器不导入标准库 (mscorlib.dll)。|  
|[/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)|从包含程序集的文件导入元数据。|  
|/analyzer|从此程序集（缩写形式：/a）运行分析器|  
|/additionalfile|命名其他文件，这些文件不会直接影响代码生成，但可能由分析器用于生成错误或警告。|  
  
### <a name="debuggingerror-checking"></a>调试/错误检查  
  
|选项|目标|  
|------------|-------------|  
|[/bugreport](../../../csharp/language-reference/compiler-options/bugreport-compiler-option.md)|创建一个文件，其中包含可以轻松报告 bug 的信息。|  
|[/checked](../../../csharp/language-reference/compiler-options/checked-compiler-option.md)|指定溢出数据类型边界的整数算法是否将导致运行时异常。|  
|[/debug](../../../csharp/language-reference/compiler-options/debug-compiler-option.md)|指示编译器发出调试信息。|  
|[/errorreport](../../../csharp/language-reference/compiler-options/errorreport-compiler-option.md)|设置错误报告行为。|  
|[/fullpaths](../../../csharp/language-reference/compiler-options/fullpaths-compiler-option.md)|指定编译器输出中文件的绝对路径。|  
|[/nowarn](../../../csharp/language-reference/compiler-options/nowarn-compiler-option.md)|取消编译器对指定警告的生成。|  
|[/warn](../../../csharp/language-reference/compiler-options/warn-compiler-option.md)|设置警告等级。|  
|[/warnaserror](../../../csharp/language-reference/compiler-options/warnaserror-compiler-option.md)|将警告提升为错误。|  
|/ruleset:\<file>|指定可禁用特定诊断的规则集文件。|  
  
### <a name="preprocessor"></a>预处理器  
  
|选项|目标|  
|------------|-------------|  
|[/define](../../../csharp/language-reference/compiler-options/define-compiler-option.md)|定义预处理器符号。|  
  
### <a name="resources"></a>资源  
  
|选项|目标|  
|------------|-------------|  
|[/link](../../../csharp/language-reference/compiler-options/link-compiler-option.md)|使指定程序集中的 COM 类型信息对项目可用。|  
|[/linkresource](../../../csharp/language-reference/compiler-options/linkresource-compiler-option.md)|创建指向托管资源的链接。|  
|[/resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md)|将 .NET Framework 资源嵌入到输出文件。|  
|[/win32icon](../../../csharp/language-reference/compiler-options/win32icon-compiler-option.md)|指定要插入到输出文件的 .ico 文件。|  
|[/win32res](../../../csharp/language-reference/compiler-options/win32res-compiler-option.md)|指定要插入到输出文件的 Win32 资源。|  
  
### <a name="miscellaneous"></a>杂项  
  
|选项|目的|  
|------------|-------------|  
|[@](../../../csharp/language-reference/compiler-options/response-file-compiler-option.md)|指定响应文件。|  
|[/?](../../../csharp/language-reference/compiler-options/help-compiler-option.md)|列出到 stdout 的编译器选项。|  
|[/baseaddress](../../../csharp/language-reference/compiler-options/baseaddress-compiler-option.md)|指定要加载 DLL 的首选基址。|  
|[/codepage](../../../csharp/language-reference/compiler-options/codepage-compiler-option.md)|指定要用于编译中所有源代码文件的代码页。|  
|[/help](../../../csharp/language-reference/compiler-options/help-compiler-option.md)|列出到 stdout 的编译器选项。|  
|[/highentropyva](../../../csharp/language-reference/compiler-options/highentropyva-compiler-option.md)|指定可执行文件支持地址空间布局随机化 (ASLR)。|  
|[/langversion](../../../csharp/language-reference/compiler-options/langversion-compiler-option.md)|指定语言版本模式：默认、ISO-1、ISO-2、3、4、5、6、7、7.1 或最新 |  
|[/main](../../../csharp/language-reference/compiler-options/main-compiler-option.md)|指定 Main 方法的位置。|  
|[/noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md)|指示编译器不使用 csc.rsp 进行编译。|  
|[/nologo](../../../csharp/language-reference/compiler-options/nologo-compiler-option.md)|禁止显示编译器横幅信息。|  
|[/recurse](../../../csharp/language-reference/compiler-options/recurse-compiler-option.md)|搜索要编译的源文件的子目录。|  
|[/subsystemversion](../../../csharp/language-reference/compiler-options/subsystemversion-compiler-option.md)|指定可执行文件可以使用的子系统的最低版本。|  
|[/unsafe](../../../csharp/language-reference/compiler-options/unsafe-compiler-option.md)|启用使用 [unsafe](../../../csharp/language-reference/keywords/unsafe.md) 关键字的代码编译。|  
|[/utf8output](../../../csharp/language-reference/compiler-options/utf8output-compiler-option.md)|显示使用 UTF-8 编码的编译器输出。|  
|/parallel[+&#124;-]|指定是否使用并发生成 (+)。|  
|/checksumalgorithm:\<alg>|指定用于计算 PDB 中存储的源文件校验和的算法。  支持的值为：SHA1（默认值）或 SHA256。|  
  
## <a name="obsolete-options"></a>已过时的选项  
  
|选项|目标|  
|---|---|  
|/incremental|启用增量编译。|  
  
## <a name="see-also"></a>另请参阅  
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [按字母顺序列出的 C# 编译器选项](../../../csharp/language-reference/compiler-options/listed-alphabetically.md)   
 [如何：为 Visual Studio 命令行设置环境变量](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)

