---
title: "实现具有恢复能力的应用程序"
description: "适用于容器化 .NET 应用程序的 .NET 微服务体系结构 | 实现具有恢复能力的应用程序"
keywords: "Docker, 微服务, ASP.NET, 容器"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.translationtype: HT
ms.sourcegitcommit: 9bb64ea7199f5699ff166d1affb7f8126dcc6612
ms.openlocfilehash: a1041938891219fd2e3b17d004bb40b544b8ceaa
ms.contentlocale: zh-cn
ms.lasthandoff: 09/05/2017

---
# <a name="implementing-resilient-applications"></a>实现具有恢复能力的应用程序

基于微服务和云的应用程序必须包容最终必然会发生的部分故障。需要设计应用程序，使其可从这些部分故障中恢复。

恢复能力是指从故障中恢复并继续工作的能力。 这并不是指避免故障，而是接受会发生故障这一事实，并以能够避免停机或数据丢失的方式对故障做出响应。 恢复的目标是使应用程序在发生故障后回到完全正常运行的状态。

设计和部署基于微服务的应用程序已经非常具有挑战性。 然而还需要让应用程序在必然发生某种故障的环境中保持正常运行。 因此，应用程序应具有恢复能力。 应将其设计为能够处理部分故障，如网络中断或者云中节点或 VM 故障。 甚至将微服务（容器）移动到群集内的另一个节点，也可能导致应用程序出现间歇性的功能短缺故障。

应用程序的各个组件还应涵盖运行状况监视功能。 遵循本章节中的准则，可创建这样的应用程序：即使在基于云的复杂部署中出现短暂停机或暂时中断，它也能平稳运行。


>[!div class="step-by-step"]
[上一页] (../microservice-ddd-cqrs-patterns/microservice-application-layer-implementation-web-api.md) [下一页] (handle-partial-failure.md)

