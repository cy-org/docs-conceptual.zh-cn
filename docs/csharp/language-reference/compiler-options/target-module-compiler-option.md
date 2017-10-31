---
title: "-target:module（C# 编译器选项）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /target:module
dev_langs:
- CSharp
helpviewer_keywords:
- -target compiler options [C#], /target:module
- target compiler options [C#], /target:module
- /target compiler options [C#], /target:module
ms.assetid: 9af1e4fa-c749-44e7-ae58-90a3d05d4e72
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
ms.openlocfilehash: 23c91fe0e4002ebf4c002eb4e0c7e25020fed356
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="targetmodule-c-compiler-options"></a>/target:module（C# 编译器选项）
此选项会导致编译器不生成程序集清单。  
  
## <a name="syntax"></a>语法  
  
```console  
/target:module  
```  
  
## <a name="remarks"></a>备注  
 默认情况下，使用此选项编译时所创建的输出文件具有扩展名 .netmodule。  
  
 .NET Framework 公共语言运行时无法加载不含程序集清单的文件。 但是，此类文件可以通过 [/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md) 合并到程序集的程序集清单中。  
  
 如果在一次编译中创建了多个模块，某个模块中的[内部](../../../csharp/language-reference/keywords/internal.md)类型将适用于编译中的其他模块。 如果一个模块中的代码引用另一模块中的 `internal` 类型，则两个模块必须通过 /addmodule 合并到一个程序集清单中。  
  
 Visual Studio 开发环境中不支持创建模块。  
  
 有关如何以编程方式设置此编译器选项的信息，请参阅 <xref:VSLangProj80.ProjectProperties3.OutputType%2A>。  
  
## <a name="example"></a>示例  
 通过创建 `in.netmodule` 编译 `in.cs`：  
  
```console  
csc /target:module in.cs  
```  
  
## <a name="see-also"></a>请参阅  
 [/target（C# 编译器选项）](../../../csharp/language-reference/compiler-options/target-compiler-option.md)   
 [C# 编译器选项](../../../csharp/language-reference/compiler-options/index.md)

