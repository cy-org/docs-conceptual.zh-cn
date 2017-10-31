---
title: "从 .NET Framework 移植到 .NET Core"
description: "了解移植过程以及发现在将 .NET Framework 项目移植到 .NET Core 时可能有用的工具。"
keywords: .NET, .NET Core
author: cartermp
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 00d00d38-99af-44f4-a75f-defcd9729dc5
ms.translationtype: HT
ms.sourcegitcommit: 3155295489e1188640dae5aa5bf9fdceb7480ed6
ms.openlocfilehash: 4fc68a3dbdec634d8e92a066a46939ba19c65db7
ms.contentlocale: zh-cn
ms.lasthandoff: 08/05/2017

---

# <a name="porting-to-net-core-from-net-framework"></a>从 .NET Framework 移植到 .NET Core

如果已在 .NET Framework 上运行了代码，则可能会对在 .NET Core 1.0 上运行代码感兴趣。  本文提供移植过程的概述以及在移植到 .NET Core 时可能非常有用的工具列表。

## <a name="overview-of-the-porting-process"></a>移植过程概述

建议按照以下步骤进行移植过程。  该步骤的每个部分将在以后的文章中详细介绍。

1. 标识并记录第三方依赖项。

   因此需要了解什么是第三方依赖项，如何依赖于它们，如何查看它们是否也在 .NET Core 上运行，以及如果没有在其上运行可以采取的步骤。
   
2. 将希望移植的所有项目重定向目标到目标 .NET Framework 4.6.2。

   这可确保在 .NET Core 不支持特殊 API 的情况下，可以为特定于 .NET Framework 的目标使用备用 API。
   
3. 使用 [API Portability Analyzer 工具](https://github.com/Microsoft/dotnet-apiport/)来分析程序集并基于结果制定移植计划。

   API Portability Analyzer 工具将分析已编译的程序集并生成报表，该报表将显示高级可移植性摘要和不可用于 .NET Core 上的正在使用的每个 API 的细目。  可以使用此报表和代码库的分析结果一起制定移植代码的计划。
   
4. 移植测试代码。

   由于移植到 .NET Core 对代码库来说是很大的更改，因此强烈建议移植测试代码，以便在移植代码时可以进行测试。  如今，MSTest、xUnit 和 NUnit 都支持 .NET Core 1.0。
   
6. 执行移植计划！

## <a name="tools-to-help"></a>帮助工具

以下是非常有用的工具的简短列表：

* NuGet - [Nuget 客户端](https://dist.nuget.org/index.html)或 [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)，是 Microsoft 针对 .NET 实现的包管理器。
* Api Portability Analyzer - [命令行工具](https://github.com/Microsoft/dotnet-apiport/releases)或 [Visual Studio 扩展](https://visualstudiogallery.msdn.microsoft.com/1177943e-cfb7-4822-a8a6-e56c7905292b)，可生成有关 .NET Framework 和 .NET Core 之间代码移植性的报表的工具链，并且带有程序集到程序集的问题细目。  有关详细信息，请参阅 [Tooling to help you on the process](https://github.com/Microsoft/dotnet-apiport/blob/master/docs/HowTo/)（过程中使用的帮助工具）。
* Reverse Package Search - 一个[有用的 Web 服务](https://packagesearch.azurewebsites.net)，能够实现搜索某一类型并找到包含该类型的包。

## <a name="next-steps"></a>后续步骤

[分析第三方依赖项。](third-party-deps.md)
   

