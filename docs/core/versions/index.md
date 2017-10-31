---
title: ".NET Core 版本控制"
description: "了解 .NET Core 版本控制的工作原理。"
author: bleroy
ms.author: mairaw
ms.date: 08/25/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: f6f684b1-1d2c-4105-8376-7c1959e23803
ms.translationtype: HT
ms.sourcegitcommit: 02cfb7708959057de593506db55e4f31f5ab4fd0
ms.openlocfilehash: 48343ad8d42ad576b1975e81cd764b4ec6f5bc76
ms.contentlocale: zh-cn
ms.lasthandoff: 08/28/2017

---
# <a name="net-core-versioning"></a>.NET Core 版本控制

.NET Core 由作为单元分布的 [NuGet 包](../packages.md)、工具和框架组成。 每个平台层都可单独进行版本控制，以实现更好的敏捷性。 虽然在此方面有巨大的版本控制灵活性，但仍需要将平台作为单元进行版本控制以使产品更易于理解。

本文旨在说明 .NET Core SDK 和运行时版本控制的工作原理。

.NET Core 中有很多版本各异的移动部件。 但从 .NET Core 2.0 开始，采用了所有人都易于理解的顶级版本号，即作为整体的“.NET Core”的唯一版本。 本文的其余部分将详细介绍所有这些部分的版本控制。 这些详细信息对包管理员很重要。

## <a name="versioning-details"></a>版本控制详细信息

从 .NET Core 2.0 开始，下载会在其文件名中显示单一版本号。 以下版本号已统一：

* 共享框架和关联的运行时。
* .NET Core SDK 和关联的 .NET Core CLI。
* `Microsoft.NETCore.App` 元包。

使用单一版本号可让用户更容易知道要在其开发计算机上安装什么版本的 SDK，以及在预配生产环境时应使用共享框架的哪种相应版本。 下载 SDK 或运行时时，你看到的版本号应相同。

### <a name="installers"></a>安装程序

从 .NET Core 2.0 开始，[Daily Builds](https://github.com/dotnet/core-setup#daily-builds)（每日生成）和[发布](https://www.microsoft.com/net/download/core)上提供的下载采用了一种更容易理解的新命名方案。
还修改了这些下载中的安装程序 UI，以便清楚地显示所安装组件的名称和版本。 具体而言，标题现在显示与下载的文件名相同的版本号。

#### <a name="file-name-format"></a>文件名格式

`[product]-[component]-[major].[minor].[patch]-[previewN]-[optional build #]-[rid].[file ext]`

下面是该格式的一些示例：

```
dotnet-runtime-2.0.4-macos.10.12-x64.pkg            # Mac runtime installer
dotnet-sdk-2.0.4-win10-x64.exe                      # Windows SDK installer
dotnet-sdk-2.0.4-fedora.24-x64.tar.gz               # Fedora 24 binary archive

#Ubuntu file set needed for the SDK
dotnet-host-2.0.4-ubuntu.16.04-x64.deb              # Host / muxer and host policy
dotnet-runtime-2.0.4-ubuntu.16.04-x64.deb           # runtime
dotnet-sdk-2.0.4-ubuntu.16.04-x64.deb               # SDK tools
```

这是一种可读格式，能够清晰地显示下载内容、版本，以及适用平台。 运行时包名称包括 `runtime`，SDK 包括`SDK`。

#### <a name="ui-string-format"></a>UI 字符串格式

安装程序中的所有网站说明和 UI 字符串都保持一致、准确、简单。 下表展示了一些示例：

| Installer | 窗口标题                          | 安装程序中的其他内容 | 安装内容                               |
| :--       | :--                                   | :--                        | :--                                             |
| SDK       | .NET Core 2.0 SDK (x64) Installer     | .NET Core 2.0.4 SDK        | .NET Core 2.0.4 Tools + .NET Core 2.0.4 Runtime |
| 运行时   | .NET Core 2.0 Runtime (x64) Installer | .NET Core 2.0.4 Runtime    | .NET Core 2.0.4 Runtime                         |

预览版略有不同：

| Installer | 窗口标题                                    | 安装程序中的其他内容        | 安装内容                                                   |
| :--       | :--                                             | :--                               | :--                                                                 |
| SDK       | .NET Core 2.0 Preview 1 SDK (x64) Installer     | .NET Core 2.0.0 Preview 1 SDK     | .NET Core 2.0.0 Preview 1 Tools + .NET Core 2.0.0 Preview 1 Runtime |
| 运行时   | .NET Core 2.0 Preview 1 Runtime (x64) Installer | .NET Core 2.0.0 Preview 1 Runtime | .NET Core 2.0.0 Preview 1 Runtime                                   |

有时一个 SDK 版本可能会包含多个版本的运行时。 出现这种情况时，安装程序 UX 如下所示（只显示 SDK 版本，而已安装的运行时版本显示在 Windows 和 Mac 上安装过程结束时出现的摘要页上）：

| Installer | 窗口标题                      | 安装程序中的其他内容                                   | 安装内容                                                         |
| :--       | :--                               | :--                                                          | :--                                                                       |
| SDK       | .NET Core 2.1 SDK (x64) Installer | .NET Core 2.1.1 SDK <br> .NET Core 2.1.1 Runtime <br> .NET Core 2.0.6 Runtime | .NET Core 2.1.1 Tools + .NET Core 2.1.1 Runtime + .NET Core 2.0.6 Runtime |

.NET Core Tools 也可能需要更新，但运行时保持不变。 在这种情况下，SDK 版本会升级（例如，升级至 2.1.2），然后运行时在下次传送时升级（例如，运行时和 SDK 在下次传送时升级为 2.1.3）。

### <a name="package-managers"></a>包管理器

.NET Core 可由 Microsoft 以外的其他实体分发。 具体而言，Linux 分发所有者和包维护人员可将 .NET Core 包添加到其包管理器。 有关如何对这些包进行命名和版本控制的建议，请参阅 [ .NET Core 分发打包](../build/distribution-packaging.md)。

#### <a name="minimum-package-set"></a>最小包集

* `dotnet-runtime-[major].[minor]`：包含指定版本的运行时（包管理器中应仅提供针对给定的主要/次要组合的最新修补程序版本）。 新的修补程序版本更新此包，但是新的次要和主要版本是独立的包。
 
  **依赖项**：`dotnet-host`

* `dotnet-sdk`：最新的 SDK。 `update`：前滚主要、次要和修补程序版本。

  **依赖项**：最新的 `dotnet-sdk-[major].[minor]`。

* `dotnet-sdk-[major].[minor]`：包含指定版本的 SDK。 指定的版本是包含的共享框架中最高的包含版本，以便用户可以将 SDK 轻松关联到共享框架。 新的修补程序版本更新此包，但是新的次要和主要版本是独立的包。

  **依赖项**： `dotnet-host`，一个或多个 `dotnet-runtime-[major].[minor]`（其中之一将供 SDK 代码本身使用，在此处用户针对其他运行时进行生成和运行）。

* `dotnet-host`：最新的主机。

##### <a name="preview-versions"></a>预览版

包维护人员可以决定包含运行时和 SDK 的预览版。 请勿将这些预览版包含在未进行版本控制的 `dotnet-sdk` 包中，但是可将其发布为已进行版本控制的包，并将额外的预览标记追加到该名称的主要和次要版本中。 例如，可以有 `dotnet-sdk-2.0-preview1-final` 包。

### <a name="docker"></a>Docker

Docker 标记的一般命名约定为，将版本号放在组件名称之前。 可以继续使用此约定。 当前标记仅包含运行时版本，如下所示。

* 1.0.8-runtime
* 1.0.8-sdk
* 2.0.4-runtime
* 2.0.4-sdk
* 2.1.1-runtime
* 2.1.1-sdk

应更新 SDK 标记以表示 SDK 版本，而不是运行时版本。

还有可能我们需要修复 .NET Core 工具，但重新传送一个现有的运行时。 在这种情况下，SDK 版本会升级（例如，升级至 2.1.2），然后运行时在下次传送时升级（例如，运行时和 SDK 在其后传送时升级为 2.1.3）。

## <a name="semantic-versioning"></a>语义版本控制

.NET Core 使用[语义版本控制 (SemVer)](http://semver.org/)，采用 `MAJOR.MINOR.PATCH` 版本控制，通过版本号的各部分来描述更改程度和类型。

```
MAJOR.MINOR.PATCH[-PRERELEASE-BUILDNUMBER]
```

可选的 `PRERELEASE` 和 `BUILDNUMBER` 部分将永远不会成为受支持版本的一部分，并且将仅存在于夜间版本、来自源目标的本地版本，以及不受支持的预览版本中。

### <a name="how-version-numbers-are-incremented"></a>版本号如何递增？

`MAJOR` 在下列情况时递增：
  - 旧版本不再受支持。
  - 采用了现有依赖项的较新 `MAJOR` 版本。
  - 兼容性的默认设置更改为“关”。

`MINOR` 在下列情况时递增：
  - 添加了公共 API 外围应用。
  - 添加了新行为。
  - 采用了现有依赖项的较新 `MINOR` 版本。
  - 引入了新依赖项。
  
`PATCH` 在下列情况时递增：
  - 进行了 Bug 修复。
  - 添加了对较新平台的支持。
  - 采用了现有依赖项的较新 `PATCH` 版本。
  - 任何其他不符合上述情况的更改。

存在多处更改时，单个更改影响的最高级别元素会递增，并将随后的元素重置为零。 例如，当 `MAJOR` 递增时，`MINOR` 和 `PATCH` 将重置为零。 当 `MINOR` 递增时，`PATCH` 将重置为零，而 `MAJOR` 保持不变。

### <a name="preview-versions"></a>预览版

预览版向版本中追加了 `-preview[number]-([build]|"final")`。 例如 `2.0.0-preview1-final`。

### <a name="servicing-versions"></a>服务版本

在版本发布后，版本分支通常停止生成日常版本，而开始生成服务版本。 服务版本向版本追加了 `-servicing-[number]`。 例如 `2.0.1-servicing-006924`。

### <a name="lts-vs-current"></a>对比 LTS 与 Current

.NET Core 包含两个发行版本系列：Long Term Support (LTS) 和 Current。 这使得用户能够选择所需的稳定性级别和新功能，同时仍然受到支持。

- LTS 意味着用户不会频繁地获得新功能，但是会得到一个更成熟的平台。 LTS 还具有更长的支持期。
- Current 意味着用户可以更频繁地获得新功能和 API，但缺点是用来安装更新的时间更短，并且这些更新会更频繁地出现。 Current 也具有完全支持，但支持期短于 LTS。

Current 版本可以升级为 LTS。

应将“LTS”和“Current”版本视为我们对特定版本添加的标签，便于对关联的支持级别做出声明。

有关详细信息，请参阅 [.NET Core 支持生命周期简报](https://www.microsoft.com/net/core/support)。

## <a name="versioning-scheme-details"></a>版本控制方案详细信息

.NET Core 包括以下部件：

- 主机（也称为 muxer）：`dotnet.exe` 与 `hostfxr` 策略库。
- SDK（开发人员计算机上必需的一套工具，但不用于生产）。
- 运行时。
- 以包的形式分发的共享框架实现。 对每个包进行独立的版本控制，特别是对于修补程序版本控制。
- （可选）将细粒度包作为版本控制单元引用的一组[元包](../packages.md)。 可从包单独对元包进行版本控制。

.NET Core 还包括表示一组随版本号增加而逐渐变大的 API 集的目标框架（如 `netstandard` 或 `netcoreapp`）。

### <a name="net-standard"></a>.NET Standard

.NET Standard 一直在使用 `MAJOR.MINOR` 版本控制方案。 `PATCH` 级别对于 .NET Standard 无效，因为它表示一组不太经常迭代的协定，并且它对版本控制的要求也与实际实现不相同。

.NET Standard 版本和 .NET Core 版本之间没有真正的耦合：.NET Core 2.0 恰好实现 .NET Standard 2.0，但不能保证 .NET Core 的未来版本将映射到相同的 .NET Standard 版本。 .NET Core 可传送未由 .NET Standard 定义的 API，因此，无需新的 .NET Standard 也可以传送新版本。 .NET Standard 也是一个适用于其他目标版本（如 .NET Framework 或 Mono）的概念，即使它的开始恰好与 .NET Core 的开始相一致。

### <a name="packages"></a>包

库包单独发展，并单独进行版本控制。 与 .NET Framework System.\* 程序集重叠的程序包通常使用 4.x 版本，这符合 .NET Framework 4.x 版本控制（历史选择）。 不与 .NET Framework 库重叠的包（如 [`System.Reflection.Metadata`](https://www.nuget.org/packages/System.Reflection.Metadata)）通常从 1.0 开始并由此递增。

由于处于平台的基底，由 [`NETStandard.Library`](https://www.nuget.org/packages/NETStandard.Library) 描述的包将被特殊处理。

`NETStandard.Library` 包通常作为集合进行版本控制，因为这些包之间具有实现级依赖项。

### <a name="metapackages"></a>元包

.NET Core 元包的版本控制基于其所属的 .NET Core 版本。

例如，.NET Core 2.1.3 中的元包都应具有 2.1 作为其 `MAJOR` 和 `MINOR` 版本号。

每次更新任何引用的包时，元包的修补程序版本都会递增。 修补程序版本不会包含更新的框架版本。 因此，从严格意义上讲，元包并不符合 SemVer，因为其版本控制方案不表示基础包中的更改程度，而是主要表示 API 级别。 

.NET Core 当前有两种主要的元包：

**Microsoft.NETCore.App**

- 自 .NET Core 1.0 的 v1.0 开始（这些版本匹配）。
- 映射到 `netcoreapp` 框架。
- 描述 .NET Core 分发中的包。

注意：[`Microsoft.NETCore.Portable.Compatibility`](https://www.nuget.org/packages/Microsoft.NETCore.Portable.Compatibility) 是另一个 .NET Core 元包，它的存在是为了与 .NET 的预 .NET Standard 实现兼容。 该元包不会映射到特殊框架，因此其版本控制与包相同。

**NETStandard.Library**

[`NETStandard.Library`](https://www.nuget.org/packages/NETStandard.Library) - 描述了属于 [.NET Standard](../../standard/library.md) 一部分的各种库。 适用于所有支持 .NET Standard 的 .NET 实现（例如，.NET Framework、.NET Core 和 Mono）。

### <a name="target-frameworks"></a>目标框架

添加新 API 时，目标框架版本也会更新。 它们没有修补程序版本的概念，因为其表示 API 形状，不表示实现问题。 主要和次要版本控制遵循先前指定的 SemVer 规则，并且与实现它们的 .NET Core 分发的 `MAJOR` 和 `MINOR` 数量一致。

## <a name="versioning-in-practice"></a>版本控制实践

下载 .NET Core 时，下载的文件名中将包含版本，例如 `dotnet-sdk-2.0.4-win10-x64.exe`。

每天，在 GitHub 上的 .NET Core 存储库中都有提交和拉取请求，因此会新生成许多库。 为每个更改创建 .NET Core 的新公共版本是不切实际的。 但可在发布新的 .NET Core 公共稳定版前，不定期（例如，几周或几个月一次）聚合更改。

新版本的 .NET Core 可能意味着以下内容：

- 包和元包的新版本。
- 各种框架的新版本，假定添加新 API。
- .NET Core 分发的新版本。

### <a name="shipping-a-patch-release"></a>传送修补程序版本

传送 .NET Core 的主要版本（如 2.0.0 版本）后，对 .NET Core 库进行修补程序级别更改以修复 bug 并改进性能和可靠性。 这意味着没有引入新的 API。 更新各种元包以引用更新的 .NET Core 库包。 将元包作为修补程序更新 (`MAJOR.MINOR.PATCH`) 进行版本控制。 目标框架永远不会作为修补程序版本的一部分更新。 发布新的 .NET Core 分发，其中版本号与 `Microsoft.NETCore.App` 元包匹配。

### <a name="shipping-a-minor-release"></a>传送次要发布

传送具有递增 `MAJOR` 版本号的 .NET Core 版本后，将新的 API 添加到 .NET Core 库以启用新方案。 更新各种元包以引用更新的 .NET Core 库包。 将元包作为具有 `MAJOR` 和 `MINOR` 版本号的修补程序更新进行版本控制，以匹配新的框架版本。 添加了具有新 `MAJOR.MINOR` 版本的新目标框架名称，用以描述新的 API（例如 `netcoreapp2.1`）。 发布新的 .NET Core 分发，其具有与 `Microsoft.NETCore.App` 元包匹配的版本号。

### <a name="shipping-a-major-release"></a>传送主要发布

每次传送新的 .NET Core 的主要版本时，`MAJOR` 版本号将递增，`MINOR` 版本号将重置为零。 新的主要版本至少包含由前一个主要版本后面的次要版本添加的所有 API。 新的主要版本应能够实现重要的新方案，它也可能会失去对旧平台的支持。

更新各种元包以引用更新的 .NET Core 库包。 [`Microsoft.NETCore.App`](https://www.nuget.org/packages/Microsoft.NETCore.App) 元包和 `netcore` 目标框架作为匹配新版本的 `MAJOR` 版本号的主要更新进行版本控制。

## <a name="see-also"></a>请参阅
[目标框架](../../standard/frameworks.md)   
[.NET Core 分发打包](../build/distribution-packaging.md)   
[.NET Core 支持生命周期简报](https://www.microsoft.com/net/core/support)   
[.NET Core 2 和版本绑定](https://github.com/dotnet/designs/issues/3)   

