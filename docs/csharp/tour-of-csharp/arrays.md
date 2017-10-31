---
title: "C# 数组 - C# 语言介绍"
description: "数组是 C# 语言中最基本的集合类型"
keywords: ".NET, C#, 数组, 集合"
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: a440704c-9e88-4c75-97dd-bfe30ca0fb97
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 82362a3675c431423a99d3d728fb8dd1da58c9c7
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="arrays"></a>数组

***数组***是一种数据结构，其中包含许多通过计算索引访问的变量。 数组中的变量（亦称为数组的***元素***）均为同一种类型，我们将这种类型称为数组的***元素类型***。

数组类型是引用类型，声明数组变量只是为引用数组实例预留空间。 实际的数组实例是在运行时使用 new 运算符动态创建而成。 new 运算指定了新数组实例的***长度***，然后在此实例的生存期内固定使用这个长度。 数组元素的索引介于 `0` 到 `Length - 1` 之间。 `new` 运算符自动将数组元素初始化为其默认值（例如，所有数值类型的默认值为 0，所有引用类型的默认值为 `null`）。

以下示例创建 `int` 元素数组，初始化此数组，然后打印输出此数组的内容。

[!code-csharp[ArraySample](../../../samples/snippets/csharp/tour/arrays/Program.cs#L3-L18)]

上面的示例创建***一维数组***，并对其执行运算。 C# 还支持***多维数组***。 数组类型的维数（亦称为数组类型的***秩***）是 1 与数组类型方括号内的逗号数量相加的结果。 以下示例分别分配一维、二维、三维数组。

[!code-csharp[ArrayRank](../../../samples/snippets/csharp/tour/arrays/Program.cs#L24-L26)]

`a1` 数组包含 10 个元素，`a2` 数组包含 50 个元素 (10 × 5)，`a3` 数组包含 100 个元素 (10 × 5 × 2)。
数组的元素类型可以是任意类型（包括数组类型）。 包含数组类型元素的数组有时称为***交错数组***，因为元素数组的长度不必全都一样。 以下示例分配由 `int` 数组构成的数组：

[!code-csharp[ArrayAllocation](../../../samples/snippets/csharp/tour/arrays/Program.cs#L31-L34)]

第一行创建包含三个元素的数组，每个元素都是 `int[]` 类型，并且初始值均为 `null`。 后面的代码行将这三个元素初始化为引用长度不同的各个数组实例。

通过 new 运算符，可以使用***数组初始值设定项***（在分隔符 `{` 和 `}` 内编写的表达式列表）指定数组元素的初始值。 以下示例分配 `int[]`，并将其初始化为包含三个元素。

[!code-csharp[ArrayInitialization](../../../samples/snippets/csharp/tour/arrays/Program.cs#L39-L39)]

请注意，可从 { 和 } 内的表达式数量推断出数组的长度。 局部变量和字段声明可以进一步缩短，这样就不用重新声明数组类型了。

[!code-csharp[ArrayInitialization](../../../samples/snippets/csharp/tour/arrays/Program.cs#L44-L44)]

以上两个示例等同于以下示例：

[!code-csharp[ArrayAssignment](../../../samples/snippets/csharp/tour/arrays/Program.cs#L49-L53)]

>[!div class="step-by-step"]
[上一页](structs.md)
[下一页](interfaces.md)

