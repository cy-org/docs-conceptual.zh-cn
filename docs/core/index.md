---
title: ".NET Core 指南"
description: ".NET Core 是一种用于创建 Windows、Linux 和 Mac 应用的模块式高性能的 .NET 实现。 了解 .NET Core 以开始使用。"
keywords: .NET, .NET Core
author: richlander
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: f2b312cb-f80c-4b0d-9101-93908f06a6fa
ms.translationtype: HT
ms.sourcegitcommit: 9f2128080d34e78733cec926e59ee5dbe9b98a0d
ms.openlocfilehash: 14e72dad71b8d99cea947e14f2ac77aedcfb5672
ms.contentlocale: zh-cn
ms.lasthandoff: 08/07/2017

---

# <a name="net-core-guide"></a>.NET Core 指南

> 请查看[“入门”教程](get-started.md)，了解如何创建简单的 .NET Core 应用程序。 只需几分钟即可生成并运行第一个应用。

.NET Core 是一个通用开发平台，由 Microsoft 和 [GitHub](https://github.com/dotnet/core) 上的 .NET 社区共同维护。 它是跨平台的，支持 Windows、macOS 和 Linux，并且可用于设备、云和嵌入式/IoT 方案。 

以下特征对 .NET Core 进行了最好的定义：

- **部署灵活：**可以包含在应用或已安装的并行用户或计算机范围中。
- **跨平台：**可以在 Windows、macOS 和 Linux 上运行；也可移植到其他操作系统。 Microsoft、其他公司和个人提供的[支持的操作系统 (OS)](https://github.com/dotnet/core/blob/master/roadmap.md)、CPU 和应用程序方案会随着时间推移而增多。
- **命令行工具：**可在命令行中执行所有产品方案。 
- **兼容性：**.NET Core 通过 [.NET 标准](../standard/net-standard.md)与 .NET Framework、Xamarin 和 Mono 兼容。
- **开放源：**.NET Core 是一个开放源平台，使用 MIT 和 Apache 2 许可证。 文档由 [CC-BY](https://creativecommons.org/licenses/by/4.0/) 许可发行。 .NET Core 是一个 [.NET Foundation](https://dotnetfoundation.org/) 项目。
- **由 Microsoft 支持：**.NET Core 由 Microsoft 依据 [.NET Core 支持](https://www.microsoft.com/net/core/support/)提供支持

## <a name="composition"></a>撰写

.NET Core 包括以下部分：

- [.NET 运行时](https://github.com/dotnet/coreclr)：提供类型系统、程序集加载、垃圾回收器、本机互操作和其他基本服务。 
- 一组 [框架库](https://github.com/dotnet/corefx)：提供基元数据类型、应用编写类型和基本实用程序。 
- 一组 [SDK 工具](https://github.com/dotnet/cli)和[语言编译器](https://github.com/dotnet/roslyn)：提供基本的开发人员体验，可用于 [.NET Core SDK](sdk.md)。
- “dotnet”应用主机，用于启动 .NET Core 应用。 它选择运行时并托管运行时，提供程序集加载策略来启动应用。 同一主机还可用于以大致相同的方式启动 SDK 工具。

### <a name="languages"></a>语言

可以使用 C# 和 F# 语言（即将推出 Visual Basic）编写 .NET Core 的应用程序和库。 在 .NET Core 上运行的编译器可以在其运行的任何地方进行 .NET Core 开发。 一般情况下，不会直接使用编译器，但会间接使用 SDK 工具。

C# 和 F# 编译器以及 .NET Core 工具已集成到或可以集成到多个文本编辑器和 IDE 中，包括 Visual Studio、[Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) 和 Sublime Text 以及 Vim，使 .NET Core 开发可以在你钟爱的环境和 OS 中进行。 这种集成部分由 [OmniSharp 项目](http://www.omnisharp.net/)的高手提供。

### <a name="net-apis-and-compatibility"></a>.NET API 和兼容性

可将 .NET Core 看作是 .NET Framework 在 .NET Framework 基类库 (BCL) 的跨平台版本。 它实施 [.NET 标准](../standard/net-standard.md)规范。 .NET Core 提供了一个可用于 .NET Framework 或 Mono/Xamarin 的 API 子集。 在某些情况下，类型未完全实现（某些成员不可用或已移动）。

有关 .NET Core API 的详细信息，请参阅 [.NET Core roadmap](https://github.com/dotnet/core/blob/master/roadmap.md)（.NET Core API 产品系列）。

### <a name="relationship-to-net-standard"></a>与 .NET Standard 的关系

[.NET 标准](../standard/net-standard.md)是一种 API 规范，用于描述开发者可以在每个 .NET 实现代码中使用的一组一致 .NET API。 .NET 实现需要实现此规范才能被视为符合 .NET Standard ，并且才能支持面向 .NET Standard 的库。 

由于 .NET Core 可实现 .NET Standard，因此也支持 .NET Standard 库。

### <a name="workloads"></a>工作负载

就本身而言，.NET Core 包括单个应用程序模型（控制台应用），这对工具、本地服务和基于文本的游戏很有用。 除 .NET Core 外，还生成了其他应用程序模型以扩展其功能，例如：

- [ASP.NET Core](/aspnet/core/)
- [Windows 10 通用 Windows 平台 (UWP)](https://developer.microsoft.com/windows)
- [定位 UWP 时的 Xamarin.Forms](https://www.xamarin.com/forms)

### <a name="open-source"></a>开放源

[.NET Core](https://github.com/dotnet/core) 属于开放源（MIT 许可证），由 Microsoft 于 2014 年提供给 [.NET Foundation](https://dotnetfoundation.org)。 现在它是最活跃的 .NET Foundation 项目之一。 可由个人和企业自由采用，包括用于个人、学术或商业目的。 许多公司已使用 .NET Core 作为应用、工具、新平台和托管服务的一部分。 其中某些公司对 GitHub 上的 .NET Core 做出了巨大贡献，并作为 [.NET Foundation Technical Steering Group](https://dotnetfoundation.org/blog/tsg-welcome)（.NET Foundation 技术控制组）的成员，指导产品方向。

## <a name="acquisition"></a>获取

.NET Core 主要以两种方式发行，以包方式在 NuGet.org 上发行，以及以独立方式发行。

### <a name="distributions"></a>分布

可以在 [.NET Core 入门](https://www.microsoft.com/net/core)页下载 .NET Core。

- *Microsoft.NET Core* 分发包括 CoreCLR 运行时、关联库、控制台应用程序主机和 `dotnet` 应用启动器。 相关描述请参见 [`Microsoft.NETCore.App`](https://www.nuget.org/packages/Microsoft.NETCore.App) 元包。
- *Microsoft .NET Core SDK* 分发包括 .NET Core 和一套用来还原 NuGet 数据包以及编译并生成应用的工具。 

通常情况下，将首先安装 .NET Core SDK，以开始 .NET Core 开发。 可以选择安装其他 .NET Core 版本（可以是预发行版）。

### <a name="packages"></a>包

- [.NET Core 包](packages.md)包含 .NET Core 运行时和库（引用程序集和实现）。 例如，[System.Net.Http](https://www.nuget.org/packages/System.Net.Http/)。
- [.NET Core 元包](packages.md)通过引用相应的带有版本的库包组合来描述各个层和应用模型。

## <a name="architecture"></a>体系结构

.NET Core 是一个跨平台的 .NET 实现。 .NET Core 特有的主要体系结构是为支持的平台提供特定于平台的实现。

### <a name="environments"></a>环境

.NET Core 由 Microsoft 在 Windows、macOS 和 Linux 上提供支持。 在 Linux 上，Microsoft 主要支持 Red Hat Enterprise Linux (RHEL) 和 Debian 分发系列上运行的 .NET Core。

.NET Core 目前支持 X64 CPU。 在 Windows 上，也支持 X86。 将支持 ARM64 和 ARM32。

有关工作负荷和 OS 以及 CPU 环境支持和计划的更详细信息，请参阅 [.NET Core Roadmap](https://github.com/dotnet/core/blob/master/roadmap.md)（.NET Core 产品系列）。

对于其他应用类型和环境，其他公司或团体可能支持 .NET Core。

### <a name="designed-for-adaptability"></a>针对适应性而设计

与其他 .NET 产品相比，生成的 .NET Core 与它们十分类似，但具有唯一性。 其目的是能够适应广泛的新平台、新的工作负荷和新的编译器工具链。 它有多个 OS 和 CPU 端口正在使用中，并可以移植到更多端口。 以 [LLILC](https://github.com/dotnet/llilc) 项目为例，它是早期 .NET Core 通过 [LLVM](http://llvm.org/) 编译器进行本地编译的原型。

该产品分为几个部分，使各个部件能够根据不同的计划适应新的平台。 必须将运行时和特定于平台的基础库作为一个单元进行移植。 与平台无关的库应在所有平台上按照构建的原样运行。 对于通过减少特定于平台的实现以提高开发人员效率方面，项目存在偏差，但每当可以以此方式全部或部分实现算法或 API 时，都应首选与平台无关的 C# 代码。

人们经常会问，为支持多个操作系统应如何实现 .NET Core。 他们还会问是否存在单独的实现，或是否使用 [conditional compilation](https://en.wikipedia.org/wiki/Conditional_compilation)（条件编译）。 这两者都在用，但强烈偏向条件编译。

可以在下面的图表看出大多数 [CoreFX](https://github.com/dotnet/corefx) 都是与平台无关的代码，该代码可在所有平台共享。 不限平台的代码可实现为在所有平台上使用的单个可移植程序集。

![CoreFX：每个平台的代码行数](../images/corefx-platforms-loc.png)

Windows 和 Unix 实现大小相似。 Windows 具有较大的实现，因为 CoreFX 实现了某些仅适用于 Windows 的功能，如 [Microsoft.Win32.Registry](https://github.com/dotnet/corefx/tree/master/src/Microsoft.Win32.Registry)，但尚未实现任何仅适用于 Unix 的概念。 你将发现大多数 Linux 和 macOS 实现都是在 Unix 实现中实现的，而特定于 Linux 和 macOS 的实现大小大致相同。


.NET Core 中混合存在特定于平台和与平台无关的库。 可以查看几个示例中的模式：

- [CoreCLR](https://github.com/dotnet/coreclr) 是特定于平台的。 它是使用 C/C++ 生成的，因此根据构造，它是特定于平台的。
- 考虑到每个 OS 上的存储和加密 API 具有显著差异，[System.IO](https://github.com/dotnet/corefx/tree/master/src/System.IO) 和 [System.Security.Cryptography.Algorithms](https://github.com/dotnet/corefx/tree/master/src/System.Security.Cryptography.Algorithms) 是特定于平台的。 
- 考虑到它们是通过数据结构创建和操作，[System.Collections](https://github.com/dotnet/corefx/tree/master/src/System.Collections) 和 [System.Linq](https://github.com/dotnet/corefx/tree/master/src/System.Linq) 是与平台无关的。

## <a name="comparisons-to-other-net-implementations"></a>与其他 .NET 实现比较

将 .NET Core 与现有的 .NET 实现进行比较，这可能是了解其大小和形状最简单的方法。 

### <a name="comparison-with-net-framework"></a>与 .NET Framework 比较

.NET 由 Microsoft 于 2000 年首次发布，而后发展至今。 15 年多以来，.NET Framework 一直是 Microsoft 出品的主要 .NET 实现。 

.NET Core 和 .NET Framework 的主要差异在于： 

- **应用模型** -- .NET Core 不支持所有 .NET Framework 应用模型，某种程序上是因为其中许多模型都是基于 Windows 技术，如 WPF（基于 DirectX 生成）。 但 .NET Core 和 .NET Framework 两者都支持控制台和 ASP.NET Core 应用模型。 
- **API** -- .NET Core 包含很多与 .NET Framework 相同，但数量较少的 API，并且具有不同的组成要素（程序集名称不同；关键用例中的类型形状不同）。 目前，这些差异通常都需要更改，以将源移植到 .NET Core。 .NET Core 实现 [.NET 标准](../standard/net-standard.md) API，随着时间的推移，将包含更多 .NET Framework BCL API。
- **子系统** -- .NET Core 实现 .NET Framework 中子系统的子级，目的是实现更简单的实现和编程模型。 例如，不支持代码访问安全性 (CAS)，但支持反射。
- **平台** -- .NET Framework 支持 Windows 和 Windows Server，而 NET Core 还支持 macOS 和 Linux。
- **开放源** -- .NET Core 属于开放源，而 [.NET Framework 的只读子集](https://github.com/microsoft/referencesource)属于开放源。

虽然 .NET Core 是唯一的且与 .NET Framework 和其他 .NET 实现大不相同，但使用源或二进制共享技术分享代码仍很简单。 

### <a name="comparison-with-mono"></a>与 Mono 比较

[Mono](http://www.mono-project.com/) 是原始的跨平台和 [开放源](https://github.com/mono/mono) .NET 实现，于 2004 年首次发布。 可以把它看作是 .NET Framework 的社区克隆。 Mono 项目团队依赖于 Microsoft 发布的开放 [.NET 标准](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/dotnet-standards.md)（尤其是 ECMA 335），以便实现兼容性。

.NET Core 和 Mono 的主要差异在于：

- **应用模型** -- Mono 通过 Xamarin 产品支持 .NET Framework 应用模型（例如，Windows Forms）和其他应用模型（例如，[Xamarin.iOS](https://www.xamarin.com/platform)）的子集。 而 .NET Core 不支持这些内容。
- **API** -- Mono 使用相同程序集名称和组成要素支持 .NET Framework API 的 [大型子集](http://docs.go-mono.com/?link=root%3a%2fclasslib)。
- **平台** -- Mono 支持很多平台和 CPU。
- **开放源** -- Mono 和 .NET Core 两者都使用 MIT 许可证，且都属于 .NET Foundation 项目。
- **焦点** --最近几年，Mono 的主要焦点是移动平台，而 .NET Core 的焦点是云工作负荷。

