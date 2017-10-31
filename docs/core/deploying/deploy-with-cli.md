---
title: "使用 CLI 工具部署 .NET Core 应用"
description: "了解如何使用命令行接口 (CLI) 工具部署 .NET Core 应用"
keywords: ".NET、.NET Core、.NET Core 部署"
author: rpetrusha
ms.author: ronpet
ms.date: 04/18/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 82ebe16d-5e1c-46cc-91e8-71974296429c
ms.translationtype: HT
ms.sourcegitcommit: b647c5dc4e565f9813212d75fab4a2e46c1a47b9
ms.openlocfilehash: 3d799c6f824bd5cf08c0e939b069a21092395268
ms.contentlocale: zh-cn
ms.lasthandoff: 09/12/2017

---

# <a name="deploying-net-core-apps-with-command-line-interface-cli-tools"></a>使用命令行接口 (CLI) 工具部署 .NET Core 应用

可将 .NET Core 应用程序部署为依赖框架的部署或独立部署，前者包含应用程序二进制文件，但依赖目标系统上存在的 .NET Core，而后者同时包含应用程序和 .NET Core 二进制文件。 请参阅 [.NET Core 应用程序部署](index.md)了解相关概述。

以下各节演示如何使用 [.NET Core 命令行接口工具](../tools/index.md)创建下列各类部署：

- 依赖框架的部署
- 包含第三方依赖项的依赖框架的部署
- 独立部署
- 包含第三方依赖项的独立部署

从命令行工作时，可使用所选的程序编辑器。 如果使用的程序编辑器是 [Visual Studio Code](https://code.visualstudio.com)，则可通过选择“视图” > “集成终端”打开 Visual Studio Code 环境中的命令控制台。

## <a name="framework-dependent-deployment"></a>依赖框架的部署

如果不使用第三方依赖项，部属依赖框架的部署只包括生成、测试和发布应用。 一个用 C# 编写的简单示例可说明此过程。 

1. 创建项目目录。

   为项目创建一个目录，并将其设为当前目录。

1. 创建项目。

   在命令栏行中，键入 [dotnet new console](../tools/dotnet-new.md)，在该目录中创建新的 C# 控制台项目。

1. 添加应用程序的源代码。

   在编辑器中打开 Program.cs 文件，然后使用下列代码替换自动生成的代码。 它会提示用户输入文本，并显示用户输入的个别词。 它使用正则表达式 `\w+` 来将输入文本中的词分开。

   [!code-cs[deployment#1](../../../samples/snippets/core/deploying/deployment-example.cs)]

1. 更新项目的依赖项和工具。
 
   运行 [dotnet 还原](../tools/dotnet-restore.md)命令，以还原项目中指定的依赖项。

1. 创建应用的调试版本。

   使用 [dotnet 生成](../tools/dotnet-build.md)命令生成应用程序，或使用 [dotnet 运行](../tools/dotnet-run.md)命令生成并运行应用程序。

1. 部署应用。

   完成程序调试和测试后，使用下列命令创建部署：

      ```console
      dotnet publish -f netcoreapp1.1 -c Release
      ```
   这将创建一个应用的发行版（而不是调试版）。 生成的文件位于名为“发布”的目录中，该目录位于项目的 bin 目录的子目录中。

与应用程序的文件一起，发布过程将发出包含应用调试信息的程序数据库 (.pdb) 文件。 该文件主要用于调试异常。 可以选择不将其与应用程序的文件一起分布。 但是，如果要调试应用的发布版本，则应保存该文件。

可以采用任何喜欢的方式部署完整的应用程序文件集。 例如，可以使用简单的 `copy` 命令将其打包为 Zip 文件，或者使用选择的安装包进行部署。 安装成功后，用户可通过使用 `dotnet` 命令或提供应用程序文件名（如 `dotnet fdd.dll`）来执行应用程序。

除应用程序二进制文件外，安装程序还应捆绑共享框架安装程序，或在安装应用程序的过程中将其作为先决条件进行检查。  安装共享框架需要管理员/根访问权限。

## <a name="framework-dependent-deployment-with-third-party-dependencies"></a>包含第三方依赖项的依赖框架的部署

要使用一个或多个第三方依赖项来部署依赖框架的部署，需要这些依赖项都可供项目使用。 在运行 `dotnet restore` 命令之前，还需执行额外两个步骤：

1. 向 csproj 文件的 `<ItemGroup>` 部分添加对所需第三方库的引用。 以下 `<ItemGroup>` 部分包含 [Json.NET](http://www.newtonsoft.com/json) 的依赖项（作为第三方库）：

      ```xml
      <ItemGroup>
        <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
      </ItemGroup>
      ```

1. 如果尚未安装，请下载包含第三方依赖项的 NuGet 包。 若要下载该包，请在添加依赖项后执行 `dotnet restore` 命令。 因为依赖项在发布时已从本地 NuGet 缓存解析出来，因此它一定适用于你的系统。

请注意，如果依赖框架的部署具有第三方依赖项，则其可移植性只与第三方依赖项相同。 例如，如果某个第三方库只支持 macOS，该应用将无法移植到 Windows 系统。 当第三方依赖项本身取决于本机代码时，也可能发生此情况。 [Kestrel 服务器](/aspnet/core/fundamentals/servers/kestrel)就是一个很好的示例，它需要 [libuv](https://github.com/libuv/libuv) 的本机依赖项。 当为具有此类第三方依赖项的应用程序创建 FDD 时，已发布的输出会针对每个本机依赖项支持（存在于 NuGet 包中）的[运行时标识符 (RID)](../rid-catalog.md) 包含一个文件夹。

## <a name="simpleSelf"></a>不包含第三方依赖项的独立部署

部署没有第三方依赖项的独立部署包括创建项目、修改 csproj 文件、生成、测试以及发布应用。 一个用 C# 编写的简单示例可说明此过程。 该示例演示如何使用命令行中的 [dotnet 实用工具](../tools/dotnet.md)创建独立部署。

1. 为项目创建目录。

   为项目创建一个目录，并将其设为当前目录。

1. 创建项目。

   在命令栏行中，键入 [dotnet new console](../tools/dotnet-new.md)，在该目录中创建新的 C# 控制台项目。

1. 添加应用程序的源代码。

   在编辑器中打开 Program.cs 文件，然后使用下列代码替换自动生成的代码。 它会提示用户输入文本，并显示用户输入的个别词。 它使用正则表达式 `\w+` 来将输入文本中的词分开。

   [!code-cs[deployment#1](../../../samples/snippets/core/deploying/deployment-example.cs)]

1. 定义应用的目标平台。

   在 csproj 文件（该文件用于定义应用的目标平台）的 `<PropertyGroup>` 部分中创建 `<RuntimeIdentifiers>` 标记，然后指定每个目标平台的运行时标识符 (RID)。 请注意，还需要添加分号来分隔 RID。 请查看[运行时标识符目录](../rid-catalog.md)，获取运行时标识符列表。 

   例如，以下 `<PropertyGroup>` 部分表明应用在 64 位 Windows 10 操作系统和 64 位 OS X 10.11 版本的操作系统上运行。

     ```xml
     <PropertyGroup>
         <RuntimeIdentifiers>win10-x64;osx.10.11-x64</RuntimeIdentifiers>
     </PropertyGroup>
     ```

   请注意，`<RuntimeIdentifiers>` 元素可能出现在 csproj 文件的任何 `<PropertyGroup>` 中。 本节后面部分将显示完整的示例 csproj 文件。

1. 更新项目的依赖项和工具。

   运行 [dotnet 还原](../tools/dotnet-restore.md)命令，以还原项目中指定的依赖项。

1. 创建应用的调试版本。

   在命令行中，使用 [dotnet 生成](../tools/dotnet-build.md)命令。

1. 调试并测试程序后，为应用的每个目标平台创建要与应用一起部署的文件。

   同时对两个目标平台使用 `dotnet publish` 命令，如下所示：

      ```console
      dotnet publish -c Release -r win10-x64
      dotnet publish -c Release -r osx.10.11-x64
      ```

   这将为每个目标平台创建一个应用的发行版（而不是调试版）。 生成的文件位于名为“发布”的子目录中，该子目录位于项目的 .\bin\Release\netcoreapp1.1\<runtime_identifier> 子目录的子目录中。 请注意，每个子目录中都包含完整的启动应用所需的文件集（既有应用文件，也有所有 .NET Core 文件）。

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

部署包含一个或多个第三方依赖项的独立部署包括添加依赖项。 在运行 `dotnet restore` 命令之前，还需执行额外两个步骤：

1. 将对任何第三方库的引用添加到 csproj 文件的 `<ItemGroup>` 部分。 以下 `<ItemGroup>` 部分使用 Json.NET 作为第三方库。

    ```xml
      <ItemGroup>
        <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
      </ItemGroup>
    ```

1. 如果尚未安装，请将包含第三方依赖项的 NuGet 包下载到系统。 若要使依赖项对应用适用，请在添加依赖项后执行 `dotnet restore` 命令。 因为依赖项在发布时已从本地 NuGet 缓存解析出来，因此它一定适用于你的系统。

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

请注意，可以只将具有一个第三方库的独立部署部署到该库支持的平台。 这与依赖框架的部署中具有本机依赖项和第三方依赖项相似，其中的本机依赖项必须与部署应用的平台兼容。

# <a name="see-also"></a>请参阅

[.NET Core 应用程序部署](index.md)   
[.NET Core 运行时标识符 (RID) 目录](../rid-catalog.md)   

