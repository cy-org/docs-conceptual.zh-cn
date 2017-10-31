---
title: "-appconfig（C# 编译器选项）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /appconfig
dev_langs:
- CSharp
helpviewer_keywords:
- /appconfig compiler option [C#]
ms.assetid: 1cdbcbcc-7813-4010-b5b8-e67c107c5a98
caps.latest.revision: 26
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
ms.openlocfilehash: 2aede966f92af3c94f4591b68732dbdbf5a4c5c9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/19/2017

---
# <a name="appconfig-c-compiler-options"></a>/appconfig（C# 编译器选项）
/appconfig 编译器选项让 C# 应用程序能够在程序集绑定时将程序集的应用程序配置 (app.config) 文件的位置指定为公共语言运行时 (CLR)。  
  
## <a name="syntax"></a>语法  
  
```console  
/appconfig:file  
```  
  
## <a name="arguments"></a>参数  
 `file`  
 必需。 包含程序集绑定设置的应用程序配置文件。  
  
## <a name="remarks"></a>备注  
 /appconfig 的一种用途是处理高级情形；在该情形中，程序集必须同时引用特定引用程序集的 .NET Framework 版本和 .NET Framework for Silverlight 版本。 例如，在 Windows Presentation Foundation (WPF) 中编写的 XAML 设计器可能需要为设计器用户界面引用 WPF 桌面以及随附于 Silverlight 的 WPF 子集。 同一设计器程序集必须访问这两个程序集。 默认情况下，单独引用会导致编译器错误，因为程序集绑定将这两个程序集视为等效。  
  
 通过使用 /appconfig 编译器选项，可通过使用 `<supportPortability>` 标记指定某个 app.config 文件的位置，该文件会禁用默认行为，如以下示例所示。  
  
 `<supportPortability PKT="7cec85d7bea7798e" enable="false"/>`  
  
 编译器将文件的位置传递给 CLR 的程序集绑定逻辑。  
  
> [!NOTE]
>  如果使用 Microsoft 生成引擎 (MSBuild) 生成应用程序，则可以通过将属性标记添加到 .csproj 文件来设置 /appconfig 编译器选项。 若要使用已在项目中设置的 app.config 文件，请将属性标记 `<UseAppConfigForCompiler>` 添加到 .csproj 文件，并将其值设置为 `true`。 若要指定不同的 app.config 文件，请添加属性标记 `<AppConfigForCompiler>` 并将其值设置为该文件的位置。  
  
## <a name="example"></a>示例  
 以下示例展示一个 app.config 文件，通过使用该文件，应用程序能够同时引用任何 .NET Framework 程序集（同时存在于后述两个实现中）的 .NET Framework 实现和 .NET Framework for Silverlight 实现。 /appconfig 编译器选项指定此 app.config 文件的位置。  
  
```xml  
<configuration>  
      <runtime>  
      <assemblyBinding>  
            <supportPortability PKT="7cec85d7bea7798e" enable="false"/>  
            <supportPortability PKT="31bf3856ad364e35" enable="false"/>  
      </assemblyBinding>  
      </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>另请参阅  
 [.NET Framework 程序集统一概述](http://msdn.microsoft.com/en-us/8d8cc65e-031d-463b-bde3-2c6dc2e3bc48)   
 [\<supportPortability> 元素](../../../framework/configure-apps/file-schema/runtime/supportportability-element.md)   
 [按字母顺序列出的 C# 编译器选项](../../../csharp/language-reference/compiler-options/listed-alphabetically.md)

