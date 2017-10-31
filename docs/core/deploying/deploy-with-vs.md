---
title: "使用 Visual Studio 部署 .NET Core 应用"
description: "了解如何使用 Visual Studio 部署 .NET Core 应用"
keywords: ".NET、.NET Core、.NET Core 部署"
author: rpetrusha
ms.author: ronpet
ms.date: 04/18/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 01049a21-fd50-4419-9ab2-0e4a2e091050
ms.translationtype: HT
ms.sourcegitcommit: b647c5dc4e565f9813212d75fab4a2e46c1a47b9
ms.openlocfilehash: 19f5234ce667b2064a1e5b3fb50222c1ef4fe2a5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/12/2017

---

# <a name="deploying-net-core-apps-with-visual-studio"></a>使用 Visual Studio 部署 .NET Core 应用

可将 .NET Core 应用程序部署为依赖框架的部署或独立部署，前者包含应用程序二进制文件，但依赖目标系统上存在的 .NET Core，而后者同时包含应用程序和 .NET Core 二进制文件。 有关 .NET Core 应用程序部署的概述，请参阅 [.NET Core 应用程序部署](index.md)。

以下各节演示如何使用 Microsoft Visual Studio 创建下列各类部署：

- 依赖框架的部署
- 包含第三方依赖项的依赖框架的部署
- 独立部署
- 包含第三方依赖项的独立部署

有关使用 Visual Studio 开发 .NET Core 应用程序的信息，请参阅 [Windows 上 .NET Core 的先决条件](../windows-prerequisites.md#prerequisites-with-visual-studio-2017)。

## <a name="framework-dependent-deployment"></a>依赖框架的部署

如果不使用第三方依赖项，部属依赖框架的部署只包括生成、测试和发布应用。 一个用 C# 编写的简单示例可说明此过程。  

1. 创建项目。

   选择“文件” > “新建” > “项目”。 在“新建项目”对话框中，在“已安装”项目类型窗格中选择“.NET Core”，然后在中心窗格中选择“控制台应用(.NET Core)”模板。 在“名称”文本框中输入项目名称，如“FDD”。 选择“确定”按钮。

1. 添加应用程序的源代码。

   在编辑器中打开 Program.cs 文件，然后使用下列代码替换自动生成的代码。 它会提示用户输入文本，并显示用户输入的个别词。 它使用正则表达式 `\w+` 来将输入文本中的词分开。

   [!code-cs[deployment#1](../../../samples/snippets/core/deploying/deployment-example.cs)]

1. 创建应用的调试版本。

   选择“生成” > “生成解决方案”。 也可通过选择“调试” > “开始调试”来编译和运行应用程序的调试版本。

1. 部署应用。

   调试并测试程序后，创建要与应用一起部署的文件。 若要从 Visual Studio 发布，请执行以下操作：

      1. 将工具栏上的解决方案配置从“调试”更改为“发布”，生成应用的发布（而非调试）版本。

      1. 在“解决方案资源管理器”中右键单击项目（而非解决方案），然后选择“发布”。

      1. 在“发布”选项卡上，选择“发布”。 Visual Studio 将包含应用程序的文件写入本地文件系统。

      1. “发布”选项卡现在显示单个配置文件 FolderProfile。 该配置文件的配置设置显示在选项卡的“摘要”部分。

   生成的文件位于名为 `PublishOutput` 的目录中，该目录位于项目的 .\bin\release 子目录的子目录中。

与应用程序的文件一起，发布过程将发出包含应用调试信息的程序数据库 (.pdb) 文件。 该文件主要用于调试异常。 可以选择不使用应用程序文件打包该文件。 但是，如果要调试应用的发布版本，则应保存该文件。

可以采用任何喜欢的方式部署完整的应用程序文件集。 例如，可以使用简单的 `copy` 命令将其打包为 Zip 文件，或者使用选择的安装包进行部署。 安装成功后，用户可通过使用 `dotnet` 命令或提供应用程序文件名（如 `dotnet fdd.dll`）来执行应用程序。

除应用程序二进制文件外，安装程序还应捆绑共享框架安装程序，或在安装应用程序的过程中将其作为先决条件进行检查。  安装共享框架需要管理员/根访问权限，因为它属于计算机范围。

## <a name="framework-dependent-deployment-with-third-party-dependencies"></a>包含第三方依赖项的依赖框架的部署

要使用一个或多个第三方依赖项来部署依赖框架的部署，需要任何依赖项都可供项目使用。 在生成应用之前，还需执行以下额外步骤：

1. 使用 NuGet 包管理器向项目添加对 NuGet 包的引用；如果系统上还没有此包，请先安装它。 要打开包管理器，请选择“工具” > “NuGet 包管理器” > “管理解决方案的 NuGet 包”。

1. 确认已在系统中安装 `Newtonsoft.Json`，如果尚未安装，请先安装它。 “已安装”选项卡列出了系统中已安装的 NuGet 包。 如果此处未列出 `Newtonsoft.Json`，请选择“浏览”选项卡，然后在搜索框中输入“Newtonsoft.Json”。 选择 `Newtonsoft.Json`，在右侧窗格中选择项目，然后选择“安装”。

1. 如果系统中已安装 `Newtonsoft.Json`，请在“管理解决方案包”选项卡的右侧窗格中选择项目，将该项添加到项目。

请注意，如果依赖框架的部署具有第三方依赖项，则其可移植性只与第三方依赖项相同。 例如，如果某个第三方库只支持 macOS，该应用将无法移植到 Windows 系统。 当第三方依赖项本身取决于本机代码时，也可能发生此情况。 [Kestrel 服务器](http://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel)就是一个很好的示例，它需要 [libuv](https://github.com/libuv/libuv) 的本机依赖项。 当为具有此类第三方依赖项的应用程序创建 FDD 时，已发布的输出会针对每个本机依赖项支持（存在于 NuGet 包中）的[运行时标识符 (RID)](../rid-catalog.md) 包含一个文件夹。

## <a name="simpleSelf"></a>不包含第三方依赖项的独立部署

部署没有第三方依赖项的独立部署包括创建项目、修改 csproj 文件、生成、测试以及发布应用。 一个用 C# 编写的简单示例可说明此过程。 

1. 创建项目。

   选择“文件” > “新建” > “项目”。 在“添加新项目”对话框中，在“已安装”项目类型窗格中选择“.NET Core”，然后在中心窗格中选择“控制台应用(.NET Core)”模板。 在“名称”文本框中输入项目名称如“SCD”，然后选择“确定”按钮。

1. 添加应用程序的源代码。

   在编辑器中打开 Program.cs 文件，然后使用下列代码替换自动生成的代码。 它会提示用户输入文本，并显示用户输入的个别词。 它使用正则表达式 `\w+` 来将输入文本中的词分开。

   [!code-cs[deployment#1](../../../samples/snippets/core/deploying/deployment-example.cs)]

1. 定义应用的目标平台。

   1. 在“解决方案资源管理器”中右键单击项目（而非解决方案），然后选择“编辑 SCD.csproj”。

   1. 在 csproj 文件（该文件用于定义应用的目标平台）的 `<PropertyGroup>` 部分中创建 `<RuntimeIdentifiers>` 标记，然后指定每个目标平台的运行时标识符 (RID)。 请注意，还需要添加分号来分隔 RID。 请查看[运行时标识符目录](../rid-catalog.md)，获取运行时标识符列表。 

   例如，以下示例表明应用在 64 位 Windows 10 操作系统和 64 位 OS X 10.11 版本的操作系统上运行。

```xml
<PropertyGroup>
    <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
</PropertyGroup>
```
   请注意，`<RuntimeIdentifiers>` 元素可能会进入 csproj 文件的任何 `<PropertyGroup>` 中。 本节后面部分将显示完整的示例 csproj 文件。

1. 创建应用的调试版本。

   选择“生成” > “生成解决方案”。 也可通过选择“调试” > “开始调试”来编译和运行应用程序的调试版本。

1. 发布你的应用。

   调试并测试程序后，为应用的每个目标平台创建要与应用一起部署的文件。

   若要从 Visual Studio 发布应用，请执行以下操作：

      1. 将工具栏上的解决方案配置从“调试”更改为“发布”，生成应用的发布（而非调试）版本。

      1. 在“解决方案资源管理器”中右键单击项目（而非解决方案），然后选择“发布”。 

      1. 在“发布”选项卡上，选择“发布”。 Visual Studio 将包含应用程序的文件写入本地文件系统。

      1. “发布”选项卡现在显示单个配置文件 FolderProfile。 该配置文件的配置设置显示在选项卡的“摘要”部分。目标运行时用于标识已发布的运行时，目标位置用于标识独立部署文件的写入位置。

      1. 默认情况下，Visual Studio 将所有已发布文件写入单个目录。 为了方便起见，最好为每个目标运行时创建单个配置文件，并将已发布文件置于特定于平台的目录中。 这包括为每个目标平台创建单独的发布配置文件。 现在，请执行下列操作，为每个平台重新生成应用程序：

         1. 在“发布”对话框中选择“创建新配置文件”。

         1. 在“选取发布目标”对话框中，将“选择文件夹”位置更改为 bin\Release\PublishOutput\win10-x64。 选择“确定”。

         1. 在配置文件列表中选择新配置文件 (FolderProfile1) ，并确保“目标运行时”为 `win10-x64`。 如果不是，请选择“设置”。 在“配置文件设置”对话框中，将“目标运行时”更改为 `win10-x64`，然后选择“保存”。 否则，选择“取消”。

         1. 选择“发布”，发布 64 位 Windows 10 平台的应用。

         1. 请再次按照上述步骤创建 `osx.10.11-x64` 平台的配置文件。 “目标位置”为 bin\Release\PublishOutput\osx.10.11-x64，“目标运行时”为 `osx.10.11-x64`。 Visual Studio 分配给此配置文件的名称是 FolderProfile2。

      请注意，每个目标位置中都包含启动应用所需的完整文件集（既包含应用文件，又包含所有 .NET Core 文件）。

与应用程序的文件一起，发布过程将发出包含应用调试信息的程序数据库 (.pdb) 文件。 该文件主要用于调试异常。 可以选择不使用应用程序文件打包该文件。 但是，如果要调试应用的发布版本，则应保存该文件。

可按照任何喜欢的方式部署已发布的文件。 例如，可以使用简单的 `copy` 命令将其打包为 Zip 文件，或者使用选择的安装包进行部署。

下面是此项目完整的 csproj 文件。

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp1.1</TargetFramework>
    <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
  </PropertyGroup>
</Project>
```

## <a name="self-contained-deployment-with-third-party-dependencies"></a>包含第三方依赖项的独立部署

部署包含一个或多个第三方依赖项的独立部署包括添加依赖项。 在生成应用之前，还需执行以下额外步骤：

1. 使用 NuGet 包管理器向项目添加对 NuGet 包的引用；如果系统上还没有此包，请先安装它。 要打开包管理器，请选择“工具” > “NuGet 包管理器” > “管理解决方案的 NuGet 包”。

1. 确认已在系统中安装 `Newtonsoft.Json`，如果尚未安装，请先安装它。 “已安装”选项卡列出了系统中已安装的 NuGet 包。 如果此处未列出 `Newtonsoft.Json`，请选择“浏览”选项卡，然后在搜索框中输入“Newtonsoft.Json”。 选择 `Newtonsoft.Json`，在右侧窗格中选择项目，然后选择“安装”。

1. 如果系统中已安装 `Newtonsoft.Json`，请在“管理解决方案包”选项卡的右侧窗格中选择项目，将其添加到项目。

下面是此项目的完整 csproj 文件：

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp1.1</TargetFramework>
    <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
  </ItemGroup>
</Project>
```

部署应用程序时，应用中使用的任何第三方依赖项也包含在应用程序文件中。 运行应用的系统上不需要第三方库。

请注意，可以只将具有一个第三方库的独立部署部署到该库支持的平台。 这与依赖框架的部署中具有本机依赖项和第三方依赖项相似，其中的本机依赖项不会存在于目标平台上，除非之前在该平台上安装了该依赖项。

# <a name="see-also"></a>请参阅
[.NET Core 应用程序部署](index.md)   
[.NET Core 运行时标识符 (RID) 目录](../rid-catalog.md)   

