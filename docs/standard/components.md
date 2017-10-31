---
title: ".NET 体系结构组件"
description: "描述 .NET 体系结构组件，例如 .NET Standard、.NET 实现和工具。"
author: cartermp
ms.author: mairaw
ms.date: 08/23/2017
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.translationtype: HT
ms.sourcegitcommit: 1b028e5880f9e57e87c16eabeb442e0a46a369da
ms.openlocfilehash: ce3368f4c34a8e4b20a7deb2a6c6e4d163927cd4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/23/2017

---
# <a name="net-architectural-components"></a>.NET 体系结构组件

.NET 应用开发用于并运行于一个或多个 .NET 实现。  .NET 实现包括 .NET Framework、.NET Core 和 Mono。 .NET 的所有实现都有一个名为 .NET Standard 的通用 API 规范。 本文简要介绍了每个概念。

## <a name="net-standard"></a>.NET Standard

.NET Standard 是一组由 .NET 实现的基类库实现的 API。 更正式地说，它是构成协定统一集（这些协定是编写代码的依据）的特定 .NET API 组。 这些协定在每个 .NET 实现中实现。 这可实现不同 .NET 实现间的可移植性，有效地使代码可在任何位置运行。

.NET Standard 也是一个[目标框架](glossary.md#target-framework)。 如果代码面向 .NET Standard 版本，则它可在支持该 .NET Standard 版本的任何 .NET 实现上运行。

若要详细了解 .NET Standard 以及如何将其作为目标，请参阅 [.NET Standard](net-standard.md) 主题。

## <a name="net-implementations"></a>.NET 实现

.NET 的每个实现都具有以下组件：

- 一个或多个运行时。 示例：用于 .NET Framework 的 CLR、CoreCLR 和用于 .NET Core 的 CoreRT。
- 实现 .NET Standard 并且可实现其他 API 的类库。 示例：.NET Framework 基类库、.NET Core 基类库。
- 可选择包含一个或多个应用程序框架。 示例： [ASP.NET](https://www.asp.net/)、[Windows 窗体](../framework/winforms/windows-forms-overview.md)和 [Windows Presentation Foundation (WPF)](../framework/wpf/index.md) 包含在 .NET Framework 中。
- 可包含开发工具。 某些开发工具在多个实现之间共享。

Microsoft 积极开发和维护的主要 .NET 实现有 4 个：.NET Core、.NET Framework、Mono 和 UWP。

### <a name="net-core"></a>.NET 核心

.NET Core 是 .NET 的跨平台实现，专用于处理大规模的服务器和云工作负荷。 可在 Windows、macOS 和 Linux 上运行。 它实现 .NET Standard，因此面向 .NET Standard 的代码都可在 .NET Core 上运行。 ASP.NET Core 在 .NET Core 上运行。 

要了解有关 .NET Core 的详细信息，请参阅 [.NET Core 指南](../core/index.md)和[为服务器应用选择 .NET Core 或 .NET Framework](choosing-core-framework-server.md)。

### <a name="net-framework"></a>.NET Framework

.Net Framework 是自 2002 年起就已存在的原始 .NET 实现。 它是当前 .NET 开发人员经常使用的 .NET Framework。 4.5 版以及更高版本实现 .NET Standard，因此面向 .NET Standard 的代码都可在这些版本的 .NET Framework 上运行。 它还包含一些特定于 Windows 的 API，如通过 Windows 窗体和 WPF 进行 Windows 桌面开发的 API。 .NET Framework 非常适合用于生成 Windows 桌面应用程序。

若要了解有关 .NET Framework 的详细信息，请参阅 [.NET Framework 指南](../framework/index.md)。

### <a name="mono"></a>Mono

Mono 是主要在需要小型运行时使用的 .NET 实现。 它是在 Android、Mac、iOS、tvOS 和 watchOS 上驱动 Xamarin 应用程序的运行时，且主要针对小内存占用。

它支持所有当前已发布的 .NET Standard 版本。

以前，Mono 实现更大的 .NET Framework API 并模拟一些 Unix 上最常用的功能。 有时使用它运行依赖 Unix 上的这些功能的 .NET 应用程序。

Mono 通常与实时编译器一起使用，但它也提供在 iOS 之类的平台使用的完整静态编译器（预先编译）。

若要了解有关 Mono 的详细信息，请参阅 [Mono 文档](http://www.mono-project.com/docs/)。

### <a name="universal-windows-platform-uwp"></a>通用 Windows 平台 (UWP)

UWP 是用于为物联网 (IoT) 生成新式触控 Windows 应用程序和软件的 .NET 实现。 它旨在统一可能想要以其为目标的不同类型的设备，包括电脑、平板电脑、平板手机、电话，甚至 Xbox。 UWP 提供许多服务，如集中式应用商店、执行环境 (AppContainer) 和一组 Windows API（用于代替 Win32 (WinRT)）。 应用可采用 C++、C#、VB.NET 和 JavaScript 编写。 使用 C# 和 VB.NET 时，.NET API 由 .NET Core 提供。

若要详细了解 UWP，请参阅[通用 Windows 平台简介](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)。

## <a name="net-runtimes"></a>.NET 运行时

运行时是用于托管程序的执行环境。 OS 属于运行时环境，但不属于 .NET 运行时。 下面是 .NET 运行时的一些示例：
 
 - .NET Framework 公共语言运行时 (CLR)
 - .NET Core 核心公共语言运行时 (CoreCLR)
 - 适用于通用 Windows 平台的 .NET Native 
 - 用于 Xamarin.iOS、Xamarin.Android、Xamarin.Mac 和 Mono 桌面框架的 Mono 运行时

## <a name="net-tooling-and-common-infrastructure"></a>.NET 工具和常见基础结构

可访问一整套适用于每种 .NET 实现的工具和基础结构组件。 包括（但不限于）以下几种：

- .NET 语言及其编译器
- .NET 项目系统（基于 .csproj.vbproj 和 .fsproj 文件）
- [MSBuild](/visualstudio/msbuild/msbuild)（用于生成项目的生成引擎）
- [NuGet](/nuget/)（适用于.NET 的 Microsoft 程序包管理器）
- 开放源生成业务流程工具，例如 [CAKE](http://cakebuild.net/) 和 [FAKE](https://fake.build/)

## <a name="see-also"></a>请参阅
[为服务器应用选择 .NET Core 或 .NET Framework](choosing-core-framework-server.md)   
[.NET Standard](net-standard.md)  
[.NET Core 指南](../core/index.md)  
[.NET Framework 指南](../framework/index.md)  
[C# 指南](../csharp/index.md)  
[F# 指南](../fsharp/index.md)  
[VB.NET 指南](../visual-basic/index.md)  


