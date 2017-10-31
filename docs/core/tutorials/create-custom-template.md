---
title: "创建 dotnet new 自定义模板"
description: "在本趣味性教程中，了解如何创建 dotnet new 命令的自定义模板。"
keywords: ".NET, .NET Core, 模板, 模板化, 教程, dotnet new"
author: guardrex
ms.author: mairaw
ms.date: 08/12/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 519b910a-6efe-4394-9b81-0546aa3e7462
ms.translationtype: HT
ms.sourcegitcommit: a7af88d8d7b19e201c0f7829915e817daa61c838
ms.openlocfilehash: 243c924826a54907840b337a91cf1e5d19cff985
ms.contentlocale: zh-cn
ms.lasthandoff: 09/08/2017

---

# <a name="create-a-custom-template-for-dotnet-new"></a>创建 dotnet new 自定义模板

本教程介绍了如何：

- 通过现有项目或新控制台应用程序项目创建基本模板。
- 从 nuget.org 或本地 nupkg 文件打包模板以供分发。
- 从 nuget.org、本地 nupkg 文件或本地文件系统安装模板。
- 卸载模板。

若要通过完整示例继续学习本教程，请下载[示例项目模板](https://github.com/dotnet/dotnet-template-samples/tree/master/16-nuget-package)。 示例模板针对 NuGet 分发进行了配置。

若要将下载的示例与文件系统分发相结合，请按照以下步骤操作：

- 将示例中 content 文件夹的内容移到上一级 GarciaSoftware.ConsoleTemplate.CSharp 文件夹中。
- 删除空的 content 文件夹。
- 删除 nuspec 文件。

## <a name="prerequisites"></a>先决条件

- 安装 [.NET Core 2.0 SDK](https://www.microsoft.com/net/core) 或更高版本。
- 阅读参考主题 [dotnet new 自定义模板](../tools/custom-templates.md)。

## <a name="create-a-template-from-a-project"></a>通过项目创建模板

使用已确认可以编译或运行的现有项目，或在硬盘上的文件夹中新建一个控制台应用程序项目。 本教程假定项目文件夹名为 GarciaSoftware.ConsoleTemplate.CSharp，并存储在用户配置文件中的 Documents/Templates。 本教程的项目模板名称采用格式“\<公司名称>.\<模板类型>.\<编程语言>”，但也可以根据自己的意愿随意命名项目和模板。

1. 向 .template.config 项目根添加文件夹。
1. 在 .template.config 文件夹中，创建 template.json 文件来配置模板。 有关 template.json 文件的详细信息和成员定义，请参阅 [dotnet new 自定义模板](../tools/custom-templates.md#templatejson)主题和 [JSON 架构存储中的 template.json 架构](http://json.schemastore.org/template)。

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

模板已完成。 此时，可通过两种方式分发模板。 若要继续阅读本教程，请选择下面两种路径之一：

1. [NuGet 分发](#use-nuget-distribution)：从 NuGet 或本地 nupkg 文件安装模板，并使用安装后的模板。
2. [文件系统分发](#use-file-system-distribution)。

## <a name="use-nuget-distribution"></a>使用 NuGet 分发

### <a name="pack-the-template-into-a-nuget-package"></a>将模板打包到 NuGet 包中

1. 为 NuGet 包创建文件夹。 在本教程中，此文件夹名为 GarciaSoftware.ConsoleTemplate.CSharp，并在用户配置文件中的 Documents/NuGetTemplates 文件夹内创建。 在新建的模板文件夹内，创建名为 content 的文件夹，以保存项目文件。
1. 将项目文件夹的内容连同 .template.config/template.json 文件一起复制到创建的 content 文件夹中。
1. 在 content 文件夹旁边，添加 [nuspec 文件](/nuget/create-packages/creating-a-package)。 nuspec 文件是 XML 清单文件，用于描述包内容，并促进创建 NuGet 包。
   
   ![显示 NuGet 包布局的目录结构](./media/create-custom-template/nugetdirectorylayout.png)

1. 在 nuspec文件的 \<packageTypes> 元素中，添加 `name` 属性值为 `Template` 的 \<packageType> 元素。 content 文件夹和 nuspec 文件应位于同一目录。 下表列出了将模板生成为 NuGet 包至少所需的 nuspec 文件元素。

   | 元素            | 类型   | 描述 |
   | ------------------ | ------ | ----------- |
   | **\<authors>**     | string | 包创建者的逗号分隔列表，与 nuget.org 上的配置文件名称一致。创建者显示在 nuget.org 上的 NuGet 库中，用于交叉引用同一创建者的包。 |
   | **\<description>** | string | 用于 UI 显示的包的详细说明。 |
   | **\<id>**          | string | 不区分大小写的包标识符，在 nuget.org 或包驻留的任意库中必须是唯一的。 ID 不得包含空格或对 URL 无效的字符，通常遵循 .NET 命名空间规则。 有关指南，请参阅[选择唯一包标识符并设置版本号](/nuget/create-packages/creating-a-package#choosing-a-unique-package-identifier-and-setting-the-version-number)。 |
   | **\<packageType>** | string | 将此元素置于 \<metadata> 元素之间的 \<packageTypes> 元素内。 将 \<packageType> 元素的 `name` 属性设置为 `Template`。 |
   | **\<version>**     | string | 遵循 major.minor.patch 模式的包版本。 版本号可能包括预发布后缀，如[预发布版本](/nuget/create-packages/prerelease-packages#semantic-versioning)中所述。 |

   有关完整的 nuspec 文件架构，请参阅 [.nuspec 参考](/nuget/schema/nuspec)。

   在本教程中，nuspec 文件命名为 GarciaSoftware.ConsoleTemplate.CSharp.nuspec，包含以下内容：

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
     <metadata>
       <id>GarciaSoftware.ConsoleTemplate.CSharp</id>
       <version>1.0.0</version>
       <description>
         Creates the Garcia Software console app.
       </description>
       <authors>Catalina Garcia</authors>
       <packageTypes>
         <packageType name="Template" />
       </packageTypes>
     </metadata>
   </package>
   ```

1. 使用 `nuget pack <PATH_TO_NUSPEC_FILE>` 命令[创建包](/nuget/create-packages/creating-a-package#creating-the-package)。 以下命令假定包含 NuGet 资产的文件夹位于 C:/Users/\<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp/。 不过，无论将文件夹放置在系统上的什么位置，`nuget pack` 命令都接受 nuspec 文件路径：

   ```console
   nuget pack C:/Users/<USER>/Documents/NuGetTemplates/GarciaSoftware.ConsoleTemplate.CSharp/GarciaSoftware.ConsoleTemplate.CSharp.nuspec
   ```

### <a name="publishing-the-package-to-nugetorg"></a>将包发布到 nuget.org

若要发布 NuGet 包，请按照[创建和发布包](/nuget/quickstart/create-and-publish-a-package#publish-the-package)主题中的说明操作。 不过，不建议将本教程的模板发布到 NuGet，因为一旦发布，便永远无法删除，只能从列表去除。 至此已拥有 nupkg 文件形式的 NuGet 包，建议按照下面的说明操作，直接从本地 nupkg 文件安装模板。

### <a name="install-the-template-from-a-nuget-package"></a>从 NuGet 包安装模板

#### <a name="install-the-template-from-the-local-nupkg-file"></a>从本地 nupkg 文件安装模板

若要从生成的 nupkg 文件安装模板，请结合使用 `dotnet new` 命令和 `-i|--install` 选项，并提供 nupkg 文件路径：

```console
dotnet new -i C:/Users/<USER>/GarciaSoftware.ConsoleTemplate.CSharp.1.0.0.nupkg
```

#### <a name="install-the-template-from-a-nuget-package-stored-at-nugetorg"></a>从 nuget.org 中存储的 NuGet 包安装模板

若要从 nuget.org 中存储的 NuGet 包安装模板，请结合使用 `dotnet new` 命令和 `-i|--install` 选项，并提供 NuGet 包名称：

```console
dotnet new -i GarciaSoftware.ConsoleTemplate.CSharp
```

> [!NOTE]
> 示例代码只为了方便本文演示。 如果 nuget.org 中没有 `GarciaSoftware.ConsoleTemplate.CSharp` NuGet 包，不建议发布并从 NuGet 使用测试模板。 如果运行此命令，不会安装任何模板。 不过，可以安装尚未发布到 nuget.org 的模板，具体方法是直接在本地文件系统上引用 nupkg 文件，如前一部分[从本地 nupkg 文件安装模板](#install-the-template-from-the-local-nupkg-file)所述。

如果需要获取有关如何从 nuget.org 中的包安装模板的实际示例，可以使用 [dotnet-new 的 NUnit 3 模板](https://www.nuget.org/packages/NUnit3.DotNetNew.Template/)。 此模板将项目设置为使用 NUnit 单元测试。 运行以下命令安装此模板：

```console
dotnet new -i NUnit3.DotNetNew.Template
```

使用 `dotnet new -l` 列出模板时，模板列表中会列出短名称为“nunit”的“NUnit 3 测试项目”。 可以在下一部分中使用此模板了。

![控制台窗口将 NUnit 模板与其他已安装的模板一起列出](./media/create-custom-template/nunit1.png)

### <a name="create-a-project-from-the-template"></a>通过模板创建项目

从 NuGet 安装模板后，在要放置模板引擎输出的目录（除非使用 `-o|--output` 选项指定特定的目录）执行 `dotnet new <TEMPLATE>` 命令，即可使用模板。 有关详细信息，请参阅 [`dotnet new` 选项](~/docs/core/tools/dotnet-new.md#options)。 直接向 `dotnet new` 命令提供模板的短名称。 若要通过 NUnit 模板创建项目，请运行以下命令：

```console
dotnet new nunit
```

控制台显示项目已创建，且项目包已还原。 运行此命令后，项目便可供使用。

![控制台窗口显示 dotnet new 命令创建 NUnit 项目并还原项目依赖项时的输出](./media/create-custom-template/nunit2.png)

### <a name="to-uninstall-a-template-from-a-nuget-package-stored-at-nugetorg"></a>从 nuget.org 中存储的 NuGet 包卸载模板的具体步骤

```console
dotnet new -u GarciaSoftware.ConsoleTemplate.CSharp
```

> [!NOTE]
> 示例代码只为了方便本文演示。 `GarciaSoftware.ConsoleTemplate.CSharp` NuGet 包没有存储到 nuget.org 或与 .NET Core SDK 一起安装。 如果运行此命令，不会卸载任何包/模板，并会看到以下异常消息：
> 
> > 找不到要卸载的“GarciaSoftware.ConsoleTemplate.CSharp”包/模板。

若要卸载已安装的 [dotnet-new 的 NUnit 3 模板](https://www.nuget.org/packages/NUnit3.DotNetNew.Template/)，请运行以下命令：

```console
dotnet new -u NUnit3.DotNetNew.Template
```

### <a name="uninstall-the-template-from-a-local-nupkg-file"></a>从本地 nupkg 文件卸载模板

若要卸载模板，请勿尝试使用 nupkg 文件路径。 无法尝试使用 `dotnet new -u <PATH_TO_NUPKG_FILE>` 卸载模板。 按 `id` 引用包：

```console
dotnet new -u GarciaSoftware.ConsoleTemplate.CSharp.1.0.0
```

## <a name="use-file-system-distribution"></a>使用文件系统分发

若要分发模板，请确保用户可以在网络上访问项目模板文件夹的位置。 结合使用 `dotnet new` 命令和 `-i|--install` 选项，并指定模板文件夹路径（包含项目和 .template.config 文件夹的项目文件夹）。

本教程假定项目模板存储在用户配置文件中的 Documents/Templates 文件夹内。 从这个位置，使用以下命令安装模板，只将 \<USER> 替换为用户的配置文件名称：

```console
dotnet new -i C:/Users/<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp
```

### <a name="create-a-project-from-the-template"></a>通过模板创建项目

从文件系统安装模板后，在要放置模板引擎输出的目录（除非使用 `-o|--output` 选项指定特定的目录）执行 `dotnet new <TEMPLATE>` 命令，即可使用模板。 有关详细信息，请参阅 [`dotnet new` 选项](~/docs/core/tools/dotnet-new.md#options)。 直接向 `dotnet new` 命令提供模板的短名称。

从 C:/Users/\<USER>/Documents/Projects/MyConsoleApp 处创建的新项目文件夹，通过 `garciaconsole` 模板创建项目：

```console
dotnet new garciaconsole
```

### <a name="uninstall-the-template"></a>卸载模板

如果在本地文件系统中的 C:/Users/\<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp 处创建模板，请使用 `-u|--uninstall` 开关和模板文件夹路径卸载模板：

```console
dotnet new -u C:/Users/<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp
```

> [!NOTE]
> 若要从本地文件系统卸载模板，需要完全限定路径。 例如，C:/Users/\<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp 有效，但是包含文件夹中的 ./GarciaSoftware.ConsoleTemplate.CSharp 无效。
> 此外，模板路径中不要包含最后的终止目录斜杠。

## <a name="see-also"></a>请参阅

[dotnet/templating GitHub 存储库 Wiki](https://github.com/dotnet/templating/wiki)  
[dotnet/dotnet-template-samples GitHub 存储库](https://github.com/dotnet/dotnet-template-samples)  
[如何创建自己的 dotnet new 模板](https://blogs.msdn.microsoft.com/dotnet/2017/04/02/how-to-create-your-own-templates-for-dotnet-new/)  
[JSON 架构存储中的 template.json 架构](http://json.schemastore.org/template)  

