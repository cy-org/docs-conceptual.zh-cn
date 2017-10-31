---
title: "-target:winexe（C# 编译器选项）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /target:winexe
dev_langs:
- CSharp
helpviewer_keywords:
- /target compiler options [C#], /target:winexe
- -target compiler options [C#], /target:winexe
- target compiler options [C#], /target:winexe
ms.assetid: b5a0619c-8caa-46a5-a743-1cf68408ad7a
caps.latest.revision: 11
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
ms.openlocfilehash: afb49fc6d45cc904c97988ab1b569f37a4e44a51
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="targetwinexe-c-compiler-options"></a>/target:winexe（C# 编译器选项）
**/target:winexe** 选项将使编译器创建可执行文件 (EXE) 和 Windows 程序。  
  
## <a name="syntax"></a>语法  
  
```console  
/target:winexe  
```  
  
## <a name="remarks"></a>备注  
 将创建扩展名为 .exe 的可执行文件。 Windows 程序从 .NET Framework 库或使用 Win32 API 提供用户界面。  
  
 使用 [/target:exe](../../../csharp/language-reference/compiler-options/target-exe-compiler-option.md) 创建控制台应用程序。  
  
 除非使用 [/out](../../../csharp/language-reference/compiler-options/out-compiler-option.md) 选项进行指定，否则输出文件名采用包含 [Main](../../../csharp/programming-guide/main-and-command-args/index.md) 方法的输入文件的名称。  
  
 在命令行中进行指定时，直到下一个 **/out** 或 [/target](../../../csharp/language-reference/compiler-options/target-compiler-option.md) 选项为止的所有文件均用于创建 Windows 程序。  
  
 编译为 .exe 文件的源代码文件中只需要一个 **Main** 方法。 如果代码具有多个附带 **Main** 方法的类，则可使用 [/main](../../../csharp/language-reference/compiler-options/main-compiler-option.md) 选项指定包含 **Main** 方法的类。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的“属性”页。  
  
2.  单击“应用程序”属性页。  
  
3.  修改“输出类型”属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参阅 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>。  
  
## <a name="example"></a>示例  
 将 `in.cs` 编译为 Windows 程序：  
  
```console  
csc /target:winexe in.cs  
```  
  
## <a name="see-also"></a>请参阅  
 [/target（C# 编译器选项）](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [C# 编译器选项](../../../csharp/language-reference/compiler-options/index.md)

