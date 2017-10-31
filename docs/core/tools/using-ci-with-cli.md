---
title: "在持续集成 (CI) 中使用 .NET Core SDK 和工具"
description: "了解如何在生成服务器上使用 .NET Core SDK 及其工具。"
keywords: ".NET, .NET Core, 持续集成, ci, 生成, 自动化, Travis CI, AppVeyor, Visual Studio Team Services, vsts"
author: guardrex
ms.author: mairaw
ms.date: 05/18/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 0d6e1e34-277c-4aaf-9880-3ebf81023857
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 67c08dd9804f6b51961be250033161427159e66e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="using-net-core-sdk-and-tools-in-continuous-integration-ci"></a>在持续集成 (CI) 中使用 .NET Core SDK 和工具

## <a name="overview"></a>概述

本文档概述了如何在生成服务器上使用 .NET Core SDK 及其工具。 .NET Core 工具集既可以交互方式运行（当开发者在命令提示符处键入命令时），也可以自动运行（当持续集成 (CI) 服务器运行生成脚本时）。 命令、选项、输入和输出都相同，可通过提供的唯一内容来获取用于生成应用的工具和系统。 本文档重点介绍了 CI 工具获取方案，并提供了有关如何设计和构建生成脚本的建议。

## <a name="installation-options-for-ci-build-servers"></a>CI 生成服务器的安装选项

### <a name="using-the-native-installers"></a>使用本机安装程序

本机安装程序适用于 macOS、Linux 和 Windows。 安装程序需要拥有对生成服务器的管理员 (sudo) 访问权限。 使用本机安装程序的优势在于，可以安装运行工具所需的全部本机依赖项。 本机安装程序还可以在整个系统内安装 SDK。

macOS 用户应使用 PKG 安装程序。 在 Linux 上，可选择使用基于源的包管理器（如用于 Ubuntu 的 apt-get 或用于 CentOS 的 yum），也可以选择使用包本身（即 DEB 或 RPM）。 在 Windows 上，使用 MSI 安装程序。

有关最新的稳定二进制文件，请参阅 [.NET Core 入门](https://aka.ms/dotnetcoregs)。 若要使用最新（但可能不稳定）的预览版工具，请使用 [dotnet/cli GitHub 存储库](https://github.com/dotnet/cli#installers-and-binaries)中提供的链接。 对于 Linux 发行版本，可以使用 `tar.gz` 存档（亦称为 `tarballs`）；使用存档中的安装脚本来安装 .NET Core。

### <a name="using-the-installer-script"></a>使用安装程序脚本

使用安装程序脚本，可以在生成服务器上执行非管理员安装，并能轻松实现自动化，以便获取工具。 安装程序脚本负责下载并将工具提取到默认或指定位置，以供使用。 还可以指定要安装的工具版本，以及是要安装整个 SDK，还是仅安装共享运行时。

安装程序脚本在开始生成时自动运行，以提取和安装相应版本的 SDK。 相应版本是指生成项目所需的任意 SDK 版本。 使用安装程序脚本，可以在服务器的本地目录中安装 SDK，并能从安装位置运行工具，还可以在生成后进行清理（或让 CI 服务进行清理）。 这样，可以封装和隔离整个生成进程。 有关安装脚本参考，请参阅 [dotnet-install](dotnet-install-script.md) 主题。

> [!NOTE]
> 使用安装程序脚本时，不会自动安装本机依赖项。 如果操作系统没有本机依赖项，必须手动安装。 请参阅 [.NET Core 本机先决条件](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md)主题中的先决条件列表。

## <a name="ci-setup-examples"></a>CI 安装示例

此部分介绍了如何使用 PowerShell 或 bash 脚本进行手动安装，同时还介绍了多个服务型软件 (SaaS) CI 解决方案。 涵盖的 SaaS CI 解决方案包括 [Travis CI](https://travis-ci.org/)、[AppVeyor](https://www.appveyor.com/) 和 [Visual Studio Team Services 生成](https://www.visualstudio.com/docs/build/overview)。

### <a name="manual-setup"></a>手动安装

每个 SaaS 服务都有自己的生成进程创建和配置方法。 如果使用与所列不同的 SaaS 解决方案，或需要超越预封装支持范围的自定义设置，至少必须执行一些手动配置。

一般来说，手动安装需要获取一个版本的工具（或最新每日版工具），再运行生成脚本。 可以使用 PowerShell 或 bash 脚本安排 .NET Core 命令，也可以使用概述生成进程的项目文件。 [业务流程部分](#orchestrating-the-build)详细介绍了这些选项。

创建执行手动 CI 生成服务器安装的脚本后，在开发计算机上使用它来生成本地代码以供测试。 确认此脚本可以在本地正常运行后，将它部署到 CI 生成服务器。 下面展示了相对简单的 PowerShell 脚本，以说明如何获取 .NET Core SDK，并将它安装到 Windows 生成服务器上：

```powershell
$ErrorActionPreference="Stop"
$ProgressPreference="SilentlyContinue"

# $LocalDotnet is the path to the locally-installed SDK to ensure the 
#   correct version of the tools are executed.
$LocalDotnet=""
# $InstallDir and $CliVersion variables can come from options to the 
#   script.
$InstallDir = "./cli-tools"
$CliVersion = "1.0.1"

# Test the path provided by $InstallDir to confirm it exists. If it 
#   does, it's removed. This is not strictly required, but it's a 
#   good way to reset the environment.
if (Test-Path $InstallDir)
{
    rm -Recurse $InstallDir
}
New-Item -Type "directory" -Path $InstallDir

Write-Host "Downloading the CLI installer..."

# Use the Invoke-WebRequest PowerShell cmdlet to obtain the 
#   installation script and save it into the installation directory.
Invoke-WebRequest `
    -Uri "https://raw.githubusercontent.com/dotnet/cli/rel/1.0.1/scripts/obtain/dotnet-install.ps1" `
    -OutFile "$InstallDir/dotnet-install.ps1"

Write-Host "Installing the CLI requested version ($CliVersion) ..."

# Install the SDK of the version specified in $CliVersion into the 
#   specified location ($InstallDir).
& $InstallDir/dotnet-install.ps1 -Version $CliVersion `
    -InstallDir $InstallDir

Write-Host "Downloading and installation of the SDK is complete."

# $LocalDotnet holds the path to dotnet.exe for future use by the 
#   script.
$LocalDotnet = "$InstallDir/dotnet"

# Run the build process now. Implement your build script here.
```

在此脚本末尾提供生成进程的实现代码。 此脚本先获取工具，再执行生成进程。 对于 UNIX 计算机，下面的 bash 脚本以类似方式执行 PowerShell 脚本中所述的操作：

```bash
#!/bin/bash
# Do not use an INSTALLDIR path containing spaces:
#   https://github.com/dotnet/cli/issues/5281
INSTALLDIR="cli-tools"
CLI_VERSION=1.0.1
DOWNLOADER=$(which curl)
if [ -d "$INSTALLDIR" ]
then
    rm -rf "$INSTALLDIR"
fi
mkdir -p "$INSTALLDIR"
echo Downloading the CLI installer.
$DOWNLOADER https://raw.githubusercontent.com/dotnet/cli/rel/1.0.1/scripts/obtain/dotnet-install.sh > "$INSTALLDIR/dotnet-install.sh"
chmod +x "$INSTALLDIR/dotnet-install.sh"
echo Installing the CLI requested version $CLI_VERSION. Please wait, installation may take a few minutes.
"$INSTALLDIR/dotnet-install.sh" --install-dir "$INSTALLDIR" --version $CLI_VERSION
if [ $? -ne 0 ]
then
    echo Download of $CLI_VERSION version of the CLI failed. Exiting now.
    exit 0
fi
echo The CLI has been installed.
LOCALDOTNET="$INSTALLDIR/dotnet"
# Run the build process now. Implement your build script here.
```

### <a name="travis-ci"></a>Travis CI

可以将 [Travis CI](https://travis-ci.org/) 配置为使用 `csharp` 语言和 `dotnet` 键安装 .NET Core SDK。 有关详细信息，请参阅 Travis CI 官方文档[生成 C#、F# 或 Visual Basic 项目](https://docs.travis-ci.com/user/languages/csharp/)。 请注意，访问 Travis CI 信息时，社区维护的 `language: csharp` 语言标识符适用于所有 .NET 语言，包括 F# 和 Mono。

Travis CI 可同时在生成矩阵中运行 macOS（OS X 10.11、OS X 10.12）和 Linux (Ubuntu 14.04) 作业。在生成矩阵中，可以指定运行时、环境和排除项/包含项的组合，从而涵盖应用的生成组合。 有关详细信息，请参阅 Travis CI 文档 [.travis.yml 示例](https://github.com/dotnet/docs/blob/master/.travis.yml)文件和[自定义生成](https://docs.travis-ci.com/user/customizing-the-build)。 基于 MSBuild 的工具在包中添加 LTS (1.0.x) 和最新 (1.1.x) 运行时；因此，通过安装 SDK，可以收到执行生成所需的一切。

### <a name="appveyor"></a>AppVeyor

[AppVeyor](https://www.appveyor.com/) 使用 `Visual Studio 2017` 生成辅助角色映像安装 .NET Core 1.0.1 SDK。 可以使用其他包含不同版本 .NET Core SDK 的生成映像；有关详细信息，请参阅 AppVeyor 文档中的 [appveyor.yml 示例](https://github.com/dotnet/docs/blob/master/appveyor.yml)和[生成辅助角色映像](https://www.appveyor.com/docs/build-environment/#build-worker-images)主题。

.NET Core SDK 二进制文件通过安装脚本下载并解压缩到子目录，再添加到 `PATH` 环境变量。 添加生成矩阵可以运行包含多个版本 .NET Core SDK 的集成测试：

```yaml
environment:
  matrix:
    - CLI_VERSION: 1.0.1
    - CLI_VERSION: Latest

install:
  # See appveyor.yml example for install script
```

### <a name="visual-studio-team-services-vsts"></a>Visual Studio Team Services (VSTS)

将 Visual Studio Team Services (VSTS) 配置为使用以下方法之一生成 .NET Core 项目：

1. 使用命令运行[手动安装步骤](#manual-setup)中的脚本。
1. 创建包含多个 VSTS 内置生成任务的生成，这些任务被配置为使用 .NET Core。

这两种均为有效解决方案。 使用手动安装脚本，可以控制收到的工具版本，因为工具是作为生成的一部分进行下载。 此生成是通过必须创建的脚本进行运行。 本主题仅涉及手动选项。 若要详细了解如何撰写包含 VSTS 生成任务的生成，请参阅 VSTS [持续集成和部署](https://www.visualstudio.com/docs/build/overview)主题。

若要在 VSTS 中使用手动安装脚本，请新建生成定义，并指定要对生成步骤运行的脚本。 为此，请使用 VSTS 用户界面：

1. 首先，新建生成定义。 到达可以定义要创建的生成类型的屏幕后，选择“空”选项。

   ![选择空的生成定义](./media/using-ci-with-cli/screen1.png)

1. 配置要生成的存储库后，将转到生成定义。 选择“添加生成步骤”：

   ![添加生成步骤](./media/using-ci-with-cli/screen2.png)

1. 此时，系统会显示“任务目录”。 此目录包含在生成中使用的任务。 由于已有脚本，因此选择“PowerShell:运行 PowerShell 脚本”旁边的“添加”按钮。

   ![添加 PowerShell 脚本步骤](./media/using-ci-with-cli/screen3.png)

1. 配置生成步骤。 从要生成的存储库中添加脚本：

   ![指定要运行的 PowerShell 脚本](./media/using-ci-with-cli/screen4.png)

## <a name="orchestrating-the-build"></a>安排生成

本文档的大部分内容介绍了如何获取 .NET Core 工具和配置各种 CI 服务，并未介绍如何安排或实际生成 .NET Core 代码。 具体如何构建生成进程取决于许多因素，我们无法在本文中笼统概述。 请浏览 [Travis CI](https://travis-ci.org/)、[AppVeyor](https://www.appveyor.com/) 和 [VSTS](https://www.visualstudio.com/docs/build/overview) 文档集中提供的资源和示例，详细了解如何使用每种技术安排生成。

使用 .NET Core 工具构建 .NET Core 代码生成进程的两种常规方法是，直接使用 MSBuild 或使用 .NET Core 命令行命令。 应采用哪种方法取决于对方法的熟悉程度和复杂性取舍。 使用 MSBuild，可以将生成进程表达为任务和目标，但需要学习 MSBuild 项目文件语法，这增加了复杂性。 使用 .NET Core 命令行工具可能更为简单，但需要在 `bash` 或 PowerShell 等脚本语言中编写业务流程逻辑。

## <a name="see-also"></a>请参阅

[Ubuntu 获取步骤](https://www.microsoft.com/net/core#linuxubuntu)   

