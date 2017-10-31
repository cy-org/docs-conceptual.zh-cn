---
title: "异步概述"
description: "了解异步编程为何是一项能够简单处理多个核心上的阻塞 I/O 和并发操作的关键技术。"
keywords: .NET, .NET Core
author: cartermp
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 1e38e9d9-8284-46ee-a15f-199adc4f26f4
ms.translationtype: HT
ms.sourcegitcommit: ef6d1bf9a7153f7adf635d13b4dcfb7647ed2e33
ms.openlocfilehash: bf0cc4ed21c92a57f3f5b2cfa27ac1f054e15172
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---

# <a name="async-overview"></a>异步概述

不久前，人们通过购买更新的电脑和服务器来加快应用的速度，但是这种趋势已经停止了。 事实上，趋势逆转了。 手机配备 1ghz 单核 ARM 芯片，而服务器工作负荷转向 VM。 用户仍青睐响应式 UI，企业所有者则希望拥有能随着其业务缩放的服务器。 向手机和云的转变以及超过 30 亿使用 Internet 的人口引领着新软件模式的形成。 

* 有了高应用存储率，客户端应用有望保持始终开启，始终连接的状态，并且可持续响应用户交互（例如，触摸）！
* 用户期望服务能够通过平稳地扩展和收缩来应对流量高峰。 

异步编程是一项关键技术，使得能够简单处理多个核心上的阻塞 I/O 和并发操作。 通过 C#、VB 和 F## 中易于使用的语言级异步编程模型，.NET 可为应用和服务提供使其变得可响应且富有弹性。

## <a name="why-write-async-code"></a>为什么要编写异步代码？

新型应用广泛使用文件和网络 I/O。 默认情况下 I/O API 一般会阻塞，导致糟糕的用户体验和硬件利用率，除非希望学习和使用富有挑战的模式。 基于任务的异步 API 和语言级异步编程模型改变了这种模型，只需了解几个新概念就可默认进行异步执行。

异步代码具有以下特点：

* 等待 I/O 请求返回的同时，可通过生成处理更多请求的线程，处理更多的服务器请求。
* 等待 I/O 请求的同时生成 UI 交互线程，并通过将长时间运行的工作转换到其他 CPU 核心，让 UI 的响应速度更快。
* 许多较新的 .NET APIs 都是异步的。
* 在 .NET 中编写异步代码很简单！

## <a name="whats-next"></a>后续步骤

若要深入了解异步概念和编程，请参阅[深入了解异步](async-in-depth.md)和[基于任务的异步编程](~/docs/standard/parallel-programming/task-based-asynchronous-programming.md)。

