---
title: "表达式树摘要"
description: "总结如何使用表达式树创建将代码解释为数据并基于该代码生成新功能的动态程序。"
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: eb687ebd-1149-4453-9fc1-12a084495a66
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 8088ce0c138cdb05a6e4a4fb6467e43efd252ba7
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="expression-trees-summary"></a>表达式树摘要

[上一篇 - 翻译表达式](expression-trees-translating.md)

在此系列中，你已了解如何使用*表达式树*创建将代码解释为数据并基于该代码生成新功能的动态程序。

可以检查表达式树以了解算法的目的。 不仅可以检查该代码。 可以生成表示原始代码的修改版本的新表达式树。

还可以使用表达式树来查看算法，并将该算法翻译成另一种语言或环境。 

## <a name="limitations"></a>限制

存在一些不好翻译成表达式树的较新的 C# 语言元素。 表达式树不能包含 `await` 表达式或 `async` lambda 表达式。 C# 6 发行中添加的许多功能不会完全按照表达式树中所编写的那样显示。 较新的功能可能会显示在表达式树中等效、早期的语法中。 这可能不像你想象的那样有局限性。 实际上，这意味着在引入新语言功能时，解释表达式树的代码将仍可能照常运行。

即使具有这些限制，通过表达式树，仍可创建依赖于解释和修改表示为数据结构的代码的动态算法。 它是一种功能强大的工具，作为 .NET 生态系统的一种功能，它可使丰富的库（如实体框架）完成其所执行的操作。


