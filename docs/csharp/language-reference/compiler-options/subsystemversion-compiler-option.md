---
title: "-subsystemversion（C# 编译器选项）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: a99fce81-9d92-4813-9874-bee777041445
caps.latest.revision: 19
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
ms.openlocfilehash: c7992086eb33577d795496025820ed8f7bb51c24
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="subsystemversion-c-compiler-options"></a>/subsystemversion（C# 编译器选项）
指定可以运行生成的可执行文件的子系统的最低版本，以此确定可以运行该可执行文件的 Windows 版本。 大多数情况下，此选项确保该可执行文件可以利用早期 Windows 版本中未提供的特定安全功能。  
  
> [!NOTE]
>  若要指定子系统本身，请使用 [/target](../../../csharp/language-reference/compiler-options/target-compiler-option.md) 编译器选项。  
  
## <a name="syntax"></a>语法  
  
```console  
/subsystemversion:major.minor  
```  
  
#### <a name="parameters"></a>参数  
 `major.minor`  
 所需的子系统最低版本，以主版本和次要版本之间使用点标记的方式表示。 例如，如果将此选项的值设置为 6.01，则可以指定应用程序不能在低于 Windows 7 的操作系统上运行（如本主题后面的表中所述）。 必须将 `major` 和 `minor` 的值指定为整数。  
  
 `minor` 版本中的前导零不会更改版本，但尾随零会。 例如，6.1 和 6.01 表示相同的版本，但 6.10 表示另一个版本。 建议次要版本用两位数表示，以免混淆。  
  
## <a name="remarks"></a>备注  
 下表列出了常见的 Windows 子系统版本。  
  
|Windows 版本|子系统版本|  
|---------------------|-----------------------|  
|Windows 2000|5.00|  
|Windows XP|5.01|  
|Windows Server 2003|5.02|  
|Windows Vista|6.00|  
|Windows 7|6.01|  
|Windows Server 2008|6.01|  
|[!INCLUDE[win8](~/includes/win8-md.md)]|6.02|  
  
## <a name="default-values"></a>默认值  
 **/subsystemversion** 编译器选项的默认值取决于以下列表中的条件：  
  
-   只要设置了以下列表中的任意编译器选项，则默认值为 6.02：  
  
    -   [/target:appcontainerexe](../../../csharp/language-reference/compiler-options/target-appcontainerexe-compiler-option.md)  
  
    -   [/target:winmdobj](../../../csharp/language-reference/compiler-options/target-winmdobj-compiler-option.md)  
  
    -   [/platform:arm](../../../csharp/language-reference/compiler-options/platform-compiler-option.md)  
  
-   如果使用 MSBuild，面向 [!INCLUDE[net_v45](~/includes/net-v45-md.md)]，并且未设置先前在此列表中指定的任何编译器选项，则默认值为 6.00。  
  
-   如果前面的条件均不符合，则默认值为 4.00。  
  
## <a name="setting-this-option"></a>设置此选项  
 若要在 Visual Studio 中设置 **/subsystemversion** 编译器选项，必须打开 .csproj 文件，并在 MSBuild XML 中为 `SubsystemVersion` 属性指定一个值。 不能在 Visual Studio IDE 中设置此选项。 有关详细信息，请参阅本主题前面的“默认值”或[常用的 MSBuild 项目属性](/visualstudio/msbuild/common-msbuild-project-properties)。  
  
## <a name="see-also"></a>请参阅  
 [C# 编译器选项](../../../csharp/language-reference/compiler-options/index.md)

