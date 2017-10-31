---
title: "@（C# 编译器选项）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- '@'
dev_langs:
- CSharp
helpviewer_keywords:
- response files, specifying for compilation [C#]
- '@ compiler option'
ms.assetid: dda4fa9f-a02c-400f-8b6a-d58834e13d7f
caps.latest.revision: 9
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
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 219c12e4e3c9b847400f00a135d58506c72d2e7f
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="-c-compiler-options"></a>@（C# 编译器选项）
通过 @ 选项，可以指定包含编译器选项和要编译的源代码文件的文件。  
  
## <a name="syntax"></a>语法  
  
```  
@response_file  
```  
  
## <a name="arguments"></a>参数  
 `response_file`  
 列出了编译器选项或要编译的源代码文件的文件。  
  
## <a name="remarks"></a>备注  
 编译器选项和源代码文件将由编译器处理，如同在命令行被指定一样。  
  
 若要在一次编译中指定多个响应文件，请指定多个响应文件选项。 例如：  
  
```  
@file1.rsp @file2.rsp  
```  
  
 在响应文件中，多个编译器选项和源代码文件可以出现在同一行中。 单个编译器选项的指定必须出现在同一行中（不能跨行）。 响应文件的注释可以 # 符号开始。  
  
 从响应文件内指定编译器选项就如同在命令行发出这些命令。 有关详细信息，请参阅[从命令行生成](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)。  
  
 编译器在遇到命令选项时会进行处理。 因此，命令行参数可以重写先前在响应文件中列出的选项。 反之，响应文件中的选项也将重写先前在命令行或其他响应文件中列出的选项。  
  
 C# 提供 csc.rsp 文件，该文件与 csc.exe 文件位于同一目录。 有关 csc.rsp 的详细信息，请参阅 [/noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md)。  
  
 不能在 Visual Studio 开发环境中设置此编译器选项，也不能以编程方式对其进行更改。  
  
## <a name="example"></a>示例  
 以下几行来自示例响应文件：  
  
```console  
# build the first output file  
/target:exe /out:MyExe.exe source1.cs source2.cs  
```  
  
## <a name="see-also"></a>另请参阅  
 [C# 编译器选项](../../../csharp/language-reference/compiler-options/index.md)

