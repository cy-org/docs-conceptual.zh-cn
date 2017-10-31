---
title: Expression Trees
description: "介绍 .NET Core 中的表达式树，以及如何用它们将代码表示为可以检查、修改和执行的结构。"
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: aceb4719-0d5a-4b19-b01f-b51063bcc54f
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 3935906d9fca81a094999eefdd49ae4ed56990bf
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="expression-trees"></a>Expression Trees

如果你使用过 LINQ，则会有丰富库（其中 `Func` 类型是 API 集的一部分）的经验。 （如果尚不熟悉 LINQ，则可能需要阅读 [LINQ 教程](linq/index.md)以及在此之前的有关 [lambda 表达式](lambda-expressions.md)的教程。）表达式树提供与作为函数的参数的更丰富的交互。

在创建 LINQ 查询时，通常使用 Lambda 表达式编写函数参数。 在典型的 LINQ 查询中，这些函数参数会被转换为编译器创建的委托。 

当想要进行更丰富的交互时，需要使用*表达式树*。
表达式树将代码表示为可以检查、修改或执行的结构。 这些工具让你能够在运行时操作代码。 可以编写检查正在运行的算法的代码，或插入新的功能。 在更加高级的方案中，你可以修改正在运行的算法，甚至可以将 C# 表达式转换为另一种形式从而可在另一环境中执行。

你可能已经编写过使用表达式树的代码。 实体框架的 LINQ API 接受表达式树，以此作为 LINQ 查询表达式模式的参数。
这使得 [Entity Framework](http://docs.efproject.net/en/latest/)（实体框架）能够将使用 C# 编写的查询转换为在数据库引擎中执行的 SQL。 另一个示例是 [Moq](https://github.com/Moq/moq)，它是用于 .NET 的热门模拟框架。

本教程的其余部分将探索表达式树是什么、检查支持表达式树的框架类，并介绍如何使用表达式树。 你将学习如何阅读表达式树、如何创建表达式树、如何创建修改的表达式树，以及如何执行表达式树所表示的代码。 阅读后，便可以开始使用这些结构来创建丰富的自适应算法。

1. [已解释的表达式树](expression-trees-explained.md)

    了解表达式树的结构和概念。
    
2. [框架类型支持表达式树](expression-classes.md)
    
    了解定义和控制表达式树的结构和类。
    
3. [执行表达式](expression-trees-execution.md)

    了解如何将表示为 Lambda 表达式的表达式树转换为委托，并执行结果委托。

4. [解释表达式](expression-trees-interpreting.md)

    了解如何遍历并检查表达式树，以理解表达式树表示的代码。

5. [生成表达式](expression-trees-building.md)

    了解如何构造表达式树的节点并生成表达式树。

6. [转换表达式](expression-trees-translating.md)

    了解如何生成表达式树的修改副本，或将表达式树转换为另一种格式。

7. [总结](expression-trees-summary.md)

    查看表达式树上的信息。
    

