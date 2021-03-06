---
title: "委托简介"
description: "本概述主题介绍委托的基本概念，并讨论委托的语言设计目标。"
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 59b61d77-84e5-457b-8da5-fb5f24ca6ed6
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: dd4c68fb4f960d0c2d5cbdc9e699650070cacaf1
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="introduction-to-delegates"></a>委托简介

[上一篇](delegates-events.md)

在 .NET 中委托提供*后期绑定*机制。 后期绑定意味着调用方在你所创建的算法中至少提供一个方法来实现算法的一部分。

例如，在天文应用程序中对恒星列表进行排序。
你可以选择按照恒星与地球的距离、恒星的大小或者可以感知的亮度来对它们进行排序。

在所有这些情况下，Sort() 方法本质上执行的是同一操作：基于某种比较方法对列表中的项目进行排序。 对于每个排序顺序，比较两种恒星的代码是不同的。

这些类型的解决方案已在软件中使用了半个世纪。
C# 语言的委托概念提供一流的语言支持和以此概念为中心的类型安全性。

正如你稍后将在此系列文章中看到的，为与此类似的算法编写的 C# 代码是类型安全的，它利用语言和编译器来确保类型与参数匹配，并返回类型。

## <a name="language-design-goals-for-delegates"></a>委托的语言设计目标

语言设计人员针对最终成为委托的功能列举了一些目标。

团队想要拥有可用于任何后期绑定算法的公共语言构造。 这促使开发人员学习一个概念，并在许多不同的软件问题中使用这同一概念。

其次，团队想要支持单播和多播方法调用。 多播委托是将多种方法连在一起的委托。 稍后你可以在[本系列文章](delegate-class.md)中查看示例。 

团队想要委托在所有 C# 构造中支持开发人员所预期的相同的类型安全性。 

最后，团队认识到事件模式是一个特定模式，委托或任何后期绑定算法在其中非常有用。 团队想要确保委托的代码可以为 .NET 事件模式提供基础。

所有这些工作的结果是 C# 和 .NET 中的委托和事件支持。 本部分的剩余文章将介绍语言功能、库支持和使用委托时使用的通用语法结构。

你将了解 `delegate` 关键字和它所生成的代码。 你将了解 `System.Delegate` 类中的功能，以及如何使用这些功能。 你将了解如何创建类型安全的委托，以及如何创建可以通过委托调用的方法。 你还将了解如何使用 Lambda 表达式来处理委托和事件。 你将看到作为 LINQ 的构建基块的委托的用途。 你将了解委托如何成为 .NET 事件模式的基础，以及委托和事件之间的区别。

总之，你将看到委托如何成为 .NET 编程和使用框架 API 的重要组成部分。

让我们开始吧。

[下一篇](delegate-class.md)

