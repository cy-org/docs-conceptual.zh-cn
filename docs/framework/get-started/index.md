---
title: ".NET Framework 入门"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- .NET Framework, getting started
- getting started [.NET Framework]
ms.assetid: c693fd34-88fe-4d90-b332-19eeadf3b7e7
caps.latest.revision: 35
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 21c6a1485f3d0c38bde065d6ecc7b07d5e424c1d
ms.openlocfilehash: 327aad36a560a772e9ddb4d8d721c2545f800151
ms.contentlocale: zh-cn
ms.lasthandoff: 08/05/2017

---

# <a name="get-started-with-the-net-framework"></a>.NET Framework 入门

.NET Framework 是管理面向 .NET Framework 的应用的运行时执行环境。 它包括公共语言运行时（提供内存管理和其他系统服务）和一个全面的类库（使程序员能利用强大可靠的代码实现所有主要领域的应用开发）。

<a name="Introducing"></a>
## <a name="what-is-the-net-framework"></a>什么是 .NET Framework？

.NET Framework 是为其运行的应用提供各种服务的托管执行环境。 它包括两个主要组件：公共语言运行时 (CLR)，它是处理运行应用的执行引擎；.NET Framework 类库，它提供开发人员可从其自己的应用中调用的已测试、可重用代码库。 .NET Framework 提供的用于运行应用的服务包括：

- 内存管理。 在许多编程语言中，程序员负责分配和释放内存并处理对象生存期。 在 .NET Framework 应用中，CLR 代表应用提供这些服务。

- 常规类型系统。 在传统编程语言中，基本类型由编译器定义，这将使跨语言互操作性复杂化。 在 .NET Framework 中，基本类型由 .NET Framework 类型系统定义，并且是面向 .NET Framework 的所有语言所共有的。

- 一个全面的类库。 处理常见的低级编程操作时，程序员可通过 .NET Framework 类库使用类型及其成员的易访问库，而不必编写大量代码。

- 开发框架和技术。 .NET Framework 包括用于特定区域应用开发的库，如用于 Web 应用的 ASP.NET，用于数据访问的 ADO.NET 以及用于面向服务的应用的 Windows Communication Foundation。

- 语言互操作性。 面向 .NET Framework 的语言编译器发出名为公共中间语言 (CIL) 的中间代码，反过来，通过公共语言运行时在运行时进行编译。 借助此功能，使用某种语言编写的例程可由另一种语言访问，程序员可以专注于使用其首选语言创建应用。

- 版本兼容性。 除少数例外，使用特定版本的 .NET Framework 开发的应用无需在更高版本中修改即可运行。

- 并行执行。 通过允许同一台计算机上存在公共语言运行时的多个版本，.NET Framework 可帮助解决版本冲突。 这意味着应用的多个版本可以共存，并且应用可在构建它的 .NET Framework 版本上运行。 并行执行适用于 .NET Framework 版本组 1.0/1.1、2.0/3.0/3.5 和 4/4.5.x/4.6.x/4.7。

- 多定向。 通过定向 [.NET Standard](~/docs/standard/net-standard.md)，开发人员可创建在多个 .NET Framework 平台（例如，Windows 7、Windows 8、Windows 8.1、Windows 10、Windows Phone 和 Xbox 360）上工作的程序集。

<a name="ForUsers"></a>
## <a name="the-net-framework-for-users"></a>面向用户的 .NET Framework

如果你不开发 .NET Framework 应用，而只需要使用它们，则不需要掌握有关 .NET Framework 或其操作的特定知识。 大多数情况下，.NET Framework 对用户是完全透明的。

如果你使用的是 Windows 操作系统，则你的计算机上可能已安装 .NET Framework。 此外，如果安装需要 .NET Framework 的应用，则应用的安装程序可能会在你的计算机上安装特定版本的 .NET Framework。 在某些情况下，可能会显示一个要求你安装 .NET Framework 的对话框。 如果在该对话框出现时刚尝试过运行应用，并且计算机可以访问 Internet，则可以转到一个可安装缺少的 .NET Framework 版本的网页。

一般而言，不应卸载计算机上已安装的 .NET Framework 版本。 主要有两个原因：

- 如果使用的应用依赖于特定版本的 .NET Framework，则该版本一旦删除，应用就会暂停。

- 一些 .NET Framework 版本是早期版本的就地更新版。 例如，[!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] 是版本 2.0 的就地更新版，而 .NET Framework 4.7 是版本 4、4.5、4.5.1、4.5.2、4.6、4.6.1 和 4.6.2 的就地更新版。 有关详细信息，请参见 [.NET Framework 版本和依赖关系](../../../docs/framework/migration-guide/versions-and-dependencies.md)。

如果选择删除 .NET Framework，请始终通过“控制面板”的“程序及功能”进行卸载。 请勿手动删除某个版本的 .NET Framework。

请注意，一台计算机上可同时存在多个 .NET Framework 版本。 这意味着，你不必卸载旧版本即可安装更新版本。

<a name="ForDevelopers"></a> 
## <a name="the-net-framework-for-developers"></a>面向开发人员的 .NET Framework

如果你是开发人员，可选择任何支持 .NET Framework 的编程语言来创建应用。 由于 .NET Framework 提供了语言独立性和互操作性，因此无论开发时使用何种语言，你都可以与其他 .NET Framework 应用和组件进行交互。

若要开发 .NET Framework 应用或组件，请执行以下操作：

1. 如果未在操作系统上预安装 .NET Framework，请安装应用所面向的 .NET Framework 版本。 最新的生产版本是 .NET Framework 4.7，此版本预安装在 Windows 10 创意者更新上，并可下载到旧版 Windows 操作系统。 有关 .NET Framework 系统要求，请参阅[系统要求](../../../docs/framework/get-started/system-requirements.md)。 有关安装其他版本的 .NET Framework 的信息，请参阅[安装指南](../../../docs/framework/install/guide-for-developers.md)。 其他 .NET Framework 包为带外发布，这意味着这些包在滚动基础上发布，没有任何定期或计划的发布周期。 有关这些包的信息，请参阅 [.NET Framework 和带外版本](../../../docs/framework/get-started/the-net-framework-and-out-of-band-releases.md)。

2. 选择要用于开发应用的 .NET Framework 所支持的语言。 大量语言可供选择，包括来自 Microsoft 的 Visual Basic、C#、Visual F# 和 C++/CLI。 （一种用于开发 .NET Framework 应用的编程语言，它遵循[公共语言基础结构 (CLI) 规范](http://go.microsoft.com/fwlink/?LinkId=199862)。）

3. 选择并安装将用于创建应用并支持所选程序语言的开发环境。 适用于 .NET Framework 应用的 Microsoft 集成开发环境 (IDE) 是 [Visual Studio](http://go.microsoft.com/fwlink/?LinkId=325532)。 它提供多种版本。

若要深入了解如何开发面向.NET Framework 的应用，请参阅[开发指南](../../../docs/framework/development-guide.md)。

## <a name="related-topics"></a>相关主题

| 标题 | 说明 |
| ----- |------------ |
| [概述](../../../docs/framework/get-started/overview.md) | 为构建面向 .NET Framework 的应用的开发人员提供详细信息。 |
| [安装指南](../../../docs/framework/install/index.md) | 提供有关安装 .NET Framework 的信息。 |  
| [.NET Framework 和带外版本](../../../docs/framework/get-started/the-net-framework-and-out-of-band-releases.md) | 介绍 .NET Framework 带外版本以及如何在应用中使用它们。 |
| [系统要求](../../../docs/framework/get-started/system-requirements.md) | 列出运行 .NET Framework 的硬件和软件要求。 |
| [.NET 核心和开放源代码](../../../docs/framework/get-started/net-core-and-open-source.md) | 介绍 .NET Core 与 .NET Framework 的关系，以及如何访问开放源代码 .NET Core 项目。 |
| [.NET 核心文档](https://docs.microsoft.com/dotnet/) | 提供 .NET Core 的概念和 API 参考文档。 |

## <a name="see-also"></a>请参阅

[.NET Framework 指南](../../../docs/framework/index.md)   
[新增功能](../../../docs/framework/whats-new/index.md)   
[.NET API 浏览器](/dotnet/api/)   
[开发指南](../../../docs/framework/development-guide.md)

