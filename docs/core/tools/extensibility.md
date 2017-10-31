---
title: ".NET Core CLI 扩展性模型"
description: "了解如何扩展命令行接口 (CLI) 工具。"
keywords: "CLI, 扩展性, 自定义命令, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 04/12/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: fffc3400-aeb9-4c07-9fea-83bc8dbdcbf3
ms.translationtype: HT
ms.sourcegitcommit: 434b27f6c2d44c63b4ce4deee094ac6c322cf2b5
ms.openlocfilehash: 62de584fe5d7f1029e73e4c8c5f9b428c567751a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

---

# <a name="net-core-cli-tools-extensibility-model"></a>.NET Core CLI 工具扩展性模型

本文档介绍扩展 .NET Core 命令行接口 (CLI) 工具的多种方式，并解释驱动每个方式的不同方案。
还将介绍如何使用这些工具，以及如何生成不同类型的工具。

## <a name="how-to-extend-cli-tools"></a>如何扩展 CLI 工具
主要可以通过以下三种方式扩展 CLI 工具：

1. [通过基于每个项目的 NuGet 包](#per-project-based-extensibility)

  基于项目的工具包含在项目上下文中，但允许通过还原轻松安装。

2. [通过具有自定义目标的 NuGet 包](#custom-targets)

  通过自定义目标，可使用自定义任务轻松扩展生成过程。

3. [通过系统路径](#path-based-extensibility)

  基于路径的工具非常适合可在一台计算机上使用的常规、跨项目工具。

上方列出的三种扩展性机制并不相互排斥。 可以单独使用、同时使用或结合使用。 选择何种机制很大程度上取决于希望通过扩展实现的目标。

## <a name="per-project-based-extensibility"></a>基于每个项目的扩展性
基于项目的工具是作为 NuGet 包分布的[依赖框架的部署](../deploying/index.md#framework-dependent-deployments-fdd)。 工具仅在项目的上下文中可用，这些工具被该项目引用或为该项目还原。 项目上下文外（例如，包含该项目的目录外）的调用将因无法找到命令而失败。

这些工具非常适合生成服务器，因为除项目文件外不需要任何条件。 生成过程会对所生成的项目运行还原操作，并且工具可用。 语言项目（如 F#）也属于此类别；因为只能采用某种特定语言编写每个项目。

最后，此扩展性模型支持创建需要访问项目生成输出的工具。 例如，[ASP.NET](https://www.asp.net/) MVC 应用程序中的多种 Razor 视图工具均属于此类别。

### <a name="consuming-per-project-tools"></a>使用基于项目的工具
使用这些工具要求将想要使用的每个工具的 `<DotNetCliToolReference>` 元素添加到项目文件。 在 `<DotNetCliToolReference>` 元素中，引用该工具所在的包并指定所需的版本。 运行 [`dotnet restore`](dotnet-restore.md) 后，将还原该工具及其依赖项。

对于需要加载用于执行的项目生成输出的工具，通常还有一个依赖项，它位于项目文件中的常规依赖项下。 由于 CLI 使用 MSBuild 作为其生成引擎，因此建议将该工具的这些部分作为自定义 MSBuild [目标](/visualstudio/msbuild/msbuild-targets)和[任务](/visualstudio/msbuild/msbuild-tasks)写入，以便这些部分可以参与整个生成过程。 此外，它们还可以轻松获取通过该生成产生的所有数据（例如，输出文件的位置、正在生成的当前配置等）。所有此类信息将成为一组可从任意目标中读取的 MSBuild 属性。 本文档的后面将介绍如何使用 NuGet 添加自定义目标。

我们来看看将简单的工具专用工具添加到简单项目的示例。 假定示例命令称为 `dotnet-api-search`，通过它可搜索指定 API 的所有 NuGet 包，以下是使用该工具的控制台应用程序的项目文件：

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp1.1</TargetFramework>
  </PropertyGroup>

  <!-- The tools reference -->
  <ItemGroup>
    <DotNetCliToolReference Include="dotnet-api-search" Version="1.0.0" />
  </ItemGroup>
</Project>
```

`<DotNetCliToolReference>` 元素采用与 `<PackageReference>` 元素相同的方式进行结构化。 它需要包含该工具及其可还原版本的包的包 ID。

### <a name="building-tools"></a>生成工具
如前所述，工具仅仅是可移植控制台应用程序。 可以采用与生成其他控制台应用程序类似的方式生成工具。
生成后，使用 [`dotnet pack`](dotnet-pack.md) 命令创建 NuGet 包（.nupkg 文件），其中包含代码和依赖项等相关信息。 可以随意命名包，但内部应用程序（即实际的工具二进制文件）必须遵循 `dotnet-<command>` 的约定，以便 `dotnet` 能够调用它。

> [!NOTE]
> 在低于 RC3 版本的 .NET Core 命令行工具中，`dotnet pack` 命令存在一个 bug，导致 `runtime.config.json` 无法与该工具一起打包。 缺少该文件导致发生运行时错误。 如果遇到此行为，请务必更新到最新工具，然后重试 `dotnet pack`。

由于工具是可移植应用程序，因此使用该工具的用户必须拥有生成该工具时所针对的 .NET Core 库版本，以便运行此工具。 工具使用的以及 .NET Core 库未包含的其他任何依赖项均被还原并放置在 NuGet 缓存中。 因此，使用 .NET Core 库和 NuGet 缓存中的程序集可以运行整个工具。

这些类型的工具含有依赖项关系图，它完全独立于使用这些工具的项目的依赖项关系图。 还原过程将首先还原项目的依赖项，然后还原每个工具及其依赖项。

可在 [.NET Core CLI 存储库](https://github.com/dotnet/cli/tree/rel/1.0.1/TestAssets/TestProjects)中找到有关此过程的更多示例和不同组合。
还可以在相同存储库中查看[所用工具的实现](https://github.com/dotnet/cli/tree/rel/1.0.1/TestAssets/TestPackages)。

### <a name="custom-targets"></a>自定义目标
NuGet 可将[自定义 MSBuild 目标和属性文件打包](/nuget/create-packages/creating-a-package#including-msbuild-props-and-targets-in-a-package)。 在移动 .NET Core CLI 工具以使用 MSBuild 后，会对 .NET Core 项目应用可扩展性的相同机制。 若要扩展生成过程、访问生成过程中的任何项目（如生成的文件）或检查调用生成时使用的配置等，建议使用该类型的扩展。

在下面的示例中，可看到目标的项目文件，它使用的是 `csproj` 语法。 该语法指示 [`dotnet pack`](dotnet-pack.md) 命令对哪些内容打包，以便将目标文件和程序集放在包中的 build 文件夹内。 请注意将 `Label` 属性设置为 `dotnet pack instructions` 的 `<ItemGroup>` 元素，以及在其下定义的目标。

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <Description>Sample Packer</Description>
    <VersionPrefix>0.1.0-preview</VersionPrefix>
    <TargetFramework>netstandard1.3</TargetFramework>
    <DebugType>portable</DebugType>
    <AssemblyName>SampleTargets.PackerTarget</AssemblyName>
  </PropertyGroup>
  <ItemGroup>
    <EmbeddedResource Include="Resources\Pkg\dist-template.xml;compiler\resources\**\*" Exclude="bin\**;obj\**;**\*.xproj;packages\**" />
    <None Include="build\SampleTargets.PackerTarget.targets" />
  </ItemGroup>
  <ItemGroup Label="dotnet pack instructions">
    <Content Include="build\*.targets">
      <Pack>true</Pack>
      <PackagePath>build\</PackagePath>
    </Content>
  </ItemGroup>
  <Target Name="CollectRuntimeOutputs" BeforeTargets="_GetPackageFiles">
    <!-- Collect these items inside a target that runs after build but before packaging. -->
    <ItemGroup>
      <Content Include="$(OutputPath)\*.dll;$(OutputPath)\*.json">
        <Pack>true</Pack>
        <PackagePath>build\</PackagePath>
      </Content>
    </ItemGroup>
  </Target>
  <ItemGroup>
    <PackageReference Include="Microsoft.Extensions.DependencyModel" Version="1.0.1-beta-000933"/>
    <PackageReference Include="Microsoft.Build.Framework" Version="0.1.0-preview-00028-160627" />
    <PackageReference Include="Microsoft.Build.Utilities.Core" Version="0.1.0-preview-00028-160627" />
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
  </ItemGroup>
  <ItemGroup />
  <PropertyGroup Label="Globals">
    <ProjectGuid>463c66f0-921d-4d34-8bde-7c9d0bffaf7b</ProjectGuid>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(TargetFramework)' == 'netstandard1.3' ">
    <DefineConstants>$(DefineConstants);NETSTANDARD1_3</DefineConstants>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">
    <DefineConstants>$(DefineConstants);RELEASE</DefineConstants>
  </PropertyGroup>
</Project>
```

若要使用自定义目标，请提供指向此程序包的 `<PackageReference>` 以及项目内正在进行扩展的该程序包版本。 与工具不同，自定义目标包未包含在使用项目中的依赖项结尾。

使用自定义目标仅取决于配置方式。 由于它是 MSBuild 目标，因此会依赖于给定的目标并在另一个目标后运行，也可使用 `dotnet msbuild /t:<target-name>` 命令手动调用。

但是，如果要为用户提供更好的用户体验，可以合并基于项目的工具和自定义目标。 在这种情况下，基于项目的工具实质上只需接受任何所需的参数并将其转换为执行目标所需的 [`dotnet msbuild`](dotnet-msbuild.md) 调用。 有关此类协同作用的示例，请访问 [`dotnet-packer`](https://github.com/dotnet/MVPSummitHackathon2016/tree/master/dotnet-packer) 项目中的 [2016 年编程马拉松 MVP 峰会示例](https://github.com/dotnet/MVPSummitHackathon2016)存储库。

### <a name="path-based-extensibility"></a>基于路径的扩展
基于路径的扩展常用于开发计算机，此计算机需要在概念上涵盖多个项目的工具。 此扩展机制的主要缺点在于必须将其关联到工具所在的计算机。 如果其他计算机上需要该机制，则必须对其进行部署。

此 CLI 工具集扩展的模式就非常简单。 正如 [.NET Core CLI 概述](index.md)中所述，`dotnet` 驱动程序可以运行以 `dotnet-<command>` 约定命名的任何命令。 默认的解析逻辑将首先探测多个位置，最后探测系统路径。 如果请求的命令存在于系统路径中并且属于可调用的二进制文件，则 `dotnet` 驱动程序将调用它。

文件必须是可执行的。 在 Unix 系统上，这表示通过 `chmod +x` 设置了执行位的任何内容。 在 Windows 上，可使用 cmd 文件。

来看看非常简单的“Hello World”工具的实现。 我们将在 Windows 上同时使用 `bash` 和 `cmd`。
下列命令将简单地向控制台回显“Hello World”。

```bash
#!/bin/bash

echo "Hello World!"
```

```cmd
echo "Hello World"
```

在 macOS 上，可以将此脚本另存为 `dotnet-hello` 并使用 `chmod +x dotnet-hello` 设置其可执行位。 然后，可以使用命令 `ln -s <full_path>/dotnet-hello /usr/local/bin/` 在 `/usr/local/bin` 中创建其符号链接。 这样，就可以使用 `dotnet hello` 语法调用命令。

在 Windows 上，可将此脚本另存为 `dotnet-hello.cmd`，并放在系统路径中（也可以将其添加到已位于该路径中的文件夹内）。 然后，只需使用 `dotnet hello` 即可运行此示例。

