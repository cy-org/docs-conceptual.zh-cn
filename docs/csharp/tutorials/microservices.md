---
title: "Docker 中托管的微服务 - C#"
description: "了解如何创建在 Docker 容器中运行的 ASP.NET Core 服务"
keywords: ".NET, .NET Core, Docker, C#, ASP.NET, 微服务"
author: BillWagner
ms.author: wiwagn
ms.date: 02/03/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-docker
ms.devlang: csharp
ms.assetid: 87e93838-a363-4813-b859-7356023d98ed
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 5585db33fb5020ed18c26f32ce0b63f97353d20f
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="microservices-hosted-in-docker"></a>Docker 中托管的微服务

## <a name="introduction"></a>介绍

此教程将详细介绍在 Docker 容器中生成和部署 ASP.NET Core 微服务时必须完成的任务。 在此教程中，你将了解：

* 如何使用 Yeoman 生成 ASP.NET Core 应用程序
* 如何创建 Docker 开发环境
* 如何根据现有映像生成 Docker 映像。
* 如何将服务部署到 Docker 容器中。

与此同时，你还将了解下面这些 C# 语言功能：

* 如何将 C# 对象转换成 JSON 有效负载。
* 如何生成不可变的数据传输对象
* 如何处理传入的 HTTP 请求并生成 HTTP 响应
* 如何使用可以为 null 的值类型

你可以[查看或下载本主题的示例应用](https://github.com/dotnet/docs/tree/master/samples/csharp/getting-started/WeatherMicroservice)。 有关下载说明，请参阅[示例和教程](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)。

### <a name="why-docker"></a>为什么要使用 Docker？

使用 Docker，可以轻松地创建标准计算机映像，从而在数据中心或公有云中托管服务。 使用 Docker，可以配置映像，并根据需要复制映像来扩展应用程序安装。

此教程中的所有代码适用于任何 .NET Core 环境。
附加 Docker 安装任务适用于 ASP.NET Core 应用程序。 

## <a name="prerequisites"></a>先决条件
必须将计算机设置为运行 .Net Core。 有关安装说明，请访问 [.NET Core](https://www.microsoft.com/net/core) 页。
可以在 Windows、Ubuntu Linux、macOS 或 Docker 容器中运行此应用程序。 必须安装常用的代码编辑器。 在以下说明中，我们使用的是开放源代码跨平台编辑器 [Visual Studio Code](https://code.visualstudio.com/)。 不过，你可以使用习惯使用的任意工具。

还必须安装 Docker 引擎。 请参阅 [Docker 安装页](http://www.docker.com/products/docker)，了解适用于自己的平台的说明。
可以在许多 Linux 发行版本、macOS 或 Windows 中安装 Docker。 上面引用的页面分部分提供了各个可安装的版本。

大多数组件的安装是通过程序包管理器完成的。 如果已安装 node.js 的程序包管理器 `npm`，可跳过这一步。 否则，请从 [nodejs.org](https://nodejs.org) 下载并安装最新的 NodeJs，即会安装 npm 程序包管理器。 

此时，需要安装许多支持 ASP.NET Core 开发的命令行工具。 命令行模板使用 Yeoman、Bower、Grunt、和 Gulp。 如果已全部安装，可继续执行其他操作；否则，请在常用的命令行管理程序中键入以下命令：

`npm install -g yo bower grunt-cli gulp`

`-g` 选项指明此为全局安装，这些工具可在整个系统范围内使用。 （本地安装将包限定为只能供一个项目使用。） 安装这些核心工具后，必须安装 Yeoman ASP.NET 模板生成器：

`npm install -g generator-aspnet`

## <a name="create-the-application"></a>创建应用程序

至此，你已安装所有工具，是时候新建 ASP.NET Core 应用程序了。 若要使用命令行生成器，请在常用的命令行管理程序中执行以下 Yeoman 命令：

`yo aspnet`

此命令会提示你选择要创建的应用程序类型。 对于此微服务，需要的是最简单最轻量级的 Web 应用程序，因此选择“空 Web 应用程序”。 此模板会提示你选择名称。 选择“WeatherMicroservice”。 

此模板将为你创建以下八个文件：

* 为 ASP.NET Core 应用程序定制的 .gitignore 文件。
* Startup.cs 文件。 其中包含应用程序的基本内容。
* Program.cs 文件。 其中包含应用程序的入口点。
* WeatherMicroservice.csproj 文件。 这是应用程序的生成文件。
* Dockerfile。 此脚本将创建应用程序的 Docker 映像。
* README.md 文件。 其中包含指向其他 ASP.NET Core 资源的链接。
* web.config 文件。 其中包含基本配置信息。
* runtimeconfig.template.json 文件。 其中包含 IDE 使用的调试设置。

现在可以运行模板生成的应用程序了。 为此，可通过命令行使用一系列工具。 `dotnet` 命令可运行 .NET 开发所需的工具。 每个谓词执行一个不同的命令

第一步是还原所有依赖项：

```console
dotnet restore
```

dotnet restore 使用 NuGet 程序包管理器将所有必需包安装到应用程序目录中。 还将生成 project.json.lock 文件。 此文件包含引用的各个包的相关信息。 还原所有依赖项后，生成应用程序：

```console
dotnet build
```

生成应用程序后，使用命令行运行程序：

```console
dotnet run
```

默认配置侦听的是 http://localhost:5000 。 可以打开浏览器并转到相应页面，看到的是“Hello World!” 消息。

### <a name="anatomy-of-an-aspnet-core-application"></a>ASP.NET Core 应用程序剖析

至此，已生成应用程序，让我们来看看此应用程序功能是如何实现的。 此时，生成的文件中有两个需要特别关注：project.json 和 Startup.cs。 

Project.json 包含项目相关信息。 经常要用到的两个节点是“依赖项”和“框架”。 “依赖项”节点列出了此应用程序需要的所有包。
此时，这是一个小型节点，只需要列出运行 Web 服务器的包。

“框架”节点指定了将运行此应用程序的 .NET Framework 的版本和配置。

此应用程序是在 Startup.cs 中实现。 此文件包含启动类。

ASP.NET Core 基础结构调用两种方法来配置并运行此应用程序。 `ConfigureServices` 方法描述了此应用程序所需的服务。 由于要生成的是精简的微服务，因此无需配置任何依赖项。 `Configure` 方法配置传入 HTTP 请求的处理程序。 模板生成简单的处理程序来响应所有关于文本“Hello World!”的请求。

## <a name="build-a-microservice"></a>生成微服务

要生成的服务将用于传递世界各地的天气预报。 在生产应用程序中，需要调用一些服务来检索天气数据。 在此示例中，我们将生成随机天气预报服务。 

需要执行以下许多任务，才能实现随机天气预报服务：

* 分析传入请求，读取经纬度。
* 生成一些随机预报数据。
* 将随机预报数据从 C# 对象转换成 JSON 数据包。
* 将响应头设置为指示服务发送回 JSON。
* 编写响应。

下面各部分将引导你逐一完成这些步骤。

### <a name="parsing-the-query-string"></a>分析查询字符串。

首先要分析查询字符串。 此服务接受在以下形式的查询字符串中使用“lat”和“long”自变量：

`http://localhost:5000/?lat=-35.55&long=-12.35`  

只需更改定义为启动类中 `app.Run` 的自变量的 lambda 表达式。

lambda 表达式中的自变量是请求的 `HttpContext`。 其属性之一是 `Request` 对象。 `Request` 对象具有 `Query` 属性，其中包含请求查询字符串中所有值的字典。 第一次添加的代码是为了查找经纬度值：

[!code-csharp[ReadQueryString](../../../samples/csharp/getting-started/WeatherMicroservice/Startup.cs#ReadQueryString "读取查询字符串中的变量")]

查询字典值属于 `StringValue` 类型。 此类型可以包含一系列字符串。 对于天气服务，每个值都是一个字符串。 正因如此，上面的代码调用 `FirstOrDefault()`。 

接下来，需要将字符串转换成双精度类型值。 用于将字符串转换成双精度类型值的方法是 `double.TryParse()`：

```csharp
bool TryParse(string s, out double result);
```

此方法利用 C# out 参数来指示能否将输入字符串转换成双精度类型值。 如果字符串确实是双精度类型值的有效表示形式，那么此方法会返回 true，并且 `result` 自变量中包含相应的值。 如果字符串不是双精度类型值的有效表示形式，则此方法返回 false。

能够使用返回*可以为 null 的双精度类型值*的*扩展方法*来调整此 API。 *可以为 null 的值类型*是某种值类型的类型表示形式，还可以保留缺少的值或 null 值。 可以为 null 的类型以类型声明中追加的 `?` 字符表示。 

虽然扩展方法被定义为静态方法，但可以在第一个参数中添加 `this` 修饰符，这样便能调用扩展方法，就像是相应类的成员方法一样。 只能在静态类中定义扩展方法。 下面定义了包含用于分析的扩展方法的类：

[!code-csharp[TryParseExtension](../../../samples/csharp/getting-started/WeatherMicroservice/Extensions.cs#TryParseExtension "返回可以为 null 的值的 TryParse 扩展方法")]

`default(double?)` 表达式返回 `double?` 类型的默认值。 默认值是 null（或缺少的）值。

可以使用此扩展方法将查询字符串自变量转换成双精度类型：

[!code-csharp[UseTryParse](../../../samples/csharp/getting-started/WeatherMicroservice/Startup.cs#UseTryParse "使用 TryParse 扩展方法")]

为了能够轻松测试分析代码，请将响应更新为包含以下自变量值：

[!code-csharp[WriteResponse](../../../samples/csharp/getting-started/WeatherMicroservice/Startup.cs#WriteResponse "编写输出响应")]

此时，可以运行 Web 应用程序，并检查分析代码是否有效。 在浏览器中向 Web 请求添加值，应该能够看到更新后的结果。

### <a name="build-a-random-weather-forecast"></a>生成随机天气预报

下一个任务是生成随机天气预报。 让我们从包含天气预报所需值的数据容器入手：

```csharp
public class WeatherReport
{
    private static readonly string[] PossibleConditions = new string[]
    {
        "Sunny",
        "Mostly Sunny",
        "Partly Sunny",
        "Partly Cloudy",
        "Mostly Cloudy",
        "Rain"
    };

    public int HiTemperature { get; }
    public int LoTemperature { get; }
    public int AverageWindSpeed { get; }
    public string Conditions { get; }
}
```

接下来，生成用于随机设置这些值的构造函数。 此构造函数将经纬度值用作随机数生成器的源。 也就是说，同一地理位置的天气预报也是相同的。 如果更改经纬度自变量，将会生成不同的天气预报（因为源不同）。

[!code-csharp[WeatherReportConstructor](../../../samples/csharp/getting-started/WeatherMicroservice/WeatherReport.cs#WeatherReportConstructor "WeatherReport 构造函数")]

现在可以在响应方法中生成 5 天的天气预报：

[!code-csharp[GenerateRandomReport](../../../samples/csharp/getting-started/WeatherMicroservice/Startup.cs#GenerateRandomReport "生成随机天气预报")]

### <a name="build-the-json-response"></a>生成 JSON 响应

服务器上的最后一项代码任务是，将 WeatherReport 数组转换成 JSON 数据包，然后将其发送回客户端。 首先，我们要创建 JSON 数据包。 将把 NewtonSoft JSON 序列化程序添加到依赖项列表中。 为此，请使用 `dotnet` CLI：

```
dotnet add package Newtonsoft.Json
```

然后，可以使用 `JsonConvert` 类将对象写入字符串：

[!code-csharp[ConvertToJson](../../../samples/csharp/getting-started/WeatherMicroservice/Startup.cs#ConvertToJSON "将对象转换成 JSON")]

上面的代码将 forecast 对象（`WeatherForecast` 对象列表）转换成 JSON 数据包。 构造响应数据包后，将内容类型设置为 `application/json`，并编写字符串。

应用程序现在可以运行并返回随机天气预报。

## <a name="build-a-docker-image"></a>生成 Docker 映像

最后一项任务是在 Docker 中运行应用程序。 我们将创建一个 Docker 容器，用于运行表示此应用程序的 Docker 映像。

***Docker 映像***是定义应用程序运行环境的文件。

***Docker 容器***表示 Docker 映像的正在运行实例。

通过类推，可以将 *Docker 映像*视为*类*，将 *Docker 容器*视为对象或此类的实例。  

ASP.NET 模板创建的 Dockerfile 可供我们自行使用。 我们先来介绍一下此文件的内容。

第一行指定的是源映像：

```
FROM microsoft/dotnet:1.1-sdk-msbuild
```

通过 Docker，可以根据源模板配置计算机映像。 也就是说，开始时并不需要提供所有计算机参数，只需提供全部更改。 此处所说的更改包括我们的应用程序在内。

在这第一个示例中，我们将使用 .NET 映像的 `1.1-sdk-msbuild` 版本。 这是创建有效 Docker 环境的最简单方式。 此映像包括 .NET Core 运行时和 .NET SDK。 这样更便于着手生成映像，但创建的映像会比较大。

接下来的五行代码用于设置并生成应用程序：

```
WORKDIR /app

# copy csproj and restore as distinct layers

COPY WeatherMicroservice.csproj .
RUN dotnet restore

# copy and build everything else

COPY . .

# RUN dotnet restore
RUN dotnet publish -c Release -o out
```

这会将当前目录中的项目文件复制到 Docker VM 中，并还原所有包。 使用 .NET CLI 意味着 Docker 映像必须包含 .NET Core SDK。 完成上述操作之后，应用程序的其余部分会得到复制，然后 .NET 发布命令会生成并打包应用程序。

此文件的最后一行代码用于运行应用程序：

```
ENTRYPOINT ["dotnet", "out/WeatherMicroservice.dll", "--server.urls", "http://0.0.0.0:5000"]
```

Dockerfile 最后一行代码中 `dotnet` 的 `--server.urls` 自变量引用此配置端口。 `ENTRYPOINT` 命令用于指示 Docker 哪些命令和命令行选项启动了服务。 

## <a name="building-and-running-the-image-in-a-container"></a>在容器中生成并运行映像

让我们在 Docker 容器中生成映像并运行服务。 不是要将本地目录中的所有文件都复制到映像中， 而是要在容器中生成应用程序。 将创建 `.dockerignore` 文件来指定不要复制到映像中的目录。 你不想复制任何生成资产。 请在 `.dockerignore` 文件中指定生成和发布目录：

```
bin/*
obj/*
out/*
```

使用 Docker 生成命令生成映像。 从包含代码的目录运行以下命令。

```console
docker build -t weather-microservice .
```

此命令将根据 Dockerfile 中的所有信息生成容器映像。 `-t` 自变量提供此容器映像的标记或名称。 在上面的命令行中，Docker 容器的标记是 `weather-microservice`。 此命令完成后，就生成了一个可用于运行新服务的容器。 

运行以下命令，启动容器和服务：

```console
docker run -d -p 80:5000 --name hello-docker weather-microservice
```

`-d` 选项表示运行从当前终端拆离出来的容器。 也就是说，终端中不会显示命令输出。 `-p` 选项指示服务和主机之间的端口映射。 即指应将端口 80 上的所有传入请求都转发到容器上的端口 5000。 在上面的 Dockerfile 中指定的命令行自变量中，使用 5000 匹配服务要侦听的端口。 `--name` 自变量用于命名正在运行的容器。 此名称可方便与容器结合使用。 

可以运行以下命令来确定映像能否正常运行：

```console
docker ps
```

如果容器能正常运行，那么正在运行的进程中就会有一行列出它来 （可能是唯一一行）。

可以打开浏览器并转到 localhost，然后指定经纬度，从而测试服务：

```
http://localhost/?lat=35.5&long=40.75
```

## <a name="attaching-to-a-running-container"></a>附加到正在运行的容器

在命令窗口中运行服务时，可以查看针对各个请求打印输出的诊断信息。 如果容器是在拆离模式下运行，则看不到此类信息。 使用 Docker 附加命令，可以将窗口附加到正在运行的容器，以便查看日志信息。  在命令窗口中运行以下命令：

```console
docker attach --sig-proxy=false hello-docker
```

`--sig-proxy=false` 自变量表示 `Ctrl-C` 命令未发送到容器进程，而是停止运行 `docker attach` 命令。 最后的自变量是为 `docker run` 命令中的容器命名的名称。 

> [!NOTE]
> 还可以使用 Docker 分配的容器 ID 来引用任何容器。 如果没有在 `docker run` 中命名容器，必须使用容器 ID。

打开浏览器并转到服务。 将可以在命令窗口中查看附加的正在运行的容器生成的诊断消息。

按 `Ctrl-C` 可停止附加进程。

使用完后，可以停止运行容器：

```console
docker stop hello-docker
```

容器和映像仍可供重启。  若要从计算机中删除容器，可以运行以下命令：

```console
docker rm hello-docker
```

若要从计算机中删除未使用的映像，可以运行以下命令：

```console
docker rmi weather-microservice
```

## <a name="conclusion"></a>结束语 

在此教程中，你生成了 ASP.NET Core 微服务，并添加了一些简单的功能。

此外，你还生成了此服务的 Docker 容器映像，并在计算机上运行了相应的容器。 最后，你还将终端窗口附加到了服务中，并查看服务生成的诊断消息。

与此同时，你还了解了多项 C# 语言功能的实际运用。

