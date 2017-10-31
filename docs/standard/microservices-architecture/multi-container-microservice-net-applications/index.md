---
title: "设计和开发基于微服务的多容器 .NET 应用程序"
description: "容器化 .NET 应用程序的 .NET 微服务体系结构 | 设计和开发基于微服务的多容器 .NET 应用程序"
keywords: "Docker, 微服务, ASP.NET, 容器"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.translationtype: HT
ms.sourcegitcommit: 9bb64ea7199f5699ff166d1affb7f8126dcc6612
ms.openlocfilehash: 8651254f4550a1a5c6a776ebd2524b5bfe20c546
ms.contentlocale: zh-cn
ms.lasthandoff: 09/05/2017

---
# <a name="designing-and-developing-multi-container-and-microservice-based-net-applications"></a>设计和开发基于微服务的多容器 .NET 应用程序

开发容器化微服务应用程序意味着将生成多容器应用程序。但是，多容器应用程序也可以更简单（例如一个三层应用程序），并可能不是使用微服务体系结构生成的。

之前我们提出了“生成微服务体系结构时 Docker 是否是必需的？”这一问题 很显然，答案是否定。 Docker 是推动器，可以提供很多优势，但容器和 Docker 不属于微服务的硬性要求。 例如，使用 Azure Service Fabric 时，它支持将微服务作为简单的流程或 Docker 容器运行，所以使用或不使用 Docker 都可以创建基于微服务的应用程序。

但是，如果知道如何设计和开发基于微服务，同时基于 Docker 容器的应用程序，将能够设计和开发任何其他更简单的应用程序模型。 例如，可以设计还需要多容器方法的三层应用程序。 鉴于此，另外还因为微服务体系结构是容器领域的重要趋势，本节会重点介绍如何使用 Docker 容器实现微服务体系结构。


>[!div class="step-by-step"]
[上一页] (../containerize-net-framework-applications/index.md) [下一页] (microservice-application-design.md)

