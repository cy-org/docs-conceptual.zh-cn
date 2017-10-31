---
title: "为服务器应用选择 .NET Core 或 .NET Framework"
description: "关于在 .NET 中生成服务器应用时应考虑使用哪种 .NET 实现的指南。"
author: cartermp
ms.author: mairaw
ms.date: 08/15/2016
ms.topic: article
ms.prod: .net
ms.translationtype: HT
ms.sourcegitcommit: fe2c7ff4055779a000b68a68333f3e4d06381410
ms.openlocfilehash: aa06ff8253f22c5c867d4ba12c0a132269e04a97
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="choosing-between-net-core-and-net-framework-for-server-apps"></a>为服务器应用选择 .NET Core 或 .NET Framework

有两种支持的实现可用于通过 NET Framework 和 .NET Core 生成服务器端应用程序。 这两者共享许多相同的组件，可在它们之间共享代码。 但两者之间存在根本的差异，可根据需要实现的目标进行选择。  本文介绍了在何种情况下进行选择。

在以下情况，对服务器应用程序使用 .NET Core：

* 用户有跨平台需求。
* 用户正在面向微服务。
* 用户正在使用 Docker 容器。
* 需要高性能和可扩展的系统。
* 需按应用程序提供并行的 .NET 版本。

在以下情况，对服务器应用程序使用 .NET Framework ：

* 应用当前使用 .NET Framework（建议扩展而不是迁移）。
* 应用使用不可用于 .NET Core 的第三方 .NET 库或 NuGet 包。
* 应用使用不可用于 .NET Core 的 .NET 技术。
* 应用使用不支持 .NET Core 的平台。

## <a name="when-to-choose-net-core"></a>选择 .NET Core 的情形

以下各部分对前面提到的选择 .NET Core 的原因进行了进一步说明。

### <a name="cross-platform-needs"></a>跨平台需求

如果应用程序（Web/服务）需要在多个平台（Windows、Linux 和 macOS）上运行，请使用 .NET Core。

.NET Core 作为开发工作站支持前面提到的操作系统。 Visual Studio 提供用于 Windows 和 Mac 的集成开发环境 (IDE)。 还可使用运行于 macOS、Linux 和 Windows 上的 Visual Studio Code。 Visual Studio Code 支持 .NET Core，包括 IntelliSense 和调试。 大多数第三方编辑器（如 Sublime、Emacs 和 VI）都可搭配 .NET Core 使用。 这些第三方编辑器可使用 [Omnisharp](http://www.omnisharp.net/) 获取编辑器 IntelliSense。 也可不使用任何代码编辑器，直接使用适用于所有支持平台的 [.NET Core CLI 工具](../core/tools/index.md)。

### <a name="microservices-architecture"></a>微服务体系结构

微服务体系结构允许跨服务边界组合使用技术。 通过这种技术组合，可逐步接受 .NET Core 作为能与其他微服务或服务搭配使用的新微服务。 例如，可组合使用微服务或使用 .NET Framework、Java、Ruby 或其他单片技术开发的服务。

可用的基础结构平台有很多。 [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/)，设计用于大型和复杂微服务系统 。 [Azure App Service](https://azure.microsoft.com/services/app-service/)，很适合用于无状态微服务。 基于 Docker 的微服务备选方案适合任何一种微服务方法，这部分内容将在[容器](#containers)部分进行说明。 所有这些平台都支持 .NET Core，是托管微服务的理想选择。

有关微服务体系结构的详细信息，请参阅 [.NET 微服务 - 适用于容器化 .NET 应用程序的体系结构](microservices-architecture/index.md)。

### <a name="containers"></a>容器

容器通常与微服务体系结构结合使用。 还可使用容器将遵循任何体系结构模式的 Web 应用或服务容器化。 可在 Windows 容器上使用 .NET Framework，但 .NET Core 的模块化和轻型性质使之成为容器的更佳选择。 在创建和部署容器时，使用 .NET Core 时容器的映像大小要远小于使用 .NET Framework 时的大小。 例如，因为它是跨平台的，所以可将服务器应用部署到 Linux Docker 容器。

Docker 容器可托管在自己的 Linux 或 Windows 基础结构中，或托管在 [Azure 容器服务](https://azure.microsoft.com/services/container-service/)等云服务中。 Azure 容器服务可管理、协调和缩放云中基于容器的应用程序。

### <a name="a-need-for-high-performance-and-scalable-systems"></a>高性能和可扩展系统的需求

如果系统需要最佳的性能和可伸缩性，.NET Core 和 ASP.NET Core 是最佳的选择。 Windows Server 和 Linux 的高性能服务器运行时使 .NET 成为 [TechEmpower 基准](https://www.techempower.com/benchmarks/#hw=ph&test=plaintext)上执行最佳的 Web 框架。

性能和可伸缩性对微服务体系结构尤为重要，体系结构中可能正在运行数百个微服务。 借助 ASP.NET Core，系统运行的服务器/虚拟机 (VM) 数要低得多。 减少服务器/VM 后可节省基础结构和托管成本。

### <a name="a-need-for-side-by-side-of-net-versions-per-application-level"></a>需要按应用程序级别选择并行的 .NET 版本

若要安装含不同 .NET 版本上的依赖项的应用程序，建议使用 NET Core。 通过 .NET Core 可在同一计算机上并行安装不同版本的 .NET Core 运行时。 并行安装允许在同一服务器上使用多个服务，每个服务位于其相应的 .NET Core 版本上。 这还可在应用程序升级和 IT 运营时降低风险、节省成本。

## <a name="when-to-choose-net-framework"></a>选择 .NET Framework 的情形

.NET Core 对新应用程序和应用程序模式特别有用。 但 .NET Framework 仍是许多现有方案非常自然的选择。 对于所有服务器应用程序，.NET Framework 不会被 .NET Core 代替。

### <a name="current-net-framework-applications"></a>现有的 .NET Framework 应用程序

在大多数情况下，不需要将现有应用程序迁移到 .NET Core。 相反，若要扩展现有的应用程序（例如，在 ASP.NET Core 中写入新的 Web 服务），建议使用 .NET Core。

### <a name="a-need-to-use-third-party-net-libraries-or-nuget-packages-not-available-for-net-core"></a>需要使用不可用于 .NET Core 的第三方 .NET 库或 NuGet 包

库很快将使用 .NET Standard。 通过 .NET Standard 可跨各种 .NET 实现（包括 .NET Core）共享代码。 使用 .NET Standard 2.0 则更简单：
- API 曲面已变为更大。 
- 引入了 .NET Framework 兼容性模式。 此兼容性模式允许 .NET Standard/.NET Core 项目引用.NET Framework 库。 若要详细了解兼容性模式，请参阅 [Announcing .NET Standard 2.0](https://blogs.msdn.microsoft.com/dotnet/2017/08/14/announcing-net-standard-2-0/)（宣布发布 .NET Standard 2.0）。

因此，只有在库或 NuGet 包使用的技术在 .NET Standard/.NET Core 中不可用的情况下，才需要使用 .NET Framework。

### <a name="a-need-to-use-net-technologies-not-available-for-net-core"></a>需要使用不可用于 .NET Core 的 .NET 技术

某些 .NET Framework 技术在 .NET Core 中不可用。 其中一些技术可能在更高版本的 .NET Core 中可用。 但其他技术不会应用于 .NET Core 面向的新应用程序模式，因此可能永远不可用。 以下列表显示无法在 .NET Core 中找到的最常见技术：

* ASP.NET Web 窗体应用程序：ASP.NET Web 窗体仅在.NET Framework 中可用。 ASP.NET Core 不能用于 ASP.NET Web 窗体。 目前没有将 ASP.NET Web 窗体引入 .NET Core 的计划。

* ASP.NET 网页应用程序：ASP.NET 网页未包含在 ASP.NET Core 中。 ASP.NET Core [Razor 页](/aspnet/core/mvc/razor-pages/)与网页有许多相似之处。

* ASP.NET SignalR 服务器/客户端实现。 目前，ASP.NET SignalR 不可用于 ASP.NET Core（非客户端或服务器）。 ASP.NET Core SignalR 预计可用于 ASP.NET Core 2.1。 请参阅 [ASP.NET Core Schedule and Roadmap](https://github.com/aspnet/Home/wiki/Roadmap)（ASP.NET Core 计划和路线图）。 [服务器端](https://github.com/aspnet/SignalR-Server)和[客户端库](https://github.com/aspnet/SignalR-Client-Net) GitHub 存储库上的预览状态可用。

* WCF 服务的实现。 虽然 [WCF 客户端库](https://github.com/dotnet/wcf)可从 .NET Core 使用 WCF 服务，WCF 服务器实现目前只在 .NET Framework 上可用。 这种情况虽然不属于 .NET Core 当前计划，但将来会考虑这点。

* 工作流相关的服务：Windows Workflow Foundation (WF)、工作流服务（WCF + 单个服务中的 WF）和 WCF 数据服务（以前称为“ADO.NET 数据服务”）仅在 .NET Framework 上可用。  尚未计划将 WF/WCF+WF/WCF Data Services 引入 .NET Core。

* Windows Presentation Foundation (WPF) 和 Windows 窗体：WPF 和 Windows 窗体应用程序仅在 .NET Framework 上可用。 没有将其移植到 .NET Core 的计划。

* 语言支持：.NET Core 目前支持 Visual Basic 和 F#，但不是所有项目类型都支持。 有关支持的项目模板列表，请参阅 [dotnet new 的模板选项](../core/tools/dotnet-new.md#arguments)。

除了正式的路线图，还有其他框架将植入 .NET Core。 若要查看完整列表，请参阅标记为 [port-to-core](https://github.com/dotnet/corefx/issues?q=is%3Aopen+is%3Aissue+label%3Aport-to-core) 的 CoreFX 问题。 此列表并不代表 Microsoft 承诺将这些组件引入 .NET Core。 这样做只是因为他们捕获到了社区所需。 如果关注任何标记为 `port-to-core` 的组件，请在 GitHub 上参与讨论。 如果认为遗漏了某些内容，请在 [CoreFX 存储库](https://github.com/dotnet/corefx/issues/new)中提出新的问题。

### <a name="a-need-to-use-a-platform-that-doesnt-support-net-core"></a>需要使用不支持 .NET Core 的平台

某些 Microsoft 或第三方平台不支持 .NET Core。 例如，某些 Azure 服务（如 Service Fabric Stateful Reliable Services 和 Service Fabric Reliable Actors）需要 .NET Framework。 某些其他服务提供尚不可用于 .NET Core 的 SDK。 这只是过渡情况，因为所有 Azure 服务都将使用 .NET Core。 在此期间，可用始终使用等效的 REST API 取代客户端 SDK。

## <a name="see-also"></a>请参阅
 [在 ASP.NET 和 ASP.NET Core 之间进行选择](/aspnet/core/choose-aspnet-framework)   
 [.NET Core 指南](../core/index.md)   
 [从 .NET Framework 移植到 .NET Core](../core/porting/index.md)   
 [Docker 上的 .NET Framework 指南](../framework/docker/index.md)   
 [.NET 组件概述](components.md)   
 [.NET 微服务 - 适用于容器化 .NET 应用程序的体系结构](microservices-architecture/index.md)

