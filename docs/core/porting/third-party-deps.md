---
title: "移植到 .NET Core - 分析第三方依赖项"
description: "移植到 .NET Core - 分析第三方依赖项"
keywords: .NET, .NET Core
author: cartermp
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: b446e9e0-72f6-48f6-92c6-70ad0ce3f86a
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: a074978f2817abafa7b8a9fefe7c67c9c52195b3
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="porting-to-net-core---analyzing-your-third-party-party-dependencies"></a>移植到 .NET Core - 分析第三方依赖项

移植过程的第一步是了解第三方依赖项。  需要找出尚未在 .NET Core 上运行的依赖项（如果有），并为这些没有在 .Net Core 上运行的依赖项制定应变计划。

## <a name="prerequisites"></a>先决条件

今天，本文假定使用 Windows 和 Visual Studio，并拥有在 .NET Framework 上运行的代码。

## <a name="analyzing-nuget-packages"></a>分析 NuGet 包

分析 NuGet 包的可移植性非常简单。  因为 NuGet 包本身是一组包含特定于平台的程序集的文件夹，因此仅需检查确认是否存在包含 .NET Core 程序集的文件夹即可。

检查 NuGet 包文件夹最简单的方法是使用 [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) 工具。  以下是使用方法。

1. 下载并打开 NuGet Package Explorer。
2. 单击“从在线源打开包”。
3. 搜索包的名称。
4. 展开右侧的“lib”文件夹并查看文件夹名称。

还可以在该包页面的“依赖项”部分下的 [nuget.org](https://www.nuget.org/) 上查看包所支持的内容。

无论哪种情况都需要在 [nuget.org](https://www.nuget.org/) 上查找具有以下任何名称的文件夹或项：

```
netstandard1.0
netstandard1.1
netstandard1.2
netstandard1.3
netstandard1.4
netstandard1.5
netstandard1.6
netcoreapp1.0
portable-net45-win8
portable-win8-wpa8
portable-net451-win81
portable-net45-win8-wpa8-wpa81
```

这些是映射到 [.NET Standard](../../standard/net-standard.md) 版本的目标框架名字对象 (TFM) 以及与 .NET Core 兼容的传统可移植类库 (PCL) 配置文件。  请注意，兼容的 `netcoreapp1.0` 适用于应用程序，而非库。  尽管使用基于 `netcoreapp1.0` 的库没有任何不妥，但该库可能不适用于*不是*由其他 `netcoreapp1.0` 应用程序所使用的任何内容。

.NET Core 预发行版本中使用的某些旧 TFM 也可能兼容：

```
dnxcore50
dotnet5.0
dotnet5.1
dotnet5.2
dotnet5.3
dotnet5.4
dotnet5.5
```

**尽管这些可能适用于代码，但不保证其兼容性**。  使用预发行的 .NET Core 包生成内含这些 TFM 的包。  请注意此类包更新为基于 `netstandard` 的包的情况。

> [!NOTE]
> 若要使用以传统 PCL 或预发行的 .NET Core 目标为目标的包，必须使用 `project.json` 文件中的 `imports` 指令。

### <a name="what-to-do-when-your-nuget-package-dependency-doesnt-run-on-net-core"></a>NuGet 包依赖项未在.NET Core 上运行时应执行的操作

如果所依赖的 NuGet 包无法在 .NET Core 上运行，可以执行以下几项操作。

1. 如果项目是开放源代码并托管在诸如 GitHub 中，则可以直接与开发人员交流。
2. 可以通过搜索包并单击该包页面左侧的“联系所有者”即可直接在 [nuget.org](https://www.nuget.org/) 上与作者取得联系。
3. 可以查找在.NET Core 上运行的其他包，这些包与所使用的包进行的是相同的任务。
4. 可以尝试自己编写包所执行的代码。
5. 可以通过更改应用的功能来清除对包的依赖性，至少在该包有可用的兼容性版本之前都能这样做。

请记住，开放源代码项目维护者和 NuGet 包发布者通常是因对给定域感兴趣且拥有不同的正常工作而免费参与的志愿者。 如果确实要参与，可能首先需要写一份关于库的积极声明，然后才能咨询有关 .NET Core 支持团队的内容。

如果采取上述任何操作都无法解决问题，则可能需要移植到最近版本的 .NET Core。

.NET 团队需要了解下次使用.NET Core 时哪些是需要支持的最重要的库。 还可发送邮件到 dotnet@microsoft.com，告知我们希望使用的库。

## <a name="analyzing-dependencies-which-arent-nuget-packages"></a>分析不是 NuGet 包的依赖项

用户可能拥有不是 NuGet 包的依赖项，如文件系统中的 DLL。  因此确定依赖项是否可移植的唯一方法是运行 [ApiPort 工具](https://github.com/Microsoft/dotnet-apiport/blob/master/docs/HowTo/)。

## <a name="next-steps"></a>后续步骤

若要移植库，请参阅 [Porting your Libraries](libraries.md)（移植库）。

