---
title: "使用 DDD 和 CQRS 模式降低微服务中的业务复杂性"
description: "容器化 .NET 应用程序的 .NET 微服务体系结构 | 使用 DDD 和 CQRS 模式降低微服务中的业务复杂性"
keywords: "Docker, 微服务, ASP.NET, 容器"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.translationtype: HT
ms.sourcegitcommit: 9bb64ea7199f5699ff166d1affb7f8126dcc6612
ms.openlocfilehash: d81091bf09d690f5d57ad9a30b5f16de1358ede6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/05/2017

---
# <a name="tackling-business-complexity-in-a-microservice-with-ddd-and-cqrs-patterns"></a>使用 DDD 和 CQRS 模式降低微服务中的业务复杂性

为每个微服务或反映对业务域理解的绑定上下文设计域模型。

本节重点介绍在需要降低子系统复杂性时实现的更高级的微服务，或按不断变化的业务规则派生自域专家知识的微服务。 本节中使用的体系结构模式基于域驱动的设计 (DDD) 以及命令和查询责任分离 (CQRS) 方法，如图 9-1 中所示。

![](./media/image1.png)

**图 9-1**。 外部微服务体系结构与每个微服务的内部体系结构模式

但是，大部分用于数据驱动微服务的技术（例如如何实现 ASP.NET Core Web API 服务或如何公开具有 Swashbuckle 的 Swagger 元数据）同样适用于使用 DDD 模式在内部实现的更高级的微服务。 本节是前几节内容的扩展，因为之前所述的大部分做法也适用于此处或任何类型的微服务。

本节首先提供有关用于 eShopOnContainers 引用应用程序的简化 CQRS 模式的详细信息。 之后，将概述 DDD 技术，使你能够找到可在应用程序中重用的常见模式。

DDD 是一个大主题，具有一套丰富的学习资源。 开始时可以阅读 Eric Evans 撰写的[《域驱动设计》](https://domainlanguage.com/ddd/)等此类书籍，以及 Vaughn Vernon、Jimmy Nilsson、Greg Young、Udi Dahan、Jimmy Bogard 和许多其他 DDD/CQRS 专家撰写的其他资料。 但最重要的是需要尝试了解如何与具体业务域中的专家配合，从对话、白板和域建模会话应用 DDD 技术。

#### <a name="additional-resources"></a>其他资源

##### <a name="ddd-domain-driven-design"></a>DDD（域驱动设计）

-   **Eric Evans。Domain Language**
    [*http://domainlanguage.com/*](http://domainlanguage.com/)（域语言）

-   **Martin Fowler。Domain-Driven Design**
    [*http://martinfowler.com/tags/domain%20driven%20design.html*](http://martinfowler.com/tags/domain%20driven%20design.html)（域驱动设计）

-   **Jimmy Bogard。Strengthening your domain: a primer**
    [*https://lostechies.com/jimmybogard/2010/02/04/strengthening-your-domain-a-primer/*](https://lostechies.com/jimmybogard/2010/02/04/strengthening-your-domain-a-primer/)（增强域：初级）

##### <a name="ddd-books"></a>DDD 丛书

-   **Eric Evans。《域驱动设计：软件核心复杂性应对之道》**
    [*https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/*](https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215/)

-   **Eric Evans。《Domain-Driven Design Reference: Definitions and Pattern Summaries》**
    [*https://www.amazon.com/Domain-Driven-Design-Reference-Definitions-2014-09-22/dp/B01N8YB4ZO/*](https://www.amazon.com/Domain-Driven-Design-Reference-Definitions-2014-09-22/dp/B01N8YB4ZO/)（域驱动设计参考：定义和模式摘要）

-   **Vaughn Vernon。《实现领域驱动设计》**
    [*https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577/*](https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577/)

-   **Vaughn Vernon。《Domain-Driven Design Distilled》**
    [*https://www.amazon.com/Domain-Driven-Design-Distilled-Vaughn-Vernon/dp/0134434420/*](https://www.amazon.com/Domain-Driven-Design-Distilled-Vaughn-Vernon/dp/0134434420/)（域驱动设计精选）

-   **Jimmy Nilsson。《Applying Domain-Driven Design and Patterns》**
    [*https://www.amazon.com/Applying-Domain-Driven-Design-Patterns-Examples/dp/0321268202/*](https://www.amazon.com/Applying-Domain-Driven-Design-Patterns-Examples/dp/0321268202/)（应用域驱动的设计和模式）

-   **Cesar de la Torre。《N-Layered Domain-Oriented Architecture Guide with .NET》**
    [*https://www.amazon.com/N-Layered-Domain-Oriented-Architecture-Guide-NET/dp/8493903612/*](https://www.amazon.com/N-Layered-Domain-Oriented-Architecture-Guide-NET/dp/8493903612/)（.NET 中面向域的 N 层体系结构指南）

-   **Abel Avram 与 Floyd Marinescu。《Domain-Driven Design Quickly》**
    [*https://www.amazon.com/Domain-Driven-Design-Quickly-Abel-Avram/dp/1411609255/*](https://www.amazon.com/Domain-Driven-Design-Quickly-Abel-Avram/dp/1411609255/)（域驱动的快速设计）

DDD 培训

-   **Julie Lerman 与 Steve Smith。域驱动设计基础知识**
    [*http://bit.ly/PS-DDD*](http://bit.ly/PS-DDD)


>[!div class="step-by-step"]
[上一页] (../multi-container-microservice-net-applications/test-aspnet-core-services-web-apps.md) [下一页] (apply-simplified-microservice-cqrs-ddd-patterns.md)

