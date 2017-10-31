---
title: "-win32icon（C# 编译器选项）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /win32icon
dev_langs:
- CSharp
helpviewer_keywords:
- win32icon compiler option [C#]
- /win32icon compiler option [C#]
- -win32icon compiler option [C#]
ms.assetid: 756d9b6d-ab07-41b7-ba58-5bd88f711138
caps.latest.revision: 18
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
ms.openlocfilehash: af5b9c3a44163167d932d378cbac4976e07eacbf
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="win32icon-c-compiler-options"></a>/win32icon (C# 编译器选项)
/win32icon 选项在输出文件中插入 .ico 文件，为输出文件赋予其在文件资源管理器中所需的外观。  
  
## <a name="syntax"></a>语法  
  
```console  
/win32icon:filename  
```  
  
## <a name="arguments"></a>参数  
 `filename`  
 想向输出文件添加的 .ico 文件。  
  
## <a name="remarks"></a>备注  
 可以使用[资源编译器](http://go.microsoft.com/fwlink/?LinkId=148370)创建的 .ico 文件。 在编译 Visual C++ 程序时会调用资源编译器；.ico 文件是从 .rc 文件创建的。  
  
 请参阅 [/linkresource](../../../csharp/language-reference/compiler-options/linkresource-compiler-option.md)（引用）或 [/resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md)（附加） .NET Framework 资源文件。 请参阅 [/win32res](../../../csharp/language-reference/compiler-options/win32res-compiler-option.md) 导入 .res 文件。  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的“属性”页。  
  
2.  单击“应用程序”属性页。  
  
3.  修改“应用程序图标”属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参阅 <xref:VSLangProj80.ProjectProperties3.ApplicationIcon%2A>。  
  
## <a name="example"></a>示例  
 编译 `in.cs` 并附加 .ico 文件 `rf.ico` 以生成 `in.exe`：  
  
```console  
csc /win32icon:rf.ico in.cs  
```  
  
## <a name="see-also"></a>另请参阅  
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [管理项目和解决方案属性](/visualstudio/ide/managing-project-and-solution-properties)

