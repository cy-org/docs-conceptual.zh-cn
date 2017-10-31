---
title: ".NET Core 命令行接口 (CLI) 工具"
description: "概述了 .NET Core 命令行接口 (CLI) 工具和功能。"
author: mairaw
ms.author: mairaw
ms.date: 08/14/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.translationtype: HT
ms.sourcegitcommit: a19ab54a6cc44bd7acd1e40a4ca94da52bf14297
ms.openlocfilehash: f56b571e61f82132718ecf5890024c0f1c177227
ms.contentlocale: zh-cn
ms.lasthandoff: 08/14/2017

---
# <a name="net-core-command-line-interface-cli-tools"></a>.NET Core 命令行接口 (CLI) 工具

.NET Core 命令行接口 (CLI) 工具是用于开发 .NET 应用程序的新型跨平台工具链。 CLI 是更高级别的工具（如集成开发环境 (IDE)、编辑器和生成协调程序）可以驻留的基础。

## <a name="installation"></a>安装

使用本机安装程序或使用安装 shell 脚本：

* 本机安装程序主要用于开发人员的计算机，并使用每个受支持的平台的本机安装机制，例如，Ubuntu 上的 DEB 程序包或 Windows 上的 MSI 捆绑包。 这些安装程序安装并配置环境，供开发人员立即使用，但是需要具有该计算机上的管理权限。 可以在 [.NET Core 安装指南](https://aka.ms/dotnetcoregs)中查看安装说明。
* Shell 脚本主要用于设置生成服务器或希望安装工具但没有管理权限的情况。 安装脚本不会在计算机上安装先决条件，必须手动安装它。 有关详细信息，请参阅[安装脚本引用主题](dotnet-install-script.md)。 有关如何在你的持续集成 (CI) 生成服务器上设置 CLI 的信息，请参阅[在持续集成 (CI) 中使用 .NET Core SDK 和工具](using-ci-with-cli.md)。

在默认情况下，SLI 以并行 (SxS) 方式安装，因此，因此，CLI 工具的多个版本可以在一个计算机上共存。 有关确定在安装了多个版本的计算机上所使用的版本的类型，在[驱动程序](#driver)部分中对此有更详尽的介绍。

## <a name="cli-commands"></a>CLI 命令

默认安装以下命令：

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

**基本命令**

* [new](dotnet-new.md)
* [restore](dotnet-restore.md)
* [build](dotnet-build.md)
* [publish](dotnet-publish.md)
* [run](dotnet-run.md)
* [test](dotnet-test.md)
* [vstest](dotnet-vstest.md)
* [pack](dotnet-pack.md)
* [migrate](dotnet-migrate.md)
* [clean](dotnet-clean.md)
* [sln](dotnet-sln.md)
* [help](dotnet-help.md)
* [store](dotnet-store.md)

**项目修改命令**

* [add package](dotnet-add-package.md)
* [add reference](dotnet-add-reference.md)
* [remove package](dotnet-remove-package.md)
* [remove reference](dotnet-remove-reference.md)
* [list reference](dotnet-list-reference.md)

**高级命令**

* [nuget delete](dotnet-nuget-delete.md)
* [nuget locals](dotnet-nuget-locals.md)
* [nuget push](dotnet-nuget-push.md)
* [msbuild](dotnet-msbuild.md)
* [dotnet install script](dotnet-install-script.md)

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

**基本命令**

* [new](dotnet-new.md)
* [restore](dotnet-restore.md)
* [build](dotnet-build.md)
* [publish](dotnet-publish.md)
* [run](dotnet-run.md)
* [test](dotnet-test.md)
* [vstest](dotnet-vstest.md)
* [pack](dotnet-pack.md)
* [migrate](dotnet-migrate.md)
* [clean](dotnet-clean.md)
* [sln](dotnet-sln.md)

**项目修改命令**

* [add package](dotnet-add-package.md)
* [add reference](dotnet-add-reference.md)
* [remove package](dotnet-remove-package.md)
* [remove reference](dotnet-remove-reference.md)
* [list reference](dotnet-list-reference.md)

**高级命令**

* [nuget delete](dotnet-nuget-delete.md)
* [nuget locals](dotnet-nuget-locals.md)
* [nuget push](dotnet-nuget-push.md)
* [msbuild](dotnet-msbuild.md)
* [dotnet install script](dotnet-install-script.md)

---

CLI 采用可使你为项目指定其他工具的扩展性模型。 有关详细信息，请参阅 [.NET Core CLI 扩展性模型](extensibility.md)主题。

## <a name="command-structure"></a>命令结构

CLI 命令结构包含[驱动程序（“dotnet”）](#driver)、[命令（或“谓词”）](#command-verb)，或可能的命令[参数](#arguments)和[选项](#options)。 在大部分 CLI 操作中可看到此模式，例如创建新控制台应用并从命令行运行该应用，因为从名为 *my_app* 的目录中执行时，显示以下命令：

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

```console
dotnet new console
dotnet build --output /build_output
dotnet /build_output/my_app.dll
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```console
dotnet new console
dotnet restore
dotnet build --output /build_output
dotnet /build_output/my_app.dll
```

---

### <a name="driver"></a>驱动程序

驱动程序名为 [dotnet](dotnet.md)，并具有两项职责，即运行[依赖于框架的应用](../deploying/index.md)或执行命令。 唯一一次在不使用命令的情况下使用 `dotnet` 是在将其用于启动应用程序时。

若要运行依赖于框架的应用，请在驱动程序后指定应用，例如，`dotnet /path/to/my_app.dll`。 从应用的 DLL 驻留的文件夹执行命令时，只需执行 `dotnet my_app.dll` 即可。

为驱动程序提供命令时，`dotnet.exe` 启动 CLI 命令执行过程。 首先，驱动程序确定要使用的 SDK 版本。 如果在命令选项中未指定版本，则驱动程序使用可用的最新版本。 若要指定某个版本，而不是最新安装的版本，请使用 `--fx-version <VERSION>` 选项（请参阅 [dotnet 命令](dotnet.md) 引用）。 确定 SDK 版本后，驱动程序执行命令。

### <a name="command-verb"></a>命令（“谓词”）

命令（或“谓词”）仅仅是执行操作的命令。 例如，`dotnet build` 生成代码。 `dotnet publish` 发布代码。 使用 `dotnet {verb}` 约定将命令作为控制台应用程序实现。

### <a name="arguments"></a>参数

在命令行上传递的参数是被调用的命令的参数。 例如，执行 `dotnet publish my_app.csproj` 时，`my_app.csproj` 参数指示要发布的项目，并被传递到 `publish` 命令。

### <a name="options"></a>选项

在命令行上传递的选项是被调用的命令的选项。 例如，执行 `dotnet publish --output /build_output` 时，`--output` 选项及其值被传递到 `publish` 命令。 

## <a name="migration-from-projectjson"></a>从 project.json 迁移

如果使用预览版 2 工具生成基于 *project.json* 的项目，请查阅 [dotnet 迁移](dotnet-migrate.md)主题，了解将你的项目迁移到 MSBuild/*.csproj* 以使用版本工具的信息。 对于预览版 2 工具版本之前所创建的 .NET Core 项目，按照[从 DNX 迁移到 .NET Core CLI (project.json)](../migration/from-dnx.md) 中的指南手动更新项目，然后使用 `dotnet migrate` 或直接升级项目。

## <a name="see-also"></a>请参阅

 [dotnet/CLI GitHub 存储库](https://github.com/dotnet/cli/)   
 [.NET Core 安装指南](https://aka.ms/dotnetcoregs)   
