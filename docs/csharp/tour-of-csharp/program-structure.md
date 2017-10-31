---
title: "C# 程序结构 - C# 语言介绍"
description: "了解 C# 程序的基本构建基块"
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 984f0314-507f-47a0-af56-9011243f5e65
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 8d8f443f8458cd392c75e9787e612ca1cc3518c7
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="program-structure"></a>程序结构

C# 中的关键组织结构概念包括***程序***、***命名空间***、***类型***、***成员***和***程序集***。 C# 程序由一个或多个源文件组成。 程序声明类型，而类型则包含成员，并被整理到命名空间中。 类型示例包括类和接口。 成员示例包括字段、方法、属性和事件。 编译完的 C# 程序实际上会打包到程序集中。 程序集的文件扩展名通常为 `.exe` 或 `.dll`，具体取决于实现的是***应用程序***还是***库***。

以下示例在 `Acme.Collections` 命名空间中声明 `Stack` 类：

[!code-csharp[Stack](../../../samples/snippets/csharp/tour/program-structure/program.cs#L1-L34)]

此类的完全限定的名称为 `Acme.Collections.Stack`。 此类包含多个成员：一个 `top` 字段、两个方法（`Push` 和 `Pop`）和一个 `Entry` 嵌套类。 `Entry` 类还包含三个成员：一个 `next` 字段、一个 `data` 字段和一个构造函数。 假定示例的源代码存储在 `acme.cs` 文件中，以下命令行

```
csc /t:library acme.cs
```

将示例编译成库（不含 `Main` 入口点的代码），并生成 `acme.dll` 程序集。

> [!IMPORTANT]
> 上述示例使用 `csc` 作为命令行 C# 编译器。 此编译器是 Windows 可执行文件。 若要在其他平台上使用 C#，应使用 .NET Core 工具。 .NET Core 生态系统使用 `dotnet` CLI 来管理命令行生成。 这包括管理依赖项和调用 C# 编译器。 有关在 .NET Core 支持的平台上使用这些工具的完整说明，请参阅[这篇教程](../../core/tutorials/using-with-xplat-cli.md)。

程序集包含中间语言 (IL) 指令形式的可执行代码和元数据形式的符号信息。 执行前，程序集中的 IL 代码会被 .NET 公共语言运行时的实时 (JIT) 编译器自动转换成处理器专属代码。

由于程序集是包含代码和元数据的自描述功能单元，因此无需在 C# 中使用 `#include` 指令和头文件。 只需在编译程序时引用特定的程序集，即可在 C# 程序中使用此程序集中包含的公共类型和成员。 例如，此程序使用 `acme.dll` 程序集中的 `Acme.Collections.Stack` 类：

[!code-csharp[UsingStack](../../../samples/snippets/csharp/tour/program-structure/Program.cs#L38-L52)]

如果程序存储在文件 `example.cs` 中，那么在 `example.cs` 编译完后，可以使用编译器的 /r 选项引用 acme.dll 程序集：

```
csc /r:acme.dll example.cs
```

这会创建 `example.exe` 可执行程序集，它将在运行时输出以下内容：

```
100
10
1
```

使用 C#，可以将程序的源文本存储在多个源文件中。 编译多文件 C# 程序时，可以将所有源文件一起处理，并且源文件可以随意相互引用。从概念上讲，就像是所有源文件在处理前被集中到一个大文件中一样。 在 C# 中，永远都不需要使用前向声明，因为声明顺序无关紧要（除了极少数的例外情况）。 C# 并不限制源文件只能声明一种公共类型，也不要求源文件的文件名必须与其中声明的类型相匹配。

>[!div class="step-by-step"]
[上一页](index.md)
[下一页](types-and-variables.md)

