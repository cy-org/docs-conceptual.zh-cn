---
title: ".NET Core 应用程序部署"
description: "部署 .NET Core 应用程序。"
keywords: ".NET、.NET Core、.NET Core 部署"
author: rpetrusha
ms.author: ronpet
ms.date: 04/18/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: da7a31a0-8072-4f23-82aa-8a19184cb701
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 199bb132df201175dbdbdd19634de5c3551b5f3b
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="net-core-application-deployment"></a>.NET Core 应用程序部署

可以为 .NET Core 应用程序创建两种部署：

- 依赖框架的部署。 顾名思义，依赖框架的部署 (FDD) 依赖目标系统上存在共享系统级版本的 .NET Core。 由于已存在 .NET Core，因此应用在 .NET Core 安装程序间也是可移植的。 应用仅包含其自己的代码和任何位于 .NET Core 库外的第三方依赖项。 FDD 包含可通过在命令行中使用 [dotnet 实用程序](../tools/dotnet.md)启动的 *.dll* 文件。 例如，`dotnet app.dll` 就可以运行一个名为 `app` 的应用程序。

- 独立部署。 与 FDD 不同，独立部署 (SCD) 不依赖目标系统上存在的共享组件。 所有组件（包括 .NET Core 库和 .NET Core 运行时）都包含在应用程序中，并且独立于其他 .NET Core 应用程序。 SCD 包括一个可执行文件（如 Windows 平台上名为 `app` 的应用程序的 *app.exe*），它是特定于平台的 .NET Core 主机的重命名版本，还包括一个 .*.dll* 文件（如 *app.dll*），而它是实际的应用程序。

## <a name="framework-dependent-deployments-fdd"></a>依赖框架的部署 (FDD)

对于 FDD，仅部署应用和任何第三方依赖项。 不需要部署 .NET Core，因为应用将使用目标系统上存在的 .NET Core 版本。 这是 .NET Core 应用的默认部署模型。

### <a name="why-create-a-framework-dependent-deployment"></a>为什么创建依赖框架的部署？

部署 FDD 具有很多优点：

- 不需要提前定义 .NET Core 应用将在其上运行的目标操作系统。 因为无论什么操作系统，.NET Core 的可执行文件和库都是用通用的 PE 文件格式，因此，无论什么基础操作系统，.NET Core 都可执行应用。 有关 PE 文件格式的详细信息，请参阅 [.NET 程序集文件格式](../../standard/assembly-format.md)。

- 部署包很小。 只需部署应用及其依赖项，而无需部署 .NET Core 本身。

- 许多应用都可使用相同的 .NET Core 安装，从而降低了主机系统上磁盘空间和内存使用量。

也有几个缺点：

- 仅当主机系统上已安装你设为目标的 .NET Core 版本或更高版本时，应用才能运行。

- 如果不了解将来版本，.NET Core 运行时和库可能发生更改。 在极少数情况下，这可能会更改应用的行为。

## <a name="self-contained-deployments-scd"></a>独立部署 (SCD)

对于独立部署，可以部署应用和所需的第三方依赖项以及生成应用所使用的 .NET Core 版本。 创建 SCD 不包括各种平台上的 [.NET Core 本机依赖项](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md)，因此运行应用前这些依赖项必须已存在。

FDD 和 SCD 部署使用单独的主机可执行文件，使你可以使用发布者签名为 SCD 签署主机可执行文件。

### <a name="why-deploy-a-self-contained-deployment"></a>为什么要部署独立部署？

部署独立部署主要有两个优点：

- 可以对与应用一起部署的 .NET Core 版本具有单独的控制权。 只有你才能维护 .NET Core。

- 请放心，目标系统可以运行你的 .NET Core 应用，因为你提供的是应用将在其上运行的 .NET Core 版本。

它也有几个缺点：

- 由于 .NET Core 包含在部署包中，因此必须提前选择为其生成部署包的目标平台。

- 部署包相对较大，因为需要将 .NET Core 和应用及其第三方依赖项包括在内。

- 向系统部署大量独立的 .NET Core 应用可能会使用大量磁盘空间，因为每个应用都会复制 .NET Core 文件。

## <a name="step-by-step-examples"></a>分步示例

有关使用 CLI 工具部署 .NET Core 应用的分步示例，请参阅[使用 CLI 工具部署 .NET Core 应用](deploy-with-cli.md)。 有关使用 Visual Studio 部署 .NET Core 应用的分步示例，请参阅 [使用 Visual Studio 部署 .NET Core 应用](deploy-with-vs.md)。 每个主题都包括以下部署的示例：

- 依赖框架的部署
- 包含第三方依赖项的依赖框架的部署
- 独立部署
- 包含第三方依赖项的独立部署

# <a name="see-also"></a>请参阅

[使用 CLI 工具部署 .NET Core 应用](deploy-with-cli.md)   
[使用 Visual Studio 部署 .NET Core 应用](deploy-with-vs.md)   
[包、元包和框架](../packages.md)   
[.NET Core 运行时标识符 (RID) 目录](../rid-catalog.md)

