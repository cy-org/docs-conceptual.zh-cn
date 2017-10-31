---
title: "将旧版整体式 .NET Framework 应用程序迁移到 Windows 容器"
description: "容器化 .NET 应用程序的 .NET 微服务体系结构 | 将旧版整体式 .NET Framework 应用程序迁移到 Windows 容器"
keywords: "Docker, 微服务, ASP.NET, 容器"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.translationtype: HT
ms.sourcegitcommit: 9bb64ea7199f5699ff166d1affb7f8126dcc6612
ms.openlocfilehash: 1756ff0f49d9bb243fa561ba760418eba79de1f0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/05/2017

---
# <a name="migrating-legacy-monolithic-net-framework-applications-to-windows-containers"></a>将旧版整体式 .NET Framework 应用程序迁移到 Windows 容器

Windows 容器可作为一种用于改善开发和测试环境以及部署基于旧版 .NET Framework 技术（如 Web 窗体）的应用程序的途径。以这种方式将容器用于旧版应用程序称为“直接迁移”方案。

本指南前面几节倡导了微服务体系结构，即业务应用程序分布在不同的容器中，每个应用程序运行一个小型的集中式服务。 该目标具有诸多优点。 在新的开发中，强烈建议采用这种方法。 企业关键型应用程序还非常利于证明体系结构重建和重新实现的成本。

但并不是每个应用程序都非常利于证明成本。 这并不表示这些应用程序不能用于容器方案中。

本节会探讨 eShopOnContainers 的应用程序，如图 7-1 所示。 eShopOnContainers 企业团队的成员会将此应用程序用于查看和编辑产品目录。

![](./media/image1.png)

图 7-1。 Windows 容器上的 ASP .NET Web 窗体应用程序（旧版技术）

这是用于浏览和修改目录条目的 Web 窗体应用程序。 Web 窗体依赖项表示此应用程序在不使用 Web 窗体重写后才会在 .NET Core 上运行，另外还会改用 ASP.NET Core MVC。 用户将了解如何无需更改也可以在容器中运行此类应用程序。 还会了解如何做最少的更改在混合模式中工作。在该模式下，某些功能已移到单独的微服务，但大多数功能仍保留在整体式应用程序中。

## <a name="benefits-of-containerizing-a-monolithic-application"></a>容器化整体式应用程序的优点

Catalog.WebForms 应用程序可在 eShopOnContainers GitHub 存储库 (<https://github.com/dotnet/eShopOnContainers>) 中获得。 此应用程序是独立的 Web 应用程序，可访问高可用性数据存储。 即便如此，在容器中运行应用程序仍有其优势。 创建应用程序的映像。 自此，每个部署会在相同的环境中运行。 每个容器会使用相同的操作系统版本，安装相同版本的依赖项，使用同一个框架，并通过同一个流程生成。 可在图 7-2 看到 Visual Studio 2017 中加载的应用程序。

![](./media/image2.png)

**图 7-2**。 Visual Studio 2017 中的目录管理 Web 窗体应用程序

此外，开发人员均可在此一致的环境中运行该应用程序。 仅某些版本出现的问题会立即报告给开发人员，而不会出现在暂存或生产环境中。 应用程序在容器中运行后，开发团队的开发环境之间的差异将不那么重要。

最后，容器化应用程序具有较为平缓的的横向扩展曲线。 你已了解容器化应用如何在 VM 中启用多个容器或如何在物理计算机中启用多个容器。 这会转换为需求更少的更高密度的资源。

综上所述，请考虑使用“直接迁移”操作在 Docker 容器中运行旧版整体式应用。 “直接迁移”一词说明了任务的范围：将整个应用程序从物理计算机或虚拟机中迁出，再移到容器中。 理想情况下，不需要对应用程序做任何更改，即可在容器中运行。

## <a name="possible-migration-paths"></a>可能的迁移路径

作为整体式应用程序，Catalog.Webforms 应用程序是一个包含所有代码的 Web 应用程序，其中包括数据访问库。 数据库在单独的高可用性计算机中运行。 在示例代码中通过使用模拟目录服务模拟该配置：可以针对该模拟数据运行 Catalog.WebForms 应用程序，模拟纯“直接迁移”方案。 此示例演示了最简单的迁移路径，通过该路径可将现有的资产移动到容器中进行运行，无需更改任何代码。 此路径适用于与要移动到微服务的功能交互最少的完整应用程序。

但是，eShopOnContainers 网站已经使用适用于不同方案的微服务访问数据存储。 可以另外略微改动目录编辑器，以利用目录微服务，而不是直接访问目录数据存储。

这些更改可演示自己应用程序的演变。 从不做任何更改将现有应用程序移动到容器，到略微更改，使现有应用程序能够访问某些新的微服务，再到完全重写应用程序，以完全加入一个新的基于微服务的体系结构。 正确的路径取决于迁移成本和迁移收益。

## <a name="application-tour"></a>应用程序教程

可以加载 Catalog.WebForms 解决方案，并将该应用程序作为一个独立的应用程序运行。 在此配置中，而非持久性存储数据库中，该应用程序会使用模拟服务返回数据。 应用程序使用 Autofac (<https://autofac.org/>) 作为控制 (IOC) 容器反转。 使用依赖项注入 (DI)，可以将应用程序配置为使用模拟数据或实时目录数据服务。 （我们很快会详细介绍 DI。）启动代码会从 web.config 文件中读取 useFake 设置，并将 Autofac 容器配置为注入模拟数据服务或实时目录服务。 如果在 web.config 文件中使用设置为“false”的 useFake 运行应用程序，则会看到 Web 窗体应用程序显示目录数据。

使用过 Web 窗体的人应该会非常熟悉在此应用程序中使用的大多数技术。 但是，目录微服务会引入两项可能比较陌生的技术：之前提到的依赖项注入 (DI) 和与 Web 窗体中的异步数据存储配合使用。

对于分配所有所需资源的写入类，DI 会反转其面向对象的典型策略。 而类会从服务容器请求其依赖项。 DI 的优点是可以将外部服务替换为模拟服务，以支持测试或其他环境。

DI 容器使用 web.config appSettings 配置控制使用模拟目录数据还是使用正在运行的服务中的实时数据。 应用程序会注册生成容器的 HttpModule 对象，然后注册预先请求的处理程序，以注入依赖项。 可以在 Modules/AutoFacHttpModule.cs 文件中看到该代码，如以下示例所示：

```cs
private static IContainer CreateContainer()
{
  // Configure AutoFac:
  // Register Containers:

  var settings = WebConfigurationManager.AppSettings;
  var useFake = settings["usefake"];
  bool fake = useFake == "true";
  var builder = new ContainerBuilder();

  if (fake)
  {
    builder.RegisterType<CatalogMockService>()
    .As<ICatalogService>();
  }
  else
  {
    builder.RegisterType<CatalogService>()
    .As<ICatalogService>();
    builder.RegisterType<RequestProvider>()
    .As<IRequestProvider>();
  }

  var container = builder.Build();
  return container;
}

private void InjectDependencies()
{
  if (HttpContext.Current.CurrentHandler is Page page)
  {
    // Get the code-behind class that we may have written
    var pageType = page.GetType().BaseType;

    // Determine if there is a constructor to inject, and grab it
    var ctor = (from c in pageType.GetConstructors()
                where c.GetParameters().Length > 0
                select c).FirstOrDefault();

    if (ctor != null)
    {
      // Resolve the parameters for the constructor
      var args = (from parm in ctor.GetParameters()
                  select Container.Resolve(parm.ParameterType))
                  .ToArray();

      // Execute the constructor method with the arguments resolved
      ctor.Invoke(page, args);
    }

    // Use the Autofac method to inject any
    // properties that can be filled by Autofac
    Container.InjectProperties(page);
  }
}
```

应用程序的页面（Default.aspx.cs 和 EditPage.aspx.cs）定义采用这些依赖项的构造函数。 请注意，默认构造函数仍存在，并且可以访问。 基础结构需要以下代码。

```cs
protected _Default() { }

public _Default(ICatalogService catalog) => this.catalog = catalog;
```

目录 API 是所有的异步方法。 Web 窗体现在支持所有数据控件的异步方法。 Catalog.WebForms 应用程序将模型绑定用于列表和编辑页面；页面上的控件定义用于指定任务返回异步操作的 SelectMethod、UpdateMethod、InsertMethod 和 DeleteMethod 属性。 Web 窗体控件知道绑定到控件的方法何时是异步方法。 使用异步选择方法时遇到的唯一限制是不能支持分页。 分页签名需要输出参数，而异步方法不能具有输出参数。 这一技术用于需要来自目录服务的数据的其他页面。

目录 Web 窗体应用程序的默认配置使用 catalog.api 服务的模拟实现。 此模拟使用其数据的硬编码数据集，通过在开发环境中删除 catalog.api 服务上的依赖项可以简化某些任务。

## <a name="lifting-and-shifting"></a>直接迁移

Visual Studio 为应用程序容器化提供很好的支持。 右键单击项目节点，然后选择“添加”和“Docker 支持”。 Docker 项目模板将一个新项目添加到名为“docker-compose”的解决方案。 项目包含编写（或生成）所需映像的 Docker 资产，并开始运行必要的容器，如图 7-3 所示。

在最简单的直接迁移方案中，应用程序将是用于 Web 窗体应用程序的单个服务。 模板还会更改启动项目，以指向 docker-compose 项目。 按 Ctrl+F5 或 F5 现可创建 Docker 映像并启动 Docker 容器。

![](./media/image3.png)

**图 7-3**。 Web 窗体解决方案中的 docker-compose 项目

在运行该解决方案之前，必须确保将 Docker 配置为使用 Windows 容器。 为此，请右键单击 Windows 中的 Docker 任务栏图标，并选择“切换到 Windows 容器”，如图 7-4 所示。

![](./media/image4.png)

**图 7-4**。 在 Windows 中从 Docker 任务栏图标切换到 Windows 容器

如果菜单项显示“切换到 Linux 容器”，则表示已在 Windows 容器中运行 Docker。

运行解决方案会重启 Docker 主机。 生成时，可以生成 Web 窗体项目的应用程序和 Docker 映像。 首次执行此操作时，需要相当长的时间。 这是因为生成过程会下拉 Windows Server 基础映像和 ASP.NET 的其他映像。 后续的生成和运行循环会快得多。

让我们深入了解一下 Docker 项目模板所添加的文件。 它为你创建了多个文件。 Visual Studio 使用这些文件创建 Docker 映像并启动容器。 可以使用 CLI 的相同文件手动运行 Docker 命令。

以下 Dockerfile 示例显示基于运行 ASP.NET 站点的 Windows ASP.NET 映像生成 Docker 映像时的基本设置。

```
FROM microsoft/aspnet

ARG source

WORKDIR /inetpub/wwwroot

COPY ${source:-obj/Docker/publish} .
```

此 Dockerfile 与创建用于在 Linux 容器中运行 ASP.NET Core 应用程序的 Dockerfile 非常相似。 但是，也有一些重要的区别。 最重要的区别是基础映像为 microsoft/aspnet，它是当前的 Windows Server 映像，包括 .NET Framework。 其他差异是从源目录复制的目录各不相同。

docker-compose 项目中的其他文件是生成和配置容器所需的 Docker 资产。 Visual Studio 将各种 docker-compose.yml 文件放在一个节点下，突出显示其使用方式。 基础 docker-compose 文件包含所有配置中常见的指令。 docker-compose.override.yml 文件包含环境变量和开发人员配置的相关替代。 .vs.debug 和 .vs.release 的变量提供的环境设置允许 Visual Studio 附加到正在运行的容器并管理容器。

Visual Studio 集成属于向解决方案添加 Docker 支持时，还可以从命令行使用 docker-compose up 命令生成并运行该集成，如之前几节所示。

## <a name="getting-data-from-the-existing-catalog-net-core-microservice"></a>从现有目录 .NET Core 微服务获取数据

可以将 Web 窗体应用程序配置为使用 eShopOnContainers 目录微服务获取数据，而非使用模拟数据。 为此，请编辑 web.config 文件，并将 useFake 键的值设置为“false”。 DI 容器会使用访问实时目录微服务的类，而不会使用返回硬编码数据的类。 无需更改任何其他代码。

访问实时目录服务意味着需要更新 docker-compose 项目才能生成目录服务映像并启动目录服务容器。 Docker CE for Windows 支持 Linux 容器和 Windows 容器，但不能同时支持。 若要运行目录微服务，需要生成在基于 Windows 的容器上运行目录微服务的映像。 这种方法需要与前面几节不同的微服务项目 Dockerfile。 Dockerfile.windows 文件包含生成目录 API 容器映像所需的配置设置，以便在 Windows 容器上运行，例如使用 Windows Nano Docker 映像。

目录微服务依赖于 SQL Server 数据库。 因此，还需要使用基于 Windows 的 SQL Server Docker 映像。

更改后，docker-compose 项目需要执行其他操作才能启动应用程序。 项目现在使用基于 Windows 的 SQL Server 映像启动 SQL Server。 它会在 Windows 容器中启动目录微服务。 它还会在 Windows 容器中启动 Web 窗体目录编辑器容器。 如果任何映像需要生成，首先应创建映像。

## <a name="development-and-production-environments"></a>开发和生产环境

在开发配置与生产配置之间有一些区别。 在开发环境中，作为同一 Docker 主机的一部分，在 Windows 容器中运行 Web 窗体应用程序、目录微服务和 SQL Server。 前面几节提到了在同一 Docker 主机上部署的 SQL Server 映像作为在基于 Linux 的 Docker 主机上的另一个基于 .NET Core的服务。 在同一 Docker 主机（或群集）上运行多个微服务的优点是网络通信更少，容器之间的通信具有较低的延迟。

在开发环境中，必须在相同的操作系统中运行所有的容器。 Docker CE for Windows 不支持同时运行基于 Windows 的容器和基于 Linux 的容器。 在生产环境中，可以决定是在单个 Docker 主机（或群集）的 Windows 容器中运行目录微服务，还是让 Web 窗体应用程序与在其他 Docker 主机的 Linux 容器中运行的目录微服务实例通信。 这取决于优化网络延迟所要采用的方法。 在大多数情况下，希望应用程序所依赖的微服务能在同一 Docker 主机（或 swarm）中运行，以便于部署并降低通信延迟。 在这些配置中，唯一花费较高的通信是微服务实例与永久性数据存储的高可用性服务器之间的通信。

>[!div class="step-by-step"]
[上一页] (../net-core-single-containers-linux-windows-server-hosts/index.md) [下一页] (../multi-container-microservice-net-applications/index.md)

