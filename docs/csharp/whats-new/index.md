---
title: "C# 中的新增功能 - C# 指南"
description: "C# 语言是如何不断发展的"
keywords: "C#, 最新功能, 新增功能, Roslyn"
author: BillWagner
ms.author: wiwagn
ms.date: 03/21/2017
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 77deec51-a14d-46d4-9bb3-faf449477149
ms.translationtype: HT
ms.sourcegitcommit: df0438dd742db802bb0f935d840006236d5d9bf9
ms.openlocfilehash: 0a328f62a02aea223340fcc00e839e841041a7d6
ms.contentlocale: zh-cn
ms.lasthandoff: 08/29/2017

---

# <a name="whats-new-in-c"></a>C# 中的新增功能 #

本页介绍了 C# 语言每个主要版本中新增功能的路线图。 若要详细了解每个版本中增加的主要功能，请单击下面的链接。

> [!IMPORTANT]
> 为了提供一些功能，C# 语言依赖标准库中的类型和方法。 例如，异常处理。 为了确保引发的对象派生自 @System.Exception，将会检查每个 `throw` 语句或表达式。 同样，还会检查每个 `catch`，以确保捕获的类型派生自 @System.Exception。 每个版本都可能会新增要求。 若要在旧版环境中使用最新语言功能，可能需要安装特定库。 每个特定版本的页面中记录了这些库。 若要了解此依赖项的背景信息，可以详细了解[语言与库的关系](relationships-between-language-and-library.md)。 

* [C# 7.1](csharp-7-1.md)：
    - 此页介绍了 C# 语言的最新功能。 这包括目前在 [Visual Studio 2017 版本 15.3](https://www.visualstudio.com/vs/whatsnew/) 和 [.NET Core 2.0 SDK](../../core/whats-new/index.md) 中可用的 C# 7.1 功能。

* [C# 7](csharp-7.md)：
    - 此页介绍 C# 7 中添加的功能。 [Visual Studio 2017](https://www.visualstudio.com/vs/whatsnew/) 和 [.NET Core 1.0](../../core/whats-new/index.md) 及更高版本中添加了这些功能
     
* [C# 6](csharp-6.md)：
    - 此页介绍 C# 6 中添加的功能。 这些功能可供 Windows 开发者在 Visual Studio 2015 中使用，并可供开发者在 macOS 和 Linux 上的 .NET Core 1.0 中探索 C# 时使用。

<!--* [C# Interactive](../interactive/index.md): 
    - This page describes C# Interactive, an interactive Read Eval Print Loop (REPL) that you can use to explore the C# language. You can use it to write code interactively and see it execute immediately, without any compile or build step.
-->
* [跨平台支持](../../core/index.md)：
    - 借助 .NET Core 支持，C# 可以在多个平台上运行。 如果希望在 macOS 或众多受支持的 Linux 发行版上使用 C#，请了解有关 .NET Core 的详细信息。

<!--
- [.NET Compiler Platform SDK](../roslyn/index.md):
    - The .NET Compiler Platform SDK enables you to write code that performs static analysis on C# code. You can use these APIs to find potential errors, or bad practices, suggest fixes, and even implement those fixes.
-->
  
## <a name="previous-versions"></a>早期版本
下面列出了在以前版本的 C# 语言和 Visual Studio.NET 中引入的主要功能。  
  
 * Visual Studio .NET 2013： 
     - 此版本的 Visual Studio 包含 .NET 编译器平台（“Roslyn”）的 Bug 修复、性能改进和技术预览，Roslyn 是 .NET 编译器平台 SDK 的前身<!--Link to ../roslyn/index.md-->。

 * C# 5，Visual Studio .NET 2012： 
     - `Async` / `await` 和[调用方信息](../programming-guide/concepts/caller-information.md)特性。

 * C# 4，Visual Studio .NET 2010： 
     - `Dynamic`、[命名自变量](../programming-guide/classes-and-structs/named-and-optional-arguments.md)、可选参数、泛型[协变和逆变](../programming-guide/concepts/covariance-contravariance/index.md)。

 * C# 3，Visual Studio .NET 2008： 
     - 对象和集合初始值设定项、lambda 表达式、扩展方法、匿名类型、自动属性、本地 `var` 类型推理和[语言集成查询 (LINQ)](../programming-guide/concepts/linq/index.md)。

 * C# 2，Visual Studio .NET 2005： 
     - 匿名方法、泛型、可以为 null 的类型、迭代器/yield、`static` 类、委托的协变和逆变。

 * C# 1.1，Visual Studio .NET 2003： 
     - `#line` 杂注和 xml 文档注释。

 * C# 1，Visual Studio .NET 2002： 
     - [C#](../csharp.md) 初版。   

