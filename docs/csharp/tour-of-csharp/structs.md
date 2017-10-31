---
title: "C# 结构 - C# 语言介绍"
description: "了解 C# 值类型（称为“结构”）的基础知识"
keywords: ".NET, C#, 结构, 值类型"
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 88a74571-f741-4a31-a2b5-1ccf165535b8
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 9d435fd87a6103d505c14219499eeea9aee045fb
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="structs"></a>结构

***结构***是可以包含数据成员和函数成员的数据结构，这一点与类一样；与类不同的是，结构是值类型，无需进行堆分配。 结构类型的变量直接存储结构数据，而类类型的变量存储对动态分配的对象的引用。 结构类型不支持用户指定的继承，并且所有结构类型均隐式继承自类型 <xref:System.ValueType>，后者又隐式继承自 `object`。

结构对包含值语义的小型数据结构特别有用。 复数、坐标系中的点或字典中的键值对都是结构的典型示例。 对小型数据结构使用结构（而不是类）在应用程序执行的内存分配次数上存在巨大差异。 例如，以下程序创建并初始化包含 100 个点的数组。 通过将 `Point` 实现为类，可单独实例化 101 个对象，一个对象用于数组，其他所有对象分别用于 100 个元素。

[!code-csharp[PointClassUse](../../../samples/snippets/csharp/tour/structs/Program.cs#L5-L13)]

也可以选择将 Point 实现为结构。

[!code-csharp[PointStruct](../../../samples/snippets/csharp/tour/structs/Point.cs#L3-L11)]

现在，仅实例化一个对象（即用于数组的对象），`Point` 实例存储内嵌在数组中。

结构构造函数使用 new 运算符进行调用，但这不并表示要分配内存。 结构构造函数只返回结构值本身（通常在堆栈的临时位置中），并在必要时复制此值，而非动态分配对象并返回对此对象的引用。

借助类，两个变量可以引用同一对象；因此，对一个变量执行的运算可能会影响另一个变量引用的对象。 借助结构，每个变量都有自己的数据副本；因此，对一个变量执行的运算不会影响另一个变量。 例如，以下代码片段生成的输出取决于 Point 是类还是结构。

[!code-csharp[PointUse](../../../samples/snippets/csharp/tour/structs/Program.cs#L19-L22)]

如果 `Point` 是类，则输出 20，因为 a 和 b 引用同一对象。 如果 Point 是结构，则输出 10，因为将 `a` 赋值给 `b` 创建了值副本，而此副本不受后面对 `a.x` 的赋值的影响。

以上示例突出显示了结构的两个限制。 首先，复制整个结构通常比复制对象引用效率更低，因此通过结构进行的赋值和值参数传递可能比通过引用类型成本更高。 其次，除 `ref` 和 `out` 参数以外，无法创建对结构的引用，这就表示在很多应用场景中都不能使用结构。

>[!div class="step-by-step"]
[上一页](classes-and-objects.md)
[下一页](arrays.md)

