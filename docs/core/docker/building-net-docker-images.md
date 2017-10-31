---
title: "生成 .NET Core Docker 映像"
description: "了解 Docker 映像和 .NET Core"
keywords: .NET, .NET Core, Docker
author: spboyer
ms.author: shboyer
ms.date: 09/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-docker
ms.devlang: dotnet
ms.assetid: 03c28597-7e73-46d6-a9c3-f9cb55642739
ms.translationtype: HT
ms.sourcegitcommit: a0b6edbc13fddd8558f6677d25ce279147d761c3
ms.openlocfilehash: efec7e390f029d2f0ab952e316976ad1c6408b0f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/06/2017

---

#<a name="building-docker-images-for-net-core-applications"></a>为 .NET Core 应用程序生成 Docker 映像

 
> [!IMPORTANT]
> 我们正在针对 .NET Core 2.0 更新本文。 下列说明已过期。 对于带来的任何不便，我们深表歉意！

若要了解如何将 .NET Core 和 Docker 配合使用，首先必须了解所提供的不同 Docker 映像以及何时使用才是正确的。 下面将介绍所提供的变体、生成 ASP.NET Core Web API，使用 Yeoman Docker 工具以创建可调试容器的内容，以及快速浏览了 Visual Studio Code 如何在该过程中起到辅助的作用。 

## <a name="docker-image-optimizations"></a>Docker 映像优化

为开发人员生成 Docker 映像时，侧重于以下三种主要方案：

- 用于开发 .NET Core 应用的映像
- 用于生成 .NET Core 应用的映像
- 用于运行 .NET Core 应用的映像

为什么是三个映像？
因为在开发、生成和运行容器化应用程序时，具有不同的优先级。
- **开发：**决定循环访问更改的速度以及调试更改的能力。 与更改代码并且快速查看相比，映像的大小则不是那么重要。 一些用于 Visual Studio Code 的工具（如 [yo docker](https://aka.ms/yodocker)）在开发期间使用此映像。 
- **生成：**编译应用所需的内容。 这包括编译器和任何优化二进制文件的其他依赖项。 此映像不是部署的映像，而是用于生成放置在生产映像中的内容的映像。 此映像将用于持续集成或者生成环境中。 例如，生成代理会以生成映像为实例，使用生成包含在映像内的应用所需的全部依赖项来编译应用程序，而不是直接在生成代理上安装所有的依赖项。 生成代理只需要了解如何运行此 Docker 映像即可。 
- **生产：**决定部署和启动映像的速度。 此映像很小，因此可以快速地通过网络从 Docker 注册表传输到 Docker 主机。 已准备运行内容，以此实现从 Docker 运行到处理结果的最快时间。 在不可变 Docker 模型中，不需要动态编译代码。 放置在此映像中的内容将限制为运行应用程序所需的二进制文件和内容。 例如，使用 `dotnet publish` 的已发布输出，其中包含已编译的二进制文件、映像、.js 和 .css 文件。 随着时间的推移，用户将看到包含预实时编译的包。  

虽然 .NET Core 映像有多个版本，但它们全都共享一个或多个层。 存储所需的磁盘空间量或从注册表中拉取的增量比整个磁盘空间量要小得多，因为所有映像都共享同一基本层，或可能共享其他层。  

## <a name="docker-image-variations"></a>Docker 映像变体

为了实现上述目标，我们在 [microsoft/dotnet](https://hub.docker.com/r/microsoft/dotnet/) 下提供了映像变体。

- `microsoft/dotnet:<version>-sdk`：即 **microsoft/dotnet:1.0.0-preview2-sdk**，此映像包含带有 .NET Core 和命令行工具 (CLI) 的 .NET Core SDK。 此映像将映射到**开发方案**。 使用此映像进行本地开发、调试和单元测试。 例如，在签入代码前进行的所有开发。 此映像还可用于**生成**方案。

- `microsoft/dotnet:<version>-core`：即 **microsoft/dotnet:1.0.0-core**，它是运行[可移植 .NET Core 应用程序](../deploying/index.md)的映像，并且针对在**生产**中运行应用程序进行了优化。 它不包含 SDK，并且会使用 `dotnet publish` 的优化输出。 可移植运行时非常适合 Docker 容器方案，因为共享的映像层利于运行多个容器。  

## <a name="alternative-images"></a>备用映像

除了开发、生成和生产的优化方案外，我们还提供了其他映像：

- `microsoft/dotnet:<version>-onbuild`：即 **microsoft/dotnet:1.0.0-preview2-onbuild**，其中包含 [ONBUILD](https://docs.docker.com/engine/reference/builder/#/onbuild) 触发器。 生成将 [COPY](https://docs.docker.com/engine/reference/builder/#/copy)（复制）应用程序，运行 `dotnet restore` 并创建 [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#/entrypoint) `dotnet run` 指令，以在运行 Docker 映像时运行该应用程序。 在使用未针对生产进行优化的映像时，某些用户可能发现只将源代码复制到映像中并运行它会很有帮助。 

- `microsoft/dotnet:<version>-core-deps`：即 **microsoft/dotnet:1.0.0-core-deps**，请在希望运行独立应用程序时使用此映像。 它包括具有 .NET Core 所需的所有本机依赖项的操作系统。 此映像也可用作自己自定义 CoreFX 或 CoreCLR 版本的基本映像。 虽然 onbuild 变量已优化为只将代码放入映像并运行它，但此映像已优化为只包含运行 .NET Core 应用程序（将 .NET 运行时与应用程序一起打包）所需的操作系统依赖项。 通常，优化此映像不是为了在同一主机上运行多个 .NET Core 容器，因为每个映像在应用程序内都具有 .NET Core 运行时，映像分层则不会带来益处。   

每个变体的最新版本：

- `microsoft/dotnet` 或 `microsoft/dotnet:latest`（包括 SDK）
- `microsoft/dotnet:onbuild`
- `microsoft/dotnet:core`
- `microsoft/dotnet:core-deps`

以下是开发计算机上使用 `docker pull <imagename>` 命令后出现的映像列表，其中显示多个映像的大小。 请注意，其中开发/生成变体 `microsoft/dotnet:1.0.0-preview2-sdk` 较大，因为它包含用于开发和生成应用程序的 SDK。 生产变体 `microsoft/dotnet:core` 较小，因为它仅包含 .NET Core 运行时。 虽然能够在 Linux 上使用的最小映像 `core-deps` 较小，但应用程序仍需要使用它复制 .NET 运行时的私有副本。 由于容器已是私有的隔离屏障，因此运行多个基于 dotnet 的容器时优化会失效。 

```
REPOSITORY          TAG                     IMAGE ID            SIZE
microsoft/dotnet    1.0.0-preview2-onbuild  19b6a6c4b1db        540.4 MB
microsoft/dotnet    onbuild                 19b6a6c4b1db        540.4 MB
microsoft/dotnet    1.0.0-preview2-sdk      a92c3d9ad0e7        540.4 MB
microsoft/dotnet    core                    5224a9f2a2aa        253.2 MB
microsoft/dotnet    1.0.0-core-deps         c981a2eebe0e        166.2 MB
microsoft/dotnet    core-deps               c981a2eebe0e        166.2 MB
microsoft/dotnet    latest                  03c10abbd08a        540.4 MB
microsoft/dotnet    1.0.0-core              b8da4a1fd280        253.2 MB
```

## <a name="prerequisites"></a>先决条件

若要生成和运行，需要安装以下几个程序：

- [.NET Core](http://dot.net)
- [Docker](https://www.docker.com/products/docker)：能够在本地运行 Docker 容器
- [Node.js](https://nodejs.org/)
- [适用于 ASP.NET 的 Yeoman 生成器](https://github.com/omnisharp/generator-aspnet)：用于创建 Web API 应用程序
- 来自 Microsoft 的[适用于 Docker 的 Yeoman 生成器](http://aka.ms/yodocker)

使用 npm 安装适用于 ASP.NET Core 和 Docker 的 Yeoman 生成器 

```
npm install -g yo generator-aspnet generator-docker
```

> [!NOTE]
> 此示例将使用适用于编辑器的 [Visual Studio Code](http://code.visualstudio.com)。

## <a name="creating-the-web-api-application"></a>创建 Web API 应用程序

对于引用点，在容器化应用程序之前，请先在本地运行应用程序。 

完成的应用程序位于 [GitHub 上的 dotnet/docs 存储库](https://github.com/dotnet/docs/tree/master/samples/core/docker/building-net-docker-images)。 有关下载说明，请参阅[示例和教程](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)。

为应用程序创建目录。

打开命令或该目录中的终端会话，然后通过键入以下内容使用 ASP.NET Yeoman 生成器：
```
yo aspnet
```

选择“Web API 应用程序”，键入应用名称的 **api**，然后点击进入。  搭建好应用程序后，更改为 `/api` 目录，并使用 `dotnet restore` 还原 NuGet 依赖项。

```
cd api
dotnet restore
```

使用 `dotnet run` 测试应用程序并浏览到 **http://localhost:5000/api/values**

```javascript
[
    "value1",
    "value2"
]
```

使用 `Ctrl+C` 停止应用程序。

## <a name="adding-docker-support"></a>添加 Docker 支持

使用来自 Microsoft 的 Yeoman 生成器可向项目添加 Docker 支持。 目前它通过创建有助于在容器内生成并运行项目的 Dockerfile 和脚本，以支持 .NET Core、Node.js 和 Go 项目。 还添加了特定于 Visual Studio Code 的文件（launch.json、tasks.json），用于编辑器调试和命令面板支持。

```console
$ yo docker

     _-----_     ╭──────────────────────────╮
    |       |    │   Welcome to the Docker  │
    |--(o)--|    │        generator!        │
   `---------´   │     Let's add Docker     │
    ( _´U`_ )    │  container magic to your │
    /___A___\   /│           app!           │
     |  ~  |     ╰──────────────────────────╯
   __'.___.'__
 ´   `  |° ´ Y `

? What language is your project using? (Use arrow keys)
❯ .NET Core
  Golang
  Node.js
```

- 选择 `.NET Core` 作为项目类型
- `rtm` 用作 .NET Core 的版本
- `Y` 表示项目使用 Web 服务器
- `5000` 是 Web API 应用程序正在侦听的端口数 (http://localhost:5000)
- `api` 用作映像名称
- `api` 用作服务名称
- `api` 用作组成项目 
- `Y` 表示要覆盖当前 Dockerfile

完成生成器时，以下文件将添加到项目中

- .vscode/launch.json
- Dockerfile.debug
- Dockerfile
- docker-compose.debug.yml
- docker-compose.yml
- dockerTask.ps1
- dockerTask.sh
- .vscode/tasks.json

生成器将创建两个 Dockerfile。

**Dockerfile.debug** - 此文件基于从映像变体的列表中的 **microsoft/dotnet:1.0.0-preview2-sdk** 映像（如有注意到），其中包括 SDK、CLI 和.NET Core，而这是用于开发和调试 (F5) 的映像。 包括所有这些组件将生成大约为 540MB 的较大映像。

**Dockerfile** - 此映像是基于 **microsoft/dotnet:1.0.0-core** 的发布映像，并且应该用于生产。 此映像生成时大约为 253MB。

### <a name="creating-the-docker-images"></a>创建 Docker 映像
使用 `dockerTask.sh` 或 `dockerTask.ps1` 脚本，可以生成或编写用于特定环境的 **api** 应用程序的映像和容器。 运行以下命令生成**调试**映像。

```bash
./dockerTask.sh build debug
```

映像将生成 ASP.NET 应用程序，运行 `dotnet restore`，将调试程序添加到映像，设置 `ENTRYPOINT`，最后将应用复制到该映像。 结果是名为 *api* 的 Docker 映像，并且具有 *debug* 的 `TAG`。  使用 `docker images` 查看计算机上的映像。

```bash
docker images

REPOSITORY          TAG                  IMAGE ID            CREATED             SIZE
api                 debug                70e89fbc5dbe        a few seconds ago   779.8 MB
```

生成映像并在 Docker 容器内运行应用程序的另一种方法是在 Visual Studio Code 中打开该应用程序，然后使用调试工具。 

在 Visual Studio Code 左侧的“视图栏”中，选择“调试”图标。

![vscode 调试图标](./media/building-net-docker-images/debugging_debugicon.png)

然后点击“播放”图标或按 F5 生成映像并在容器内启动该应用程序。 会使用默认的 Web 浏览器在 http://localhost:5000 中启动 Web API。

![VSCode Docker 工具调试](./media/building-net-docker-images/docker-tools-vscode-f5.png)

可以在应用程序中以及单步调试等过程中设置断点，就如在开发计算机上本地运行应用程序一样，而不是在容器内运行。 利于在容器内进行调试的映像需要是将部署到生产环境的同一映像。

创建发布或生产映像只需从传递 `release` 环境名称的终端中运行命令即可。

```bash
./dockerTask build release
```

命令会基于较小的 **microsoft / dotnet:core** 基本映像和 [EXPOSE](https://docs.docker.com/engine/reference/builder/#/expose) 端口 5000 创建映像，为 `dotnet api.dll`设置 [ENTYRPOINT](https://docs.docker.com/engine/reference/builder/#/entrypoint)，然后将其复制到 `/app` 目录。 在如此小的映像中不会生成任何调试程序、SDK 或 `dotnet restore`。 映像名为 **api**，并且具有**最新**的 `TAG`。

```
REPOSITORY          TAG                  IMAGE ID            CREATED             SIZE
api                 debug                70e89fbc5dbe        1 hour ago        779.8 MB
api                 latest               ef17184c8de6        1 hour ago        260.7 MB
```

## <a name="summary"></a>摘要

使用 Docker 生成器将必要的文件添加到 Web API 应用程序，简化了创建映像的开发和生产版本的过程。  同时通过在对容器内的应用程序提供单步调试的 Windows 和 Visual Studio Code 集成上提供 PowerShell 脚本来达到相同结果，使工具也实现了跨平台。 通过了解映像变体和目标场景，可以优化内部循环开发过程，同时实现为生产部署优化映像。  



