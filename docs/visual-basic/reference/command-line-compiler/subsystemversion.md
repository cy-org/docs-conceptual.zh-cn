---
title: "/subsystemversion (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- /subsystemversion compiler option [Visual Basic]
- -subsystemversion compiler option [Visual Basic]
- subsystemversion compiler option [Visual Basic]
ms.assetid: 08be22b2-f447-4cd3-8203-120b1b920b54
caps.latest.revision: 9
author: dotnet-bot
ms.author: dotnetcontent
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: bc9ea6a844fae7f98315e5d3557fdf306f467dd5
ms.lasthandoff: 03/13/2017

---
# <a name="subsystemversion-visual-basic"></a>/subsystemversion (Visual Basic)
指定在其可以运行生成的可执行文件，由此决定用的可执行文件可以在其运行的 Windows 版本的子系统的最低版本。 大多数情况下，此选项可确保可执行文件可以利用无法适用于 Windows 的早期版本的特定安全功能。  
  
> [!NOTE]
>  若要指定子系统本身，请使用[target](../../../csharp/language-reference/compiler-options/target-compiler-option.md)编译器选项。  
  
## <a name="syntax"></a>语法  
  
```vb  
/subsystemversion:major.minor  
```  
  
#### <a name="parameters"></a>参数  
 `major.minor`  
 所需的最低版本的子系统，如在主要和次要版本圆点表示法表示。 例如，您可以指定应用程序不能低于 Windows 7 如果将此选项的值设置为 6.01，如本主题后面的表中所述的操作系统上运行。 您必须指定的值`major`和`minor`为整数。  
  
 的前导零`minor`版本不会更改版本，但尾随零。 例如，6.1 和 6.01 引用相同的版本，但是 6.10 引用与另一个版本。 我们建议为一个两位数，以避免混淆表达的次版本。  
  
## <a name="remarks"></a>备注  
 下表列出常见的子系统版本的 Windows。  
  
|Windows 版本|子系统版本|  
|---------------------|-----------------------|  
|Windows 2000|5.00|  
|Windows XP|5.01|  
|Windows Server 2003|5.02|  
|Windows Vista|6.00|  
|Windows 7|6.01|  
|Windows Server 2008|6.01|  
|[!INCLUDE[win8](../../../csharp/language-reference/compiler-options/includes/win8_md.md)]|6.02|  
  
## <a name="default-values"></a>默认值  
 默认值为**/subsystemversion**编译器选项取决于下面的列表中的条件︰  
  
-   默认值为 6.02，如果设置了以下列表中的任何编译器选项︰  
  
    -   [/target: appcontainerexe](../../../visual-basic/reference/command-line-compiler/target.md)  
  
    -   [/target: winmdobj](../../../visual-basic/reference/command-line-compiler/target.md)  
  
    -   [/platform:arm](../../../visual-basic/reference/command-line-compiler/platform.md)  
  
-   默认值是 6.00，如果你使用 MSBuild，您的目标[!INCLUDE[net_v45](../../../csharp/language-reference/compiler-options/includes/net_v45_md.md)]，并没有设置任何先前在此列表中已指定的编译器选项。  
  
-   如果无前几个条件为 true，则默认值是 4.00。  
  
## <a name="setting-this-option"></a>设置此选项  
 若要设置**/subsystemversion**编译器选项在 Visual Studio 中，您必须打开.vbproj 文件，并为指定值`SubsystemVersion`MSBuild XML 中的属性。 不能在 Visual Studio IDE 中设置此选项。 有关详细信息，请参阅"默认值本主题前面的或[常用的 MSBuild 项目属性](https://docs.microsoft.com/visualstudio/msbuild/common-msbuild-project-properties)。  
  

  
## <a name="see-also"></a>另请参阅  
[Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)

[MSBuild 属性](https://docs.microsoft.com/visualstudio/msbuild/msbuild-properties)

