---
title: "-reference（C# 编译器选项）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /reference
dev_langs:
- CSharp
helpviewer_keywords:
- /r compiler option [C#]
- reference compiler option [C#]
- r compiler option [C#]
- /reference compiler option [C#]
- -r compiler option [C#]
- metadata import [C#]
- public type information [C#]
- -reference compiler option [C#]
ms.assetid: 8d13e5b0-abf6-4c46-bf71-2daf2cd0a6c4
caps.latest.revision: 28
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
ms.openlocfilehash: f057da85202dc5b677af7b9106468b3bc1af6d3f
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="reference-c-compiler-options"></a>/reference（C# 编译器选项）
/reference 选项使编译器将指定文件中的[公共](../../../csharp/language-reference/keywords/public.md)类型信息导入当前项目，从而使你可从指定的程序集文件中引用元数据。  
  
## <a name="syntax"></a>语法  
  
```console  
/reference:[alias=]filename  
/reference:filename  
```  
  
## <a name="arguments"></a>参数  
 `filename`  
 包含程序集清单的文件的名称。 若要导入多个文件，请为每个文件包括一个单独的 /reference 选项。  
  
 `alias`  
 一个有效的 C# 标识符，表示将包含程序集中所有命名空间的根命名空间。  
  
## <a name="remarks"></a>备注  
 若要从多个文件导入，请为每个文件包括一个 /reference 选项。  
  
 导入的文件必须包含一个清单；输出文件必须已使用[/target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md) 以外的一个 [/target](../../../csharp/language-reference/compiler-options/target-compiler-option.md) 选项进行了编译。  
  
 /r 是 /reference 的缩写形式。  
  
 使用 [/addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md) 从不包含程序集清单的输出文件中导入元数据。  
  
 如果引用的程序集（程序集 A）引用了另一个程序集（程序集 B），那么在下列情况下需要引用程序集 B：  
  
-   使用程序集 A 中的类型，该类型继承自程序集 B 中的类型或实现程序集 B 中的接口。  
  
-   调用具有程序集 B 中的返回类型或参数类型的字段、属性、事件或方法。  
  
 使用 [/lib](../../../csharp/language-reference/compiler-options/lib-compiler-option.md) 指定一个或多个程序集引用所在的目录。 /Lib 主题还讨论了编译器在哪些目录中搜索程序集。  
  
 为使编译器可以识别程序集（而不是模块）中的某个类型，需要强制解析此类型，这可以通过定义此类型的实例来完成。 还可通过其他方法为编译器解析程序集中的类型名称：例如，如果从程序集中继承类型，编译器就能识别类型名称。  
  
 有时，需要在一个程序集内引用同一组件的两个不同版本。 为此，请在每个文件的 /reference 开关上使用别名子选项，以区分两个文件。 此别名将用作组件名的限定符，并解析为其中一个文件中的组件。  
  
 默认情况下使用 csc 响应 (.rsp) 文件，该文件引用常用的 .NET Framework 程序集。 如果希望编译器不要使用 csc.rsp，请使用 [/noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md)。  
  
> [!NOTE]
> 在 Visual Studio 中，请使用“添加引用”对话框。 有关详细信息，请参阅[如何：使用引用管理器添加或删除引用](/visualstudio/ide/how-to-add-or-remove-references-by-using-the-reference-manager)。 若要确保通过使用 `/reference` 添加引用与通过使用“添加引用”对话框添加引用之间的行为等效，请将要添加的程序集的“嵌入互操作类型”属性设置为“False”。 “True”是该属性的默认值。  
  
## <a name="example"></a>示例  
 本示例演示如何使用[外部别名](../../../csharp/language-reference/keywords/extern-alias.md)功能。  
  
 编译源文件，并从先前已编译的 `grid.dll` 和 `grid20.dll` 中导入元数据。 这两个 DLL 包含同一组件的不同版本，将使用两个带有别名选项的 /reference 编译源文件。 这两个选项如下所示：  
  
 /reference:GridV1=grid.dll 和 /reference:GridV2=grid20.dll  
  
 这将设置外部别名“GridV1”和“GridV2”，将在程序中通过外部语句使用它们：  
  
```csharp  
extern alias GridV1;  
extern alias GridV2;  
// Using statements go here.  
```  
  
 完成此操作后，可以通过在控件名称前添加 GridV1 前缀来引用 grid.dll 中的网格控件，如下所示：  
  
```csharp  
GridV1::Grid  
```  
  
 此外，可以通过在控件名称前添加 GridV2 前缀来引用 grid20.dll 中的网格控件，如下所示：  
  
```csharp  
GridV2::Grid   
```  
  
## <a name="see-also"></a>另请参阅  
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [管理项目和解决方案属性](/visualstudio/ide/managing-project-and-solution-properties)

