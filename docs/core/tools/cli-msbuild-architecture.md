---
title: ".NET Core 命令行工具体系结构"
description: "了解 .NET Core 工具层及最新版本中的更改。"
keywords: ".NET Core, MSBuild, 体系结构"
author: blackdwarf
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 7fff0f61-ac23-42f0-9661-72a7240a4456
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 6830cc46994aa44d46a9c862efff525142578003
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="high-level-overview-of-changes-in-the-net-core-tools"></a>.NET Core 工具中变更的高级概述

此文档介绍了与从 project.json 移动到 MSBuild 和 csproj 项目系统有关的更改，其中包含关于 .NET Core 工具的分层和 CLI 命令的实现的更改的信息。 这些更改与 2017 年 3 月 7 日 .NET Core SDK 1.0 和 Visual Studio 2017 的发布同时发生（请参阅[通知](https://blogs.msdn.microsoft.com/dotnet/2017/03/07/announcing-net-core-tools-1-0/)），但是最初是在 .NET Core SDK 预览 3 版本中实现的。

## <a name="moving-away-from-projectjson"></a>弃用 project.json
.NET Core 工具的最大变更无疑是[弃用 project.json，改用 csproj](https://blogs.msdn.microsoft.com/dotnet/2016/05/23/changes-to-project-json/) 作为项目系统。 最新版本的命令行工具不支持 *project.json* 文件。 这意味着它不能用于生成、运行或发布基于 project.json 的应用程序和库。 若要使用此版本的工具，需要迁移现有项目或启动新的项目。 

作为此次移动的一部分，开发用于生成 project.json 项目的自定义生成引擎被替换为一个功能完整的成熟生成引擎，即 [MSBuild](https://github.com/Microsoft/msbuild)。 MSBuild 是.NET 社区中的知名引擎，因为自该平台首个版本以来，它一直作为一项关键技术。 当然，因为它需要生成 .NET Core 应用程序，所以 MSBuild 已经移植到 .NET Core，并可在 .NET Core 运行的任何平台上使用。 .NET Core 的一个主要的好处是跨平台开发堆栈，我们已确保本次迁移不会破坏此好处。

> [!NOTE]
> 如果还不熟悉 MSBuild，并且想要了解相关详细信息，可参阅 [MSBuild 概念](/visualstudio/msbuild/msbuild-concepts)一文。 

## <a name="the-tooling-layers"></a>工具层
随着弃用现有项目系统以及改换生成引擎，自然会出现一个疑问：这些更改会改变整体 .NET Core 工具生态系统的整体“分层”吗？ 是否有新的位和组件？

首先来简要介绍下预览版 2 分层，如下图所示：

![预览版 2 工具高级体系结构](media/cli-msbuild-architecture/p2-arch.png)

这些工具的分层非常简单。 在底部，我们将 .NET Core 命令行工具作为基础。 其他所有高级工具（如 Visual Studio 或 Visual Studio Code）依靠 CLI 来生成项目、还原依赖项以及完成其他操作。 这意味着，例如，如果 Visual Studio 要执行还原操作，它会在 CLI 中调入 `dotnet restore` 命令。 

随着迁移到新的项目系统，之前的图表会更改： 

![.NET Core SDK 1.0.0 高级体系结构](media/cli-msbuild-architecture/p3-arch.png)

主要区别在于 CLI 不再作为基础层；现由“共享 SDK 组件”充当此角色。 共享 SDK 组件是一组负责编译代码、发布代码、打包 NuGet 包等操作的目标和关联任务。SDK 本身是一个开源代码，可在 GitHub 上的 [SDK 存储库](https://github.com/dotnet/sdk)中获得。 

> [!NOTE]
> “目标”是一个表示 MSBuild 可调用的已命名操作的 MSBuild 术语。 其通常伴随着执行此目标应执行的某个逻辑的一个或多个任务。 MSBuild 支持多个现成的目标，如 `Copy` 或 `Execute`；它还允许用户使用托管代码编写自己的任务，并定义要执行这些任务的目标。 有关详细信息，请参阅 [MSBuild 任务](/visualstudio/msbuild/msbuild-tasks)。 

现在所有工具集使用共享 SDK 组件及其目标，包括 CLI。 例如，下个版本的 Visual Studio 不会调用到 `dotnet restore` 命令来还原 .NET Core 项目的依赖关系，它会直接使用“还原”目标。 由于这些皆是 MSBuild 目标，因此你也可通过 [dotnet msbuild](dotnet-msbuild.md) 命令使用原始 MSBuild 来执行。 

### <a name="cli-commands"></a>CLI 命令
共享 SDK 组件意味着大部分现有 CLI 命令已重新实现为 MSBuild 任务和目标。 这对 CLI 命令和工具集的使用意味着什么？ 

从使用角度而言，它不会更改使用 CLI 的方式。 CLI 仍具有预览 2 版本中存在的核心命令：

* `new`
* `restore`
* `run` 
* `build`
* `publish`
* `test`
* `pack` 

这些命令的作用没有发生改变（仍可新建项目、生成项目、发布项目、打包项目等等）。 大部分选项并未更改，仍和以前一样。可以使用 `dotnet <command> --help` 查看相应命令的帮助屏幕，也可以参阅此网站上的文档来熟悉所有更改。 

从执行角度而言，CLI 命令会采用其参数并构造对“原始”MSBuild 的调用，从而设置所需属性和运行所需目标。 为更好的说明这点，请参考下面的命令： 

   `dotnet publish -o pub -c Release`
    
此命令会使用“发布”配置将应用程序发布到 `pub` 文件夹。 在内部，此命令会转换成下面的 MSBuild 调用： 

   `dotnet msbuild /t:Publish /p:OutputPath=pub /p:Configuration=Release`

此规则值得注意的例外是 `new` 和 `run` 命令，因为它们未实现为 MSBuild 目标。

