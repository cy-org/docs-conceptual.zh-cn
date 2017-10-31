---
title: "dotnet new 自定义模板"
description: "了解任意类型 .NET 项目或文件的自定义模板。"
keywords: "dotnet new, CLI, CLI 命令, .NET Core, 模板,模板化"
author: guardrex
ms.author: mairaw
ms.date: 08/11/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.translationtype: HT
ms.sourcegitcommit: c58ed1b3c09f1e358d0b66f6cf7186821601fd69
ms.openlocfilehash: c68e382450a763fd0521b7defdd79d8433e1acde
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---

# <a name="custom-templates-for-dotnet-new"></a>dotnet new 自定义模板

[.NET Core SDK](https://www.microsoft.com/net/download/core) 附带许多预安装的模板，与 [`dotnet new` 命令](dotnet-new.md)结合使用。 自.NET Core 2.0 起，可以为任何类型的项目（如应用程序、服务、工具或类库）创建自己的自定义模板。 甚至可以创建输出一个或多个独立文件（如配置文件）的模板。

可以从任何 NuGet 源上的 NuGet 包安装自定义模板，具体方法是直接引用 NuGet nupkg 文件，或指定包含模板的文件系统目录。 借助模板引擎提供的功能，可以替换值、添加和排除文件和文件区域，并在使用模板时执行自定义处理操作。

模板引擎是开放源代码，在线代码存储库位于 GitHub 上的 [dotnet/templating](https://github.com/dotnet/templating/)。 有关模板示例，请访问 [dotnet/dotnet-template-samples](https://github.com/dotnet/dotnet-template-samples) 存储库。 GitHub 上的 [dotnet new 可用模板](https://github.com/dotnet/templating/wiki/Available-templates-for-dotnet-new)收录了更多模板，包括第三方模板。 若要详细了解如何创建和使用自定义模板，请参阅[如何创建自己的 dotnet new 模板](https://blogs.msdn.microsoft.com/dotnet/2017/04/02/how-to-create-your-own-templates-for-dotnet-new/)和 [dotnet/templating GitHub 存储库 Wiki](https://github.com/dotnet/templating/wiki)。

若要按照演示步骤操作并创建模板，请参阅[创建 dotnet new 自定义模板](~/docs/core/tutorials/create-custom-template.md)教程。

## <a name="configuration"></a>配置

模板由以下部分组成：

- 源文件和文件夹
- 配置文件 (template.json)

### <a name="source-files-and-folders"></a>源文件和文件夹

源文件和文件夹包含执行 `dotnet new <TEMPLATE>` 命令时用户希望模板引擎使用的任何文件和文件夹。 模板引擎旨在将可运行项目用作源代码，以生成项目。 这样做有以下几个好处：

- 模板引擎不要求用户将特殊令牌注入项目的源代码。
- 代码文件不必是特殊文件，也不必以任何方式进行修改，即可与模板引擎配合使用。 因此，处理项目时通常使用的工具也适用于模板内容。
- 生成、运行和调试模板项目，就像生成、运行和调试其他任何项目一样。
- 只需将 template.json 配置文件添加到项目，即可通过现有项目快速创建模板。

模板中存储的文件和文件夹并不限于正式的 .NET 项目类型，如 .NET Core 或 .NET Framework 解决方案。 源文件和文件夹可能包含用户希望在使用模板时创建的任何内容，即使模板引擎仅输出一个文件（如配置文件或解决方案文件），也不例外。 例如，可以创建包含 web.config 源文件的模板，并在使用模板时为项目创建经过修改的 web.config 文件。 源文件修改依据为用户在 template.json 配置文件中提供的逻辑和设置，以及用户提供的作为选项传递到 `dotnet new <TEMPLATE>` 命令的值。

### <a name="templatejson"></a>template.json

template.json 文件位于模板根目录中的 .template.config 文件夹。 此文件向模板引擎提供配置信息。 最低配置必须包含下表中列出的成员，这足以创建功能模板。

| 成员            | 类型          | 描述 |
| ----------------- | ------------- | ----------- |
| `$schema`         | URI           | template.json 文件的 JSON 架构。 如果指定架构，支持 JSON 架构的编辑器启用 JSON 编辑功能。 例如，[Visual Studio Code](https://code.visualstudio.com/) 要求此成员启用 IntelliSense。 使用值 `http://json.schemastore.org/template`。 |
| `author`          | string        | 模板创建者。 |
| `classifications` | array(string) | 为了找到模板，用户可能会在搜索模板时使用的 0 个或多个模板特征。 如果出现在使用 <code>dotnet new -l&#124;--list</code> 命令生成的模板列表中，classifications 还会出现在“Tags”列中。 |
| `identity`        | string        | 此模板的唯一名称。 |
| `name`            | string        | 用户应看到的模板名称。 |
| `shortName`       | string        | 方便用户选择模板的默认速记属性，适用于模板名称由用户指定（而不是通过 GUI 选择）的环境。 例如，通过命令提示符和 CLI 命令使用模板时，短名称非常有用。 |

#### <a name="example"></a>示例:

```json
{
  "$schema": "http://json.schemastore.org/template",
  "author": "Catalina Garcia",
  "classifications": [ "Common", "Console" ],
  "identity": "GarciaSoftware.ConsoleTemplate.CSharp",
  "name": "Garcia Software Console Application",
  "shortName": "garciaconsole"
}
```

template.json 文件的完整架构位于 [JSON 架构存储](http://json.schemastore.org/template)。

## <a name="net-default-templates"></a>.NET 默认模板

安装 [.NET Core SDK](https://www.microsoft.com/net/download/core) 时，将获取十多个用于创建项目和文件的内置模板，包括控制台应用程序、类库、单元测试项目、ASP.NET Core 应用程序（包括 [Angular](https://angular.io/) 和 [React](https://facebook.github.io/react/) 项目）和配置文件。 若要列出内置模板，请执行 `dotnet new` 命令和 `-l|--list` 选项：

```console
dotnet new -l
```

## <a name="packing-a-template-into-a-nuget-package-nupkg-file"></a>将模板打包到 NuGet 包（nupkg 文件）

目前，在 Windows 上使用 [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)（而不是 [dotnet pack](dotnet-pack.md)）打包自定义模板。 若要进行跨平台打包，请考虑使用 [NuGetizer 3000](https://github.com/NuGet/Home/wiki/NuGetizer-3000)。

将项目文件夹的内容连同 .template.config/template.json 文件一起放入 content 文件夹中。 在 content 文件夹旁边，添加 [nuspec 文件](/nuget/create-packages/creating-a-package)。这是一个 XML 清单文件，用于描述包内容，并促进创建 NuGet 包。 在 nuspec文件的 \<packageTypes> 元素中，添加 `name` 属性值为 `Template` 的 \<packageType> 元素。 content 文件夹和 nuspec 文件应位于同一目录。 下表列出了将模板生成为 NuGet 包至少所需的 nuspec 文件元素。

| 元素            | 类型   | 描述 |
| ------------------ | ------ | ----------- |
| **\<authors>**     | string | 包创建者的逗号分隔列表，与 nuget.org 上的配置文件名称一致。 创建者显示在 nuget.org 上的 NuGet 库中，用于交叉引用同一创建者的包。 |
| **\<description>** | string | 用于 UI 显示的包的详细说明。 |
| **\<id>**          | string | 不区分大小写的包标识符，在 nuget.org 或包驻留的任意库中必须是唯一的。 ID 不得包含空格或对 URL 无效的字符，通常遵循 .NET 命名空间规则。 有关指南，请参阅[选择唯一包标识符并设置版本号](/nuget/create-packages/creating-a-package#choosing-a-unique-package-identifier-and-setting-the-version-number)。 |
| **\<packageType>** | string | 将此元素置于 \<metadata> 元素之间的 \<packageTypes> 元素内。 将 \<packageType> 元素的 `name` 属性设置为 `Template`。 |
| **\<version>**     | string | 遵循 major.minor.patch 模式的包版本。 版本号可能包括预发布后缀，如[预发布版本](/nuget/create-packages/prerelease-packages#semantic-versioning)主题中所述。 |

有关完整的 nuspec 文件架构，请参阅 [.nuspec 参考](/nuget/schema/nuspec)。 [创建 dotnet new 自定义模板](~/docs/core/tutorials/create-custom-template.md)教程中展示了模板的示例 nuspec 文件。

使用 `nuget pack <PATH_TO_NUSPEC_FILE>` 命令[创建包](/nuget/create-packages/creating-a-package#creating-the-package)。

## <a name="installing-a-template"></a>安装模板

从任何 NuGet 源上的 NuGet 包安装自定义模板，具体方法是直接引用 nupkg 文件，或指定包含模板配置的文件系统目录。 结合使用 `-i|--install` 选项和 [dotnet new](dotnet-new.md) 命令。

### <a name="to-install-a-template-from-a-nuget-package-stored-at-nugetorg"></a>从 nuget.org 中存储的 NuGet 包安装模板的具体步骤

```console
dotnet new -i <NUGET_PACKAGE_ID>
```

### <a name="to-install-a-template-from-a-local-nupkg-file"></a>从本地 nupkg 文件安装模板的具体步骤

```console
dotnet new -i <PATH_TO_NUPKG_FILE>
```

### <a name="to-install-a-template-from-a-file-system-directory"></a>从文件系统目录安装模板的具体步骤

`FILE_SYSTEM_DIRECTORY` 是包含项目和 .template.config 文件夹的项目文件夹：

```console
dotnet new -i <FILE_SYSTEM_DIRECTORY>
```

## <a name="uninstalling-a-template"></a>卸载模板

卸载自定义模板的方法是，按 `id` 引用 NuGet 包，或指定包含模板配置的文件系统目录。 结合使用 `-u|--uninstall` 安装选项和 [dotnet new](dotnet-new.md) 命令。

### <a name="to-uninstall-a-template-from-a-nuget-package-stored-at-nugetorg"></a>从 nuget.org 中存储的 NuGet 包卸载模板的具体步骤

```console
dotnet new -u <NUGET_PACKAGE_ID>
```

### <a name="to-uninstall-a-template-from-a-local-nupkg-file"></a>从本地 nupkg 文件卸载模板的具体步骤

若要卸载模板，请勿尝试使用 nupkg 文件路径。 无法尝试使用 `dotnet new -u <PATH_TO_NUPKG_FILE>` 卸载模板。 按 `id` 引用包：

```console
dotnet new -u <NUGET_PACKAGE_ID>
```

### <a name="to-uninstall-a-template-from-a-file-system-directory"></a>从文件系统目录卸载模板的具体步骤

`FILE_SYSTEM_DIRECTORY` 是包含项目和 .template.config 文件夹的项目文件夹：

```console
dotnet new -u <FILE_SYSTEM_DIRECTORY>
```

## <a name="create-a-project-using-a-custom-template"></a>使用自定义模板创建项目

安装模板后，通过执行 `dotnet new <TEMPLATE>` 命令来使用模板，就像使用其他任何预安装模板一样。 还可以为 `dotnet new` 命令指定[选项](dotnet-new.md#options)，包括在模板设置中配置的模板专用选项。 直接向命令提供模板的短名称：

```console
dotnet new <TEMPLATE>
```

## <a name="see-also"></a>另请参阅

[创建 dotnet new 自定义模板（教程）](../tutorials/create-custom-template.md)  
[dotnet/templating GitHub 存储库 Wiki](https://github.com/dotnet/templating/wiki)  
[dotnet/dotnet-template-samples GitHub 存储库](https://github.com/dotnet/dotnet-template-samples)  
[如何创建自己的 dotnet new 模板](https://blogs.msdn.microsoft.com/dotnet/2017/04/02/how-to-create-your-own-templates-for-dotnet-new/)  
[JSON 架构存储中的 template.json 架构](http://json.schemastore.org/template)  

