---
title: ".NET 教程 | Microsoft Docs"
description: ".NET 的一些重要功能指导教程。"
keywords: ".NET, .NET Core, 教程, 编程语言, 不安全, 内存管理, 类型安全, 异步"
author: cartermp
ms.author: wiwagn
ms.date: 05/22/2017
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: bbfe6465-329d-4982-869d-472e7ef85d93
ms.translationtype: HT
ms.sourcegitcommit: 2762cdc983465979a530192716c33de7044dd1ed
ms.openlocfilehash: c64a3113cf4e9e9ff203ed2cf449359f67ee9d10
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---

# <a name="tour-of-net"></a>.NET 教程

.NET 是一个通用开发平台。 它具有几项关键功能，例如支持多种编程语言、异步和并发编程模型以及本机互操作性，可以支持跨多个平台的各种方案。

本文还提供了 .NET 的一些关键功能的指导教程。 请参阅 [.NET 体系结构组件](components.md)主题，了解 .NET 的各体系结构部分及其用途。

## <a name="how-to-run-the-code-samples"></a>如何运行代码示例

要了解如何设置开发环境以运行代码示例，请参阅[入门](get-started.md)主题。 将代码示例从此页复制并粘贴到你的环境中以执行它们。 

## <a name="programming-languages"></a>编程语言

.NET 支持多种编程语言。 .NET 实现可实现[公共语言基础结构 (CLI)](https://www.visualstudio.com/license-terms/ecma-c-common-language-infrastructure-standards/)，除其他事项外，它指定与语言无关的运行时和语言互操作性。 这意味着可选择任意 .NET 语言在 .NET 上生成应用和服务。

Microsoft 积极开发和支持三种 .NET 语言：C#、F# 和 Visual Basic (VB)。 

* C# 是一种简单、强大、类型安全、面向对象的语言，同时保留了 C 语言的表达力度和简洁性。 熟悉 C 和类似语言的任何人在适应 C# 的过程中几乎不会遇到什么问题。 请查看 [C# 指南](../csharp/index.md)，了解有关 C# 的详细信息。

* F# 是一种跨平台、功能优先的编程语言，它也支持传统的面向对象的编程和命令式编程。 请查看 [F# 指南](../fsharp/index.md)，了解有关 F# 的详细信息。

* Visual Basic 是一种简单易学的语言，用于生成在 .NET 上运行的各种应用。 在 .NET 语言中，VB 的语法最接近于人类的普通用语，通常使软件开发新手更容易上手。

## <a name="automatic-memory-management"></a>自动内存管理

.NET 使用[垃圾回收 (GC)](garbagecollection/index.md) 为程序提供自动内存管理。 GC 以一种“懒散”的方式进行内存管理，它优先考虑应用吞吐量，而不是立即回收内存。 要了解有关 .NET GC 的详细信息，请查看[垃圾回收 (GC) 的基础](garbagecollection/fundamentals.md)。

以下两行代码都会分配内存：

[!code-csharp[MemoryManagement](../../samples/csharp/snippets/tour/MemoryManagement.csx#L1-L2)]

无法使用任何类似的关键字来取消分配内存，因为当垃圾回收器通过其计划的运行规则回收内存时，会自动取消分配。

垃圾回收站是一种帮助确保内存安全的服务。 如果某个程序仅访问分配的内存，则该程序就是内存安全的。 例如，运行时可确保应用不会访问超过数组边界的未分配内存。

下例中，运行时引发 `InvalidIndexException` 异常，强制实现内存安全：

[!code-csharp[MemoryManagement](../../samples/csharp/snippets/tour/MemoryManagement.csx#L4-L5)]

## <a name="working-with-unmanaged-resources"></a>处理未托管的资源

部分对象会引用*未托管的资源*。 未托管的资源是指不由 .NET 运行时自动维护的资源。 例如，文件句柄就是未托管的资源。 <xref:System.IO.FileStream> 对象是一个托管对象，但它引用未托管的文件句柄。 用完 <xref:System.IO.FileStream> 之后，需要释放文件句柄。

在 .NET 中，引用未托管资源的对象会实现 <xref:System.IDisposable> 接口。 用完对象后，需调用此对象的 <xref:System.IDisposable.Dispose> 方法，该方法会释放所有托管资源。 .NET 语言为此类对象提供了一种便捷的 `using` 语法，如下例所示：

[!code-csharp[UnmanagedResources](../../samples/csharp/snippets/tour/UnmanagedResources.csx#L1-L6)]

`using` 块完成后，.NET 运行时会自动调用 `stream` 对象的 <xref:System.IDisposable.Dispose> 方法，该方法会释放文件句柄。 如果某异常造成控件退出块，则运行时也会执行此操作。

有关更多详细信息，请参阅下列主题：

* 对于 C#，请参阅 [using 语句（C# 参考）](../csharp/language-reference/keywords/using-statement.md)主题。
* 对于 F#，请参阅[资源管理：use 关键字](../fsharp/language-reference/resource-management-the-use-keyword.md)。
* 对于 VB，请参阅 [Using 语句 (Visual Basic)](../visual-basic/language-reference/statements/using-statement.md) 主题。

## <a name="type-safety"></a>类型安全

对象是特定类型的实例。 给定对象允许的唯一操作属于特定的类型。 `Dog` 类型可能具有 `Jump` 和 `WagTail` 方法，但没有 `SumTotal` 方法。 程序只调用属于给定类型的方法。 所有其他调用会导致编译时错误或运行时异常（如果使用动态功能或 `object`）。

.NET 语言面向对象，包含基类和派生类的层次结构。 .NET 运行时仅允许与对象层次结构相符的对象强制转换和调用。 请记住，任何 .NET 语言中定义的每个类型都派生自 <xref:System.Object> 基类型。

[!code-csharp[TypeSafety](../../samples/csharp/snippets/tour/TypeSafety.csx#L19-L23)]

使用类型安全还有助于强制实施封装，因为它可以保证访问器关键字的保真度。 访问器关键字是控制其他代码访问给定类型的成员的项目。 这些关键字通常用于某个类型中用来管理类型行为的各种数据。

[!code-csharp[TypeSafety](../../samples/csharp/snippets/tour/TypeSafety.csx#L3-L3)]

C#、VB 和 F# 支持本地类型推理。 类型推理是指编译器根据右侧的表达式推断左侧表达式的类型。 这并不意味着类型安全遭到破坏或规避。 生成的类型具有一个隐含所有信息的强类型。 在上例中，重写了 `dog` 和 `cat` 以介绍类型推理，示例的其余部分保持不变：

[!code-csharp[TypeSafety](../../samples/csharp/snippets/tour/TypeSafety.csx#L28-L34)]

与在 C# 和 VB 中找到的方法本地类型推理相比，F# 的类型推理能力更强。 若要了解详细信息，请参阅[类型推理](../fsharp/language-reference/type-inference.md)。

## <a name="delegates-and-lambdas"></a>委托和 lambda

委托用方法签名表示。 可将任何使用该签名的方法分配给该委托，调用该委托时会执行这些方法。

委托类似于 C++ 函数指针，只是它们是类型安全的。 它们是 CLR 类型系统中某种断开连接的方法。 正则方法已连接到某个类，只能通过静态或实例调用约定来直接调用。

在 .NET 中，委托通常用于事件处理程序、定义异步操作以及 lambda 表达式，它们是 LINQ 的基础。 有关详细信息，请参见[委托和 lambda](delegates-lambdas.md) 主题。

## <a name="generics"></a>泛型

泛型可让程序员在设计类时引入一个“类型参数”，这样，客户端代码（类型的用户）便可指定要使用哪个确切的类型来取代类型参数。

添加泛型的目的是帮助程序员实现通用数据结构。 在泛型问世之前，要将 `List` 等类型用作泛型，必须处理 `object` 类型的元素。 这会造成各种性能和语义问题，甚至造成微妙的运行时错误。 例如，当数据结构包含整数和字符串时，如果在处理列表的成员时引发 `InvalidCastException`，则就会出现运行时错误这种非常棘手的问题。

以下示例显示了使用 <xref:System.Collections.Generic.List%601> 类型实例运行的基本程序：

[!code-csharp[GenericsShort](../../samples/csharp/snippets/tour/GenericsShort.csx)]

有关详细信息，请参阅[泛型类型（泛型）概述](generics.md)主题。

## <a name="async-programming"></a>异步编程

异步编程是 .NET 中的一个先进概念，它在运行时、框架库和 .NET 语言构造中提供异步支持。 在内部，异步编程基于利用操作系统尽可能高效地执行 I/O 绑定型作业的对象（例如 `Task`）。

若要了解有关 .NET 中异步编程的详细信息，请先阅读[异步概述](async.md)主题。

## <a name="language-integrated-query-linq"></a>语言集成查询 (LINQ)

LINQ 是适用于 C# 和 VB 的强大功能集，可用于编写简单的声明性代码来处理数据。 数据可采用多种形式（例如，内存中对象、SQL 数据库或 XML 文档），但针对每个数据源编写的 LINQ 代码往往没有差别。

若要了解详细信息并查看某部分示例，请参阅 [LINQ（语言集成查询）](using-linq.md)主题。

## <a name="native-interoperability"></a>本机互操作性

每个操作系统都有一个应用程序编程接口 (API)，用于提供系统服务。 .NET 提供多种方式来调用这些 API。

实现本机互操作性的主要方式是通过“平台调用”（简称 P/Invoke），Linux 和 Windows 平台均支持这种方式。 实现本机互操作性的另一种方式称为“COM 互操作”（仅限 Windows），用于在托管代码中操作 [COM 组件](https://msdn.microsoft.com/library/bwa2bx93.aspx)。 这种方式建立在 P/Invoke 基础结构之上，但工作原理略有不同。

针对 Java 和 Objective-C 的 Mono（以及 Xamarin）互操作性支持基本上以类似的方式构建，也就是说，它们运用相同的原理。

有关本机互操作性的的详细信息，请参阅[本机互操作性](native-interop.md)主题。

## <a name="unsafe-code"></a>不安全代码

根据语言支持，CLR 可通过 `unsafe` 代码访问本机内存和执行指针算术运算。 某些算法和系统互操作性需要这些操作。 尽管不安全代码的功能强大，但除非有必要与系统 API 互操作或实现最高效的算法，否则不建议使用。 在不同的环境中，不安全代码的执行方式可能不同，使用它还会丧失垃圾回收器和类型安全带来的好处。 建议尽可能地限制和集中化使用不安全代码，并全面测试该代码。

以下示例是 `StringBuilder` 类中 `ToString()` 方法的修改版本。 它演示了如何使用 `unsafe` 代码直接移动内存区块，从而有效实现某种算法：

[!code-csharp[Unsafe](../../samples/csharp/snippets/tour/Unsafe.csx)]

## <a name="next-steps"></a>后续步骤

如果对 C# 功能的教程感兴趣，请参阅 [C# 教程](../csharp/tour-of-csharp/index.md)。

如果对 F# 功能的教程感兴趣，请参阅 [F# 教程](../fsharp/tour.md)。

如果想开始自己编写代码，请访问[入门](get-started.md)。

要了解 .NET 的重要组件，请参阅 [.NET 体系结构组件](components.md)。

