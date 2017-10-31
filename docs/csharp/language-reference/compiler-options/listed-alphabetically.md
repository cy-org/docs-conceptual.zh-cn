---
title: "按字母顺序列出的 C# 编译器选项"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- compiler options [C#], listed alpabetically
- C# language, compiler options listed alphabitically
- Visual C# compiler, options listed alphabetically
- Visual C#, compiler options listed alphabetically
ms.assetid: 43535ea0-ca47-4a15-b528-615087a86092
caps.latest.revision: 25
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
ms.openlocfilehash: 8a32dcab0a64fdb715871806088825e227f08abb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/19/2017

---
# <a name="c-compiler-options-listed-alphabetically"></a>按字母顺序列出的 C# 编译器选项
下列编译器选项按字母顺序排序。 有关按类别排序的列表，请参 [按类别列出的 C# 编译器选项](../../../csharp/language-reference/compiler-options/listed-by-category.md)。  
  
|选项|用途|  
|------------|-------------|  
|[@](../../../csharp/language-reference/compiler-options/response-file-compiler-option.md)|有关更多选项，请阅读响应文件。|  
|[/?](../../../csharp/language-reference/compiler-options/help-compiler-option.md)|向 stdout 显示用法消息。|  
|/additionalfile|命名其他文件，这些文件不会直接影响代码生成，但可能由分析器用于生成错误或警告。|  
|[/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md)|将指定的模块链接到此程序集中|  
|/analyzer|从此程序集（缩写形式：/a）运行分析器|  
|[/appconfig](../../../csharp/language-reference/compiler-options/appconfig-compiler-option.md)|在程序集绑定时指定 app.config 的位置。|  
|[/baseaddress](../../../csharp/language-reference/compiler-options/baseaddress-compiler-option.md)|指定要生成的库的基址。|  
|[/bugreport](../../../csharp/language-reference/compiler-options/bugreport-compiler-option.md)|创建“Bug 报告”文件。 如果与 /errorreport:prompt 或 /errorreport:send 一起使用，则此文件会与任何崩溃信息一起发送。|  
|[/checked](../../../csharp/language-reference/compiler-options/checked-compiler-option.md)|使编译器生成溢出检查。|  
|/checksumalgorithm:\<alg>|指定用于计算 PDB 中存储的源文件校验和的算法。  支持的值为：SHA1（默认值）或 SHA256。|  
|[/codepage](../../../csharp/language-reference/compiler-options/codepage-compiler-option.md)|指定在打开源文件时使用的代码页。|  
|[/debug](../../../csharp/language-reference/compiler-options/debug-compiler-option.md)|发出调试信息。|  
|[/define](../../../csharp/language-reference/compiler-options/define-compiler-option.md)|定义条件编译符号。|  
|[/delaysign](../../../csharp/language-reference/compiler-options/delaysign-compiler-option.md)|仅使用强名称密钥公共部分对程序集进行延迟签名。|  
|[/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)|指定要生成的 XML 文档文件。|  
|[/errorreport](../../../csharp/language-reference/compiler-options/errorreport-compiler-option.md)|指定如何处理内部编译器错误；prompt、send 或 none。 默认值为 none。|  
|[/filealign](../../../csharp/language-reference/compiler-options/filealign-compiler-option.md)|指定用于输出文件节的对齐方式。|  
|[/fullpaths](../../../csharp/language-reference/compiler-options/fullpaths-compiler-option.md)|使编译器生成完全限定的路径。|  
|[/help](../../../csharp/language-reference/compiler-options/help-compiler-option.md)|向 stdout 显示用法消息。|  
|[/highentropyva](../../../csharp/language-reference/compiler-options/highentropyva-compiler-option.md)|指定支持高熵 ASLR。|  
|/incremental|启用增量编译 [已过时]。|  
|[/keycontainer](../../../csharp/language-reference/compiler-options/keycontainer-compiler-option.md)|指定强名称密钥容器。|  
|[/keyfile](../../../csharp/language-reference/compiler-options/keyfile-compiler-option.md)|指定强名称密钥文件。|  
|[/langversion:\<string>](../../../csharp/language-reference/compiler-options/langversion-compiler-option.md)|指定语言版本模式：默认、ISO-1、ISO-2、3、4、5、6、7、7.1 或最新 |  
|[/lib](../../../csharp/language-reference/compiler-options/lib-compiler-option.md)|指定要在其中搜索引用的附加目录。|  
|[/link](../../../csharp/language-reference/compiler-options/link-compiler-option.md)|使指定程序集中的 COM 类型信息对项目可用。|  
|[/linkresource](../../../csharp/language-reference/compiler-options/linkresource-compiler-option.md)|将指定的资源链接到此程序集。|  
|[/main](../../../csharp/language-reference/compiler-options/main-compiler-option.md)|指定包含入口点的类型（忽略所有其他可能的入口点）。|  
|[/moduleassemblyname](../../../csharp/language-reference/compiler-options/moduleassemblyname-compiler-option.md)|指定一个程序集，.netmodule 可以访问其非公共类型。|  
|/modulename:\<string>|指定源模块的名称|  
|[/noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md)|指示编译器不自动包含 CSC.RSP 文件。|  
|[/nologo](../../../csharp/language-reference/compiler-options/nologo-compiler-option.md)|取消编译器版权消息。|  
|[/nostdlib](../../../csharp/language-reference/compiler-options/nostdlib-compiler-option.md)|指示编译器不引用标准库 (mscorlib.dll)。|  
|[/nowarn](../../../csharp/language-reference/compiler-options/nowarn-compiler-option.md)|禁用特定的警告消息|  
|[/nowin32manifest](../../../csharp/language-reference/compiler-options/nowin32manifest-compiler-option.md)|指示编译器不在可执行文件中嵌入应用程序清单。|  
|[/optimize](../../../csharp/language-reference/compiler-options/optimize-compiler-option.md)|启用/禁用优化。|  
|[/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md)|指定输出文件名（默认值：包含主类的文件或第一个文件的基名称）。|  
|/parallel[+&#124;-]|指定是否使用并发生成 (+)。|  
|[/pdb](../../../csharp/language-reference/compiler-options/pdb-compiler-option.md)|指定 .pdb 文件的文件名和位置。|  
|[/platform](../../../csharp/language-reference/compiler-options/platform-compiler-option.md)|限定此代码可以在其上运行的平台：x86、Itanium、x64 、anycpu 或 anycpu32bitpreferred。 默认值为 anycpu。|  
|[/preferreduilang](../../../csharp/language-reference/compiler-options/preferreduilang-compiler-option.md)|指定要用于编译器输出的语言。|  
|[/recurse](../../../csharp/language-reference/compiler-options/recurse-compiler-option.md)|根据通配符规范，包括当前目录及子目录下的所有文件。|  
|[/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)|从指定的程序集文件引用元数据。|  
|[/refout](refout-compiler-option.md)|除主程序集之外，还生成引用程序集。|  
|[/refonly](refonly-compiler-option.md)|生成引用程序集，而不生成主程序集。|  
|[/resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md)|嵌入指定的资源。|  
|/ruleset:\<file>|指定可禁用特定诊断的规则集文件。|  
|[/subsystemversion](../../../csharp/language-reference/compiler-options/subsystemversion-compiler-option.md)|指定可执行文件可以使用的子系统的最低版本。|  
|[/target](../../../csharp/language-reference/compiler-options/target-compiler-option.md)|使用下列四个选项之一指定输出文件的格式：[/target:appcontainerexe](../../../csharp/language-reference/compiler-options/target-appcontainerexe-compiler-option.md)、[/target:exe](../../../csharp/language-reference/compiler-options/target-exe-compiler-option.md)、[/target:library](../../../csharp/language-reference/compiler-options/target-library-compiler-option.md)、[/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md)、[/target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md)、[/target:winmdobj](../../../csharp/language-reference/compiler-options/target-winmdobj-compiler-option.md)。|  
|[/unsafe](../../../csharp/language-reference/compiler-options/unsafe-compiler-option.md)|允许[不安全](../../../csharp/language-reference/keywords/unsafe.md)代码。|  
|[/utf8output](../../../csharp/language-reference/compiler-options/utf8output-compiler-option.md)|以 UTF-8 编码格式输出编译器消息。|  
|[/warn](../../../csharp/language-reference/compiler-options/warn-compiler-option.md)|设置警告等级 (0-4)。|  
|[/warnaserror](../../../csharp/language-reference/compiler-options/warnaserror-compiler-option.md)|将特定警告报告为错误。|  
|[/win32icon](../../../csharp/language-reference/compiler-options/win32icon-compiler-option.md)|对输出使用此图标。|  
|[/win32manifest](../../../csharp/language-reference/compiler-options/win32manifest-compiler-option.md)|指定自定义 win32 清单文件。|  
|[/win32res](../../../csharp/language-reference/compiler-options/win32res-compiler-option.md)|指定 win32 资源文件 (.res)。|  
  
## <a name="see-also"></a>另请参阅  
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [按类别列出的 C# 编译器选项](../../../csharp/language-reference/compiler-options/listed-by-category.md)   
 [如何：为 Visual Studio 命令行设置环境变量](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)   
 [\<compiler> Element](../../../framework/configure-apps/file-schema/compiler/compiler-element.md)

