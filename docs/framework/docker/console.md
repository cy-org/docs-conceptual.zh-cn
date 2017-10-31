---
title: "在 Docker 中运行控制台应用程序"
description: "了解如何利用现有 .NET Framework 控制台应用程序并在 Windows Docker 容器中运行该程序。"
author: spboyer
keywords: ".NET, 容器, 控制台, 应用程序"
ms.date: 09/28/2016
ms.topic: article
ms.prod: .net-framework
ms.technology: vs-ide-deployment
ms.devlang: dotnet
ms.assetid: 85cca1d5-c9a4-4eb2-93e6-4f878de07fd7
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 2fdce1e131eaa0d6952b2910f73105f097487711
ms.contentlocale: zh-cn
ms.lasthandoff: 08/11/2017

---

# <a name="running-console-applications-in-windows-containers"></a>在 Windows 容器中运行控制台应用程序

控制台应用程序具有多种用途；从简单的状态查询到长时间运行的文档图像处理任务。 在任何情况下，启动和缩放这些应用程序的能力始终在硬件购置、启动时间或运行多个实例方面受限。

通过移动控制台应用程序以使用 Docker 和 Windows Server 容器，可以从干净状态启动这些应用程序，使其执行操作，然后完全关闭该程序。 本主题将演示将控制台应用程序移动到基于 Windows 的容器并使用 PowerShell 脚本启动该程序所需的步骤。

本示例控制台应用程序是一个简单示例，其中具有一个参数、一个此情况下的问题，并返回随机答案。 这可能需要 `customer_id` 并处理他们的税款，或创建 `image_url` 参数的缩略图。

除答案外，已将 `Environment.MachineName` 添加到响应中，以显示在本地与在 Windows 容器中运行该应用程序的区别。 本地运行应用程序时，会返回本地计算机名称；在 Windows 容器中运行该应用程序时，则会返回容器会话 ID。

[完整示例](https://github.com/dotnet/docs/tree/master/samples/framework/docker/ConsoleRandomAnswerGenerator)位于 GitHub 上的 dotnet/docs 存储库中。 有关下载说明，请参阅[示例和教程](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)。

开始着手将应用程序移动到容器之前，需要熟悉某些 Docker 术语。

> Docker 映像是用于定义运行中容器的环境（包括操作系统 (OS)、系统组件和应用程序）的只读模板。

Docker 映像的一个重要特性是映像由基本映像组合而成。 每个新映像均会向现有映像添加小部分功能。 

> Docker 容器是映像的运行实例。 

通过在多个容器中运行同一映像来缩放应用程序。
从概念上讲，这类似于在多个主机中运行同一应用程序。

有关 Docker 体系结构的详细信息，请参阅 Docker 站点上的 [Docker 概述](https://docs.docker.com/engine/understanding-docker/)。 

移动控制台应用程序只需几个步骤。

1. [生成应用程序](#building-the-application)
1. [创建映像的 Dockerfile](#creating-the-dockerfile)
1. [生成并运行 Docker 容器的过程](#creating-the-image)

## <a name="prerequisites"></a>先决条件
[Windows 10 周年更新](https://www.microsoft.com/en-us/software-download/windows10/) 或 [Windows Server 2016](https://www.microsoft.com/en-us/cloud-platform/windows-server) 支持 Windows 容器。

> [!NOTE]
>如果使用 Windows Server 2016，则需手动启用容器，因为 Docker for Windows 安装程序不会启用该功能。 请确保已为操作系统运行所有更新，然后按照[容器主机部署](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment)文章中的说明来安装容器和 Docker 功能。

需要安装 Docker for Windows 1.12 Beta 26 版或更高版本才能支持 Windows 容器。 默认情况下，Docker 支持将基于 Linux 的容器切换到 Windows 容器，通过右键单击系统托盘中的 Docker 图标，然后选择“切换到 Windows 容器”。 Docker 将运行该过程进行更改，且可能需要重启。

![Windows 容器](./media/console/SwitchContainer.png)

## <a name="building-the-application"></a>生成应用程序
通常，通过安装程序、FTP 或文件共享部署分配控制台应用程序。 部署到容器时，需要编译资产并将其暂存到创建 Docker 映像时可以使用的位置。

在 *build.ps1* 中，脚本使用 [MSBuild](https://msdn.microsoft.com/library/dd393574.aspx) 编译应用程序以完成生成资产的任务。 有几个传递到 MSBuild 来完成所需资产的参数。 要编译的项目文件或解决方案的名称、输出位置，最后是配置（版本或调试）。

在对 `Invoke-MSBuild` 的调用中，将 `OutputPath` 设置为 **Publish**，`Configuration` 设置为 **Release**。 

```
function Invoke-MSBuild ([string]$MSBuildPath, [string]$MSBuildParameters) {
    Invoke-Expression "$MSBuildPath $MSBuildParameters"
}

Invoke-MSBuild -MSBuildPath "MSBuild.exe" -MSBuildParameters ".\ConsoleRandomAnswerGenerator.csproj /p:OutputPath=.\publish /p:Configuration=Release"
```

## <a name="creating-the-dockerfile"></a>创建 Dockerfile
用于控制台 .NET Framework 应用程序的基本映像是 [Docker 中心](https://hub.docker.com/r/microsoft/windowsservercore/)上正式推出的 `microsoft/windowsservercore`。 该基本映像包含 Windows Server 2016、.NET Framework 4.6.2 的最小安装，并充当 Windows 容器的基本 OS 映像。

```
FROM microsoft/windowsservercore
ADD publish/ /
ENTRYPOINT ConsoleRandomAnswerGenerator.exe
```
Dockerfile 中的首行使用 [`FROM`](https://docs.docker.com/engine/reference/builder/#/from) 指令指定基本映像。 接下来，文件中的 [`ADD`](https://docs.docker.com/engine/reference/builder/#/add) 将应用程序资产从 **publish** 文件夹复制到容器的根文件夹；最后，设置映像的 [`ENTRYPOINT`](https://docs.docker.com/engine/reference/builder/#/entrypoint)，表明这是将在容器启动时运行的命令或应用程序。 

## <a name="creating-the-image"></a>创建映像
为创建 Docker 映像，将以下代码添加到 *build.ps1* 脚本。 运行脚本时，使用从 MSBuild（在[生成应用程序](#building-the-application)部分定义）编译的资产创建 `console-random-answer-generator` 映像。

```powershell
$ImageName="console-random-answer-generator"

function Invoke-Docker-Build ([string]$ImageName, [string]$ImagePath, [string]$DockerBuildArgs = "") {
    echo "docker build -t $ImageName $ImagePath $DockerBuildArgs"
    Invoke-Expression "docker build -t $ImageName $ImagePath $DockerBuildArgs"
}

Invoke-Docker-Build -ImageName $ImageName -ImagePath "."
```

使用 PowerShell 命令提示符中的 `.\build.ps1` 运行该脚本。

生成完成后，使用命令行或 PowerShell 提示符中的 `docker images` 命令，可以看到已创建该映像并可随时运行。

```
REPOSITORY                        TAG                 IMAGE ID            CREATED             SIZE
console-random-answer-generator   latest              8f7c807db1b5        8 seconds ago       7.33 GB
```

## <a name="running-the-container"></a>运行容器
可以使用 Docker 命令从命令行启动该容器。

```
docker run console-random-answer-generator "Are you a square container?"
```

输出为

```
The answer to your question: 'Are you a square container?' is Concentrate and ask again on (70C3D48F4343)
```

如果从 PowerShell 运行 `docker ps -a` 命令，则可以看到该容器仍然存在。

```
CONTAINER ID        IMAGE                             COMMAND                  CREATED             STATUS                          
70c3d48f4343        console-random-answer-generator   "cmd /S /C ConsoleRan"   2 minutes ago       Exited (0) About a minute ago      
```

STATUS 列显示“大约 1 分钟前”，已完成并可关闭该应用程序。 如果该命令运行了一百次，则会存在一百个无工作的静态容器。 开始时，理想操作是完成工作并关闭或清理程序。 若要完成该工作流，将 `--rm` 选项添加到 `docker run` 命令会在收到 `Exited` 信号后立即删除该容器。

```
docker run --rm console-random-answer-generator "Are you a square container?"
```

运行带有此选项的命令，然后查看 `docker ps -a` 命令的输出；请注意，容器 ID (`Environment.MachineName`) 不在列表中。

### <a name="running-the-container-using-powershell"></a>使用 PowerShell 运行容器
示例项目文件中还包含 *run.ps1*，这是如何使用 PowerShell 来运行接受参数的应用程序的示例。

若要运行，请打开 PowerShell，然后使用以下命令：

```
.\run.ps1 "Is this easy or what?"
```

## <a name="summary"></a>摘要
无需对应用程序代码进行任何更改，只需通过添加 Dockerfile 并发布应用程序，即可容器化 .NET Framework 控制台应用程序、立即利用运行多个实例的优势、洁净启动和停止，以及使用更多 Windows Server 2016 功能。

