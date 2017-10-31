---
title: "-target:exe（C# 编译器选项）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /exe
dev_langs:
- CSharp
helpviewer_keywords:
- target compiler options [C#], /target:exe
- /target compiler options [C#], /target:exe
- -target compiler options [C#], /target:exe
ms.assetid: bda5717d-1b91-4848-956b-fcf85c30e432
caps.latest.revision: 12
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
ms.openlocfilehash: bd035bffb697e895da8765f9e5d230fa84e98f04
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="targetexe-c-compiler-options"></a>/target:exe（C# 编译器选项）
**/Target: exe** 选项将使编译器创建可执行文件 (EXE) 和控制台应用程序。  
  
## <a name="syntax"></a>语法  
  
```console  
/target:exe  
```  
  
## <a name="remarks"></a>备注  
 默认情况下，**/target:exe** 选项有效。 将创建扩展名为 .exe 的可执行文件。  
  
 使用 [/target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md) 创建 Windows 程序可执行文件。  
  
 除非使用 [/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md) 选项进行指定，否则输出文件名采用包含 [Main](../../../csharp/programming-guide/main-and-command-args/index.md) 方法的输入文件的名称。  
  
 在命令行中进行指定时，**/out** 或 **/target:module** 选项上所有文件都用于创建 .exe 文件  
  
 编译为 .exe 文件的源代码文件中只需要一个 **Main** 方法。 如果代码具有多个附带 **Main** 方法的类，则可使用 [/main](../../../csharp/language-reference/compiler-options/main-compiler-option.md) 编译器选项指定包含 **Main** 方法的类。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的“属性”页。  
  
2.  单击“应用程序”属性页。  
  
3.  修改“输出类型”属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参阅 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>。  
  
## <a name="example"></a>示例  
 以下每个命令行都将编译 `in.cs` 并创建 `in.exe`：  
  
```console  
csc /target:exe in.cs  
csc in.cs  
```  
  
## <a name="see-also"></a>请参阅  
 [/target（C# 编译器选项）](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [C# 编译器选项](../../../csharp/language-reference/compiler-options/index.md)

