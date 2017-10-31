---
title: ".NET 可移植性分析器 - .NET | Microsoft Docs"
description: "了解如何使用 .NET 可移植性分析器工具来评估代码在各种 .NET 实现中的可移植性。"
keywords: ".NET、.NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 07/26/2017
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 0375250f-5704-4993-a6d5-e21c499cea1e
ms.translationtype: HT
ms.sourcegitcommit: 3155295489e1188640dae5aa5bf9fdceb7480ed6
ms.openlocfilehash: adb1971c14c8ff8c147dba378ae0e9a5bc0fb5ad
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---

# <a name="the-net-portability-analyzer"></a>.NET 可移植性分析器

想要让你的库在多个平台上使用？ 想要了解使应用程序与其他 .NET 实现兼容需要花费多大的精力？ [.NET 可移植性分析器](http://go.microsoft.com/fwlink/?LinkID=507467)工具可通过分析程序集，详细报告程序在各种 .NET 实现上的灵活性。 可移植性分析器以 Visual Studio 扩展和控制台应用的形式提供。

## <a name="new-targets"></a>新目标

* [.NET Core](https://dotnetfoundation.org/net-core)：采用模块化设计，可并行工作，面向跨平台方案。 可并行工作意味着无需破坏其他应用即可采用新的 .NET Core 版本。
* [ASP.NET Core](https://dotnetfoundation.org/asp-net-core)：构建在 .NET Core 基础之上的新型 Web 框架，为开发人员提供与 .NET Core 相同的优势。
* [通用 Windows 平台](https://blogs.msdn.microsoft.com/dotnet/2014/04/24/net-native-performance)：使用 .NET Native 的静态编译，提高 x64 和 ARM 计算机上运行的 Windows 应用商店应用的性能。 
* .NET Core + 平台扩展：除 WCF、ASP.NET Core、FSharp 和 Azure 等 .NET 生态系统中的其他 API 外还包括 .NET Core API。
* .NET Standard + 平台扩展：除 WCF、ASP.NET Core、FSharp 和 Azure 等 .NET 生态系统中的其他 API 外还包括 .NET Standard API。

## <a name="how-to-use-portability-analyzer"></a>如何使用可移植性分析器

若要开始使用 .NET 可移植性分析器，首先需要从 [Visual Studio 库](http://go.microsoft.com/fwlink/?LinkID=507467)下载相应的扩展。 它适用于 Visual Studio 2015 和 Visual Studio 2017。 可以在 Visual Studio 中转到“分析” > “可移植性分析器设置”并选择目标平台，对可移植性分析器进行配置。

![可移植性屏幕截图](./media/portability-analyzer/portability-screenshot.png)

若要分析整个项目，请在“解决方案资源管理器”中右键单击该项目，然后选择“分析程序集可移植性”。 也可以转到“分析”菜单，选择“分析程序集可移植性”。 在该位置选择项目的可执行文件或 DLL。

![可移植性解决方案资源管理器](./media/portability-analyzer/portability-solution-explorer.png)

运行分析后，可以看到 .NET 可移植性报告。 只有不受目标平台支持的类型才显示在列表中，可在“错误列表”的“消息”选项卡中查看建议。 还可以直接从“消息”选项卡跳转到问题区域。

![可移植性报告](./media/portability-analyzer/portability-report.png)

不想使用 Visual Studio？ 还可以从命令提示符使用可移植性分析器。 仅下载 [API 可移植性分析器](http://www.microsoft.com/download/details.aspx?id=42678)。

*   键入以下命令即可分析当前目录：`\...\ApiPort.exe analyze -f .`
*   若要分析特定的 .dll 文件列表，请键入以下命令：`\...\ApiPort.exe analyze -f first.dll -f second.dll -f third.dll`

.NET 可移植性报告以 Excel 文件 (.xlsx) 格式保存在当前目录中。 Excel 工作簿中的“详细信息”选项卡包含详细信息。

有关 .NET 可移植性分析器的详细信息，请访问 [GitHub 文档](https://github.com/Microsoft/dotnet-apiport#documentation)和[简要了解 .NET 可移植性分析器](https://channel9.msdn.com/Blogs/Seth-Juarez/A-Brief-Look-at-the-NET-Portability-Analyzer)第 9 频道视频。

