---
title: "-nowarn（C# 编译器选项）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /nowarn
dev_langs:
- CSharp
helpviewer_keywords:
- nowarn compiler option [C#]
- /nowarn compiler option [C#]
- -nowarn compiler option [C#]
ms.assetid: 6dcbc5e8-ae67-4566-9df3-f63cfdd9c4e4
caps.latest.revision: 24
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
ms.openlocfilehash: 3bae7e6d16c044b8f1aeba26de434cdf17479e82
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="nowarn-c-compiler-options"></a>/nowarn（C# 编译器选项）
**/nowarn** 选项使你可以禁止编译器显示一个或多个警告。 使用逗号分隔多个警告编号。  
  
## <a name="syntax"></a>语法  
  
```console  
/nowarn:number1[,number2,...]  
```  
  
## <a name="arguments"></a>自变量  
 `number1`, `number2`  
 希望编译器禁止显示的警告编号。  
  
## <a name="remarks"></a>备注  
 只应指定警告标识符的数值部分。 例如，如果要禁止显示 CS0028，则可以指定 `/nowarn:28`。  
  
 编译器会以无提示方式忽略传递给 `/nowarn` 的警告编号，这些编号在早期版本中有效，但已从编译器中移除。 例如，CS0679 在 Visual Studio .NET 2002 的编译器中有效，但是在后来已移除。  
  
 无法通过 `/nowarn` 选项禁止显示以下警告：  
  
-   编译器警告（等级 1）CS2002  
  
-   编译器警告（等级 1）CS2023  
  
-   编译器警告（等级 1）CS2029  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项  
  
1.  打开项目的“属性”  页。 有关详细信息，请参阅[“项目设计器”->“生成”页 (C#)](/visualstudio/ide/reference/build-page-project-designer-csharp)。  
  
2.  单击“生成”属性页。  
  
3.  修改“禁止显示警告”属性。  
  
 有关如何以编程方式设置此编译器选项的信息，请参阅 <xref:VSLangProj80.ProjectProperties3.DelaySign%2A>。  
  
## <a name="see-also"></a>另请参阅  
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [管理项目和解决方案属性](/visualstudio/ide/managing-project-and-solution-properties)   
 [C# 编译器错误](../../../csharp/language-reference/compiler-messages/index.md)

