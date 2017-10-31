---
title: "移植到 .NET Core - 库"
description: "了解如何将 .NET Framework 中的库项目移植到 .NET Core。"
keywords: .NET, .NET Core
author: cartermp
ms.author: mairaw
ms.date: 07/14/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: a0fd860d-d6b6-4659-b325-8a6e6f5fa4a1
ms.translationtype: HT
ms.sourcegitcommit: 2762cdc983465979a530192716c33de7044dd1ed
ms.openlocfilehash: 7b51317b570fcabfe1847685a97c6deab32dcc5c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/04/2017

---

# <a name="porting-to-net-core---libraries"></a>移植到 .NET Core - 库

本文介绍了将库代码移植到 .NET Core 以使其跨平台运行的信息。

## <a name="prerequisites"></a>先决条件

本文假定你：

- 正在使用 Visual Studio 2017 或更高版本。 Visual Studio 的早期版本不支持 .NET Core。
- 了解[推荐的移植过程](index.md)。
- 已解决与[第三方依赖项](third-party-deps.md)有关的任何问题。

还应熟悉下列主题的内容：

[.NET Standard](~/docs/standard/net-standard.md)   
此主题介绍了适用于所有 .NET 实现代码的 .NET API 正式规范。

[包、元包和框架](~/docs/core/packages.md)   
这篇文章介绍了 .NET Core 如何定义和使用包，以及包如何支持多个 .NET 实现代码。

[使用跨平台工具开发库](~/docs/core/tutorials/libraries.md)   
此主题介绍了如何使用跨平台 CLI 工具编写 .NET 的库。

[.NET Core 的 csproj 格式的新增内容](~/docs/core/tools/csproj.md)   
本文概述了作为从移动到 csproj 和 MSBuild 的一部分，添加到项目文件的更改。

[移植到 .NET Core - 分析第三方依赖项](~/docs/core/porting/third-party-deps.md)   
本主题介绍了第三方依赖项的可移植性及 NuGet 包依赖项无法在 .NET Core 上运行时要执行的操作。

## <a name="net-framework-technologies-unavailable-on-net-core"></a>.NET Framework 技术在 .NET Core 上不可用

一些适用于 .NET Framework 库的技术不可用于 .NET Core，例如 AppDomains、远程处理、代码访问安全性 (CAS) 和安全透明度。 如果库依赖于这些技术中的一个或多个，请考虑使用下面所述的替代方法。 有关 API 兼容性的详细信息，CoreFX 团队在 GitHub 上列出了[行为更改/兼容性破坏和弃用的/旧 API 列表](https://github.com/dotnet/corefx/wiki/ApiCompat)。

当前未实现某个 API 或技术并不因此意味着有意不对其提供支持。 在 GitHub 的 [dotnet/corefx 存储库问题](https://github.com/dotnet/corefx/issues)中提交问题，以请求特定 API 和技术。 [问题中的移植请求](https://github.com/dotnet/corefx/labels/port-to-core)已标有 `port-to-core` 标签。

### <a name="appdomains"></a>AppDomain

AppDomain 可将应用相互隔离。 AppDomain 需要运行时支持并且通常价格昂贵。 .NET Core 中未实现它们。 我们不计划在将来添加此功能。 对于代码隔离，建议将流程分隔开来或将容器用作一种替代方法。 对于动态加载的程序集，我们建议使用新的 <xref:System.Runtime.Loader.AssemblyLoadContext> 类。

我们已在 .NET Core 中公开了一些 <xref:System.AppDomain> API 图面，以便可以更轻松地从 .NET Framework 进行代码迁移。 一些 API 可正常工作（例如 <xref:System.AppDomain.UnhandledException?displayProperty=fullName>），一些成员不会执行任何操作（例如 <xref:System.AppDomain.SetCachePath%2A>），也有一些会引发 <xref:System.PlatformNotSupportedException>（例如 <xref:System.AppDomain.CreateDomain%2A>）。 对照 [dotnet/corefx GitHub 存储库](https://github.com/dotnet/corefx)中的 [`System.AppDomain` 引用源](https://github.com/dotnet/corefx/blob/master/src/System.Runtime.Extensions/src/System/AppDomain.cs)检查所使用的类型，确保选择与已实现的版本相匹配的分支。

### <a name="remoting"></a>远程处理

.NET 远程处理被认为是存在问题的体系结构。 它用于进行跨 AppDomain 的通信，该通信现已不再受支持。 同样，远程处理也需要运行时支持，进行维护的成本较高。 出于这些原因，.NET Core 不支持 .NET 远程处理，并且我们不计划在将来添加对它的支持。

对于跨进程通信，可将进程间通信 (IPC) 机制视为远程处理的备用方案，如 <xref:System.IO.Pipes> 或 <xref:System.IO.MemoryMappedFiles.MemoryMappedFile> 类。

对于跨计算机的通信，可将基于网络的解决方案用作备用方案。 最好使用低开销纯文本协议，例如 HTTP。 此处，ASP.NET Core 使用的 Web 服务器 [Kestrel Web 服务器](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel)是一个选择。 也可考虑将 <xref:System.Net.Sockets> 用于基于网络的跨计算机的方案。 请参阅 [.NET 开放源代码开发人员项目：消息传送](https://github.com/Microsoft/dotnet/blob/master/dotnet-developer-projects.md#messaging)了解更多选项。

### <a name="code-access-security-cas"></a>代码访问安全性 (CAS)

沙盒依赖运行时或框架限制托管应用程序或库使用或运行的资源，其[在 .NET Framework 上不受支持](~/docs/framework/misc/code-access-security.md)，因此在 .NET Core 上也不受支持。 我们认为 .NET Framework 中有许多发生特权提升以继续将 CAS 视为安全边界的情况和运行时。 此外，CAS 使实现更加复杂，通常会对无意使用它的应用程序造成正确性-性能影响。

可使用操作系统提供的安全边界，例如虚拟化、容器或用于运行进程的用户帐户具有最少的一组特权。

### <a name="security-transparency"></a>安全透明度

与 CAS 相似，借助安全透明度可以以声明性方式将沙盒代码与安全关键代码隔离，但是[不再支持将它作为安全边界](~/docs/framework/misc/security-transparent-code.md)。 Silverlight 大规模使用了此功能。 

可使用操作系统提供的安全边界，例如虚拟化、容器或用于运行进程的用户帐户具有最少的一组特权。

### <a name="globaljson"></a>global.json

global.json 文件是可选文件，可以通过它设置项目的 .NET Core 工具版本。 如果正在使用 .NET Core 进行每日构建，并且想要指定 SDK 的特定版本，则可使用 global.json 文件指定该版本。 其通常位于当前的工作目录或其父目录之一。 

```json
{
  "sdk": {
    "version": "2.1.0-preview1-006491"
  }
}
```

## <a name="converting-a-pcl-project"></a>转换 PCL 项目

可以通过在 Visual Studio 2017 中加载库并执行以下操作来将 PCL 项目的目标转换为面向 .NET Standard：

1. 右键单击该项目文件，然后选择“属性”。
1. 在“库”下选择“目标 .NET 平台标准”。

如果包支持 NuGet 3.0，则此项目将重定向到 .NET Standard。

如果包不支持 NuGet 3.0，则将从 Visual Studio 收到一个对话框，告诉用户要卸载当前的包。 如果收到此通知，则执行以下步骤：

1. 右键单击项目，选择“管理 NuGet 包”。
1. 记录项目的包。
1. 将包逐一卸载。
1. 可能需要重启 Visual Studio 才能完成卸载过程。 如果需要重启，“NuGet 包管理器”窗口中将显示“重启”按钮。
1. 重载后，项目将面向 .NET Standard。 添加需要卸载的包。

## <a name="retargeting-your-net-framework-code-to-net-framework-462"></a>将 .NET Framework 代码重定向到 .NET Framework 4.6.2

如果代码不面向 .NET Framework 4.6.2，建议重定向到 .NET Framework 4.6.2。 在 .NET Standard 不支持现有 API 情况下，这可确保最新备用 API 的可用性。

对于 Visual Studio 中每个想要移植的项目，请执行以下操作：

1. 右键单击该项目，然后选择“属性”。
1. 在“目标框架”下拉列表中，选择“.NET Framework 4.6.2”。
1. 重新编译项目。

因为项目现在面向 .NET Framework 4.6.2，因此可使用该版本的 .NET Framework 作为移植代码的基准。

## <a name="determining-the-portability-of-your-code"></a>确定代码的可移植性

下一步是运行 API 可移植性分析器 (ApiPort) 生成可供分析的可移植性报表。

确保了解 [API 可移植性分析器 (ApiPort)](~/docs/standard/portability-analyzer.md) 及如何生成用于面向 .NET Core 的可移植性报表。 执行此操作的方式可能取决于需求和个人偏好。 下面介绍了一些不同方法。 用户可能会发现自己根据生成代码的方式混合使用了这些方法中的步骤。

### <a name="dealing-primarily-with-the-compiler"></a>主要处理编译器

此方法可能最适合小项目或不会用很多 .NET Framework API 的项目。 此方法很简单：

1. 可选择在项目上运行 ApiPort。 若运行 ApiPort，则从报告获取有关需要解决的问题的信息。
1. 将所有代码复制到新的 .NET Core 项目。
1. 查看可移植性报表（如果已生成）时，解决编译器错误，直至项目完全得到编译。

尽管这种方法非常松散，但以代码为中心的方法通常可快速解决问题，并且可能是最适合小型项目或库的方法。 只包含数据模型的项目可能是此方法的理想选择。

### <a name="staying-on-the-net-framework-until-portability-issues-are-resolved"></a>可移植性问题得到解决前停留在 .NET Framework 上

如果更希望拥有在整个过程期间编译的代码，此方法可能是最佳选择。 该方法如下所示：

1. 在项目上运行 ApiPort。
1. 通过使用可移植的不同 API 解决问题。
1. 记录阻止你使用直接替代方案的所有区域。
1. 对所有要移植的项目重复前面的步骤，直到确信每个项目都做好被复制到新的 .NET Core 项目中的准备。
1. 将代码复制到新的 .NET Core 项目。
1. 解决所有已记录的不存在直接替代方案的问题。

这种谨慎的方法比单纯解决编译器错误更有条理，但相对而言，它仍以代码为中心，且优点是始终拥有编译的代码。 解决不能通过只使用另一个 API 解决的某些问题的方法大不相同。 你可能会发现对于某些项目，需要制定更全面的计划，这将在下一种方法中涉及到。

### <a name="developing-a-comprehensive-plan-of-attack"></a>制定全面的施行计划

此方法可能最适合大型或更复杂的项目，在这种情况下，为支持 .NET Core，可能必需重构代码或将某些代码区域完全重写。 该方法如下所示：

1. 在项目上运行 ApiPort。
1. 了解每个非可移植类型使用的位置以及位置对整体可移植性的影响。
   - 了解这些类型的特性。 它们是否数量少，但使用频繁？ 它们是否数量大，但使用不频繁？ 它们是串联使用，还是在整个代码中传播？
   - 是否可以轻松隔离不可移植的代码，以便可以更有效地处理它？
   - 是否需要重构代码？
   - 对于这些不可移植的类型，是否存在可完成相同任务的备用 API？ 例如，如果使用 <xref:System.Net.WebClient> 类，也许能够改用 <xref:System.Net.Http.HttpClient> 类。
   - 是否存在其他可用于完成任务的可移植 API，即使它不是直接替代 API？ 例如，如果使用 <xref:System.Xml.Schema.XmlSchema> 来分析 XML，但是无需 XML 架构发现，则可使用 <xref:System.Xml.Linq> API 并自行实现分析，而不依赖于 API。
1. 如果具有难以移植的程序集，是否值得将其暂时留在 .NET Framework 上？ 以下是一些需要考虑的事项：
   - 库中可能具有某些与 .NET Core 不兼容的功能，因为它太依赖 .NET Framework 或 Windows 特定的功能。 是否值得暂时搁置该功能并发布在资源可用于移植这些功能前暂具较少功能的库的 .NET Core 版本？
   - 重构是否有用？
1. 编写自己对不可用 .NET Framework API 的实现是否合理？
   可以考虑复制、修改，并使用 [.NET Framework 参考源](https://github.com/Microsoft/referencesource)中的代码。 参考源代码已在 [MIT 许可证](https://github.com/Microsoft/referencesource/blob/master/LICENSE.txt)下获得许可，因此可以自由选择将此源作为自己代码的基础。 只需确保在代码中正确设置 Microsoft。
1. 根据不同项目的需要，重复此过程。
 
分析阶段可能需要一些时间，具体取决于代码库的大小。 在此阶段花费时间（尤其是在具有复杂的代码库时），全面了解所需的更改范围并制定计划，从长远看通常可节省时间。

计划可能包括对代码库做重大更改，同时面向 .NET Framework 4.6.2，使它成为前一种方法更有条理的版本。 着手执行计划的方式具体取决于代码库。

### <a name="mixing-approaches"></a>混合方法

在每个项目的基础上，可能会将上述方法进行混合。 应该进行对你和代码库最有意义的操作。

## <a name="porting-your-tests"></a>移植测试

要确保移植代码后一切正常的最佳方式是在将代码移植到 .NET Core 时进行测试。 为此，需要使用将针对 .NET Core 生成和运行测试的测试框架。 当前，有三个选择：

- [xUnit](https://xunit.github.io/)
  * [入门](http://xunit.github.io/docs/getting-started-dotnet-core.html)
  * [将 MSTest 项目转换为 xUnit 的工具](https://github.com/dotnet/codeformatter/tree/master/src/XUnitConverter)
- [NUnit](http://www.nunit.org/)
  * [入门](https://github.com/nunit/docs/wiki/Installation)
  * [关于从 MSTest 迁移到 NUnit 的博客文章](http://www.florian-rappl.de/News/Page/275/convert-mstest-to-nunit)
- [MSTest](https://docs.microsoft.com/visualstudio/test/unit-test-basics)

## <a name="recommended-approach-to-porting"></a>移植的推荐方法

从根本上讲，移植工作在很大程度上取决于生成 .NET Framework 代码的方式。 移植代码的一个好方法是从库的基项开始，这是代码的基础组件。 这可能是数据模型或某些其他内容直接或间接使用的基本类和方法。

1. 移植测试项目，该项目测试当前正在移植的库层。
1. 将库中的基项复制到新的 .NET Core 项目，然后选择想要支持的 .NET Standard 版本。
1. 进行任何所需的更改，使代码进行编译。 大部分内容可能会要求将 NuGet 包依赖项添加到 csproj 文件。
1. 运行测试并进行任何所需调整。
1. 选择下一层代码进行移植，并重复前面的步骤。

如果从库的基项开始并从基项向外移动并根据需要测试每一层，移植将是一个系统化的过程，在这种情况下，问题可以一次隔离到一层代码中。

