---
title: ".NET Core 中的单元测试"
description: "单元测试从未如此简单。 了解如何在 .NET Core 和 .NET Standard 项目中使用单元测试。"
keywords: ".NET, .NET Core, .NET Standard, 单元测试"
author: ardalis
ms.author: wiwagn
ms.date: 08/30/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 815ac74c-4bd9-4a94-a87c-78288b27c0e2
ms.translationtype: HT
ms.sourcegitcommit: b041fbec3ff22157d00af2447e76a7ce242007fc
ms.openlocfilehash: 9f6a70598f3a0c0e3f479a25171e1deb6abffa33
ms.contentlocale: zh-cn
ms.lasthandoff: 09/14/2017

---

# <a name="unit-testing-in-net-core-and-net-standard"></a>.NET Core 和 .NET Standard 中的单元测试

由于在设计 .NET Core 时考虑到了可测试性，因此为应用程序创建单元测试比以往更加简单。 本文简要介绍了单元测试（以及与其他类型测试的不同之处）。 链接的资源展示了如何将测试项目添加到解决方案中，再使用命令行或 Visual Studio 运行单元测试。

.NET Core 2.0 支持 [.NET Standard 2.0](../../standard/net-standard.md)。 本部分中用于演示单元测试的库依赖 .NET Standard，同时也适用于其他项目类型。

自 .NET Core 2.0 起，提供适用于 Visual Basic、F# 和 C# 的单元测试项目模板。

## <a name="getting-started-with-testing"></a>测试入门

确保软件应用程序按作者的期望执行操作，其中最好的一种方法是拥有自动化测试套件。 可以对软件应用程序进行各种不同的测试，包括集成测试、Web 测试、负载测试等。 测试各个软件组件或方法的单元测试是最低级测试。 单元测试只应测试开发人员控件中的代码，而不应测试基础结构问题，如数据库、文件系统或网络资源等。 可以使用[测试驱动开发 (TDD)](http://deviq.com/test-driven-development/) 编写单元测试，或将其添加到现有代码以确认其正确性。 无论属于上述哪种情况，单元测试都应该是命名恰当且运行速度快的小型测试，因为理想情况下，都希望能够先运行数百个单元测试，再将更改推送到项目的共享代码存储库中。

> [!NOTE]
> 开发人员经常要想方设法地为测试类和方法提供合适的名称。 作为起点，ASP.NET 产品团队会遵循[这些约定](https://github.com/aspnet/Home/wiki/Engineering-guidelines#unit-tests-and-functional-tests)。

编写单元测试时，注意不要在基础结构上意外引入了依赖项。 这些依赖项往往会降低测试速度，使测试更加脆弱，因此应将其保留供集成测试使用。 可以通过遵循 [Explicit Dependencies Principle](http://deviq.com/explicit-dependencies-principle/)（显示依赖项原则）和使用 [Dependency Injection](/aspnet/core/fundamentals/dependency-injection)（依赖项注入）从框架中请求依赖项，以此避免应用程序代码中的这些隐藏依赖项。 还可以将单元测试保留在单独的项目中，与集成测试相分隔，并确保单元测试项目没有引用或依赖于基础结构包。

了解有关 .NET Core 项目中的单元测试的详细信息：

支持对 .NET Core 单元测试项目使用 [C#](../../csharp/index.md)、[F#](../../fsharp/index.md) 和 [Visual Basic](../../visual-basic/index.md)。 还可以在 [xUnit](http://xunit.github.io) 与 [MSTest](https://github.com/Microsoft/vstest-docs) 之间进行选择。

下面的演练介绍了这些组合使用方式：

* [结合使用 .NET Core CLI 与 XUnit 和 C#](unit-testing-with-dotnet-test.md) 创建单元测试。
* [结合使用 .NET Core CLI 与 MSTest 和 C#](unit-testing-with-mstest.md) 创建单元测试。
* [结合使用 .NET Core CLI 与 XUnit 和 F#](unit-testing-fsharp-with-dotnet-test.md) 创建单元测试。
* [结合使用 .NET Core CLI 与 MSTest 和 F#](unit-testing-fsharp-with-mstest.md) 创建单元测试。
* [结合使用 .NET Core CLI 与 XUnit 和 Visual Basic](unit-testing-visual-basic-with-dotnet-test.md) 创建单元测试。
* [结合使用 .NET Core CLI 与 MSTest 和 Visual Basic](unit-testing-visual-basic-with-mstest.md) 创建单元测试。

可以选择不同的语言用于类库和单元测试库。 通过混合搭配参考上面引用的演练，可以了解具体操作方法。

* 如果使用的是 Visual Studio，只需参阅 [.NET Core 中的 Live Unit Testing](/visualstudio/test/live-unit-testing)
* 有关如何使用选择性单元测试筛选的其他信息和示例，请参阅[运行选择性单元测试](selective-unit-tests.md)或[使用 Visual Studio 添加和排除测试](/visualstudio/test/live-unit-testing#including-and-excluding-test-projects-and-test-methods)。
* XUnit 团队编写了一个教程，介绍[如何通过 .NET Core 和 Visual Studio 使用 xUnit](http://xunit.github.io/docs/getting-started-dotnet-core.html)。

