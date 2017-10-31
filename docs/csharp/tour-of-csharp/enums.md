---
title: "C# 枚举 - C# 语言介绍"
description: "了解 C# 中的枚举，即离散的已命名常量"
keywords: .NET, C#
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 7faba1cc-6ea9-4a19-adb9-0335e4b132e5
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 77d315dd87d9cab32605de415674d146eb9115fa
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
    
# <a name="enums"></a>枚举

***枚举类型***是包含一组已命名常量的独特值类型。 需要定义包含一组离散值的类型时，可以定义枚举。 枚举使用一种整型值类型作为其基础存储， 并提供离散值的语义含义。

以下示例声明并使用名为“`Color`”的 `enum` 类型，其中包含三个常量值（`Red`、`Green` 和 `Blue`）。

[!code-csharp[EnumExample](../../../samples/snippets/csharp/tour/enums/Program.cs#L3-L36)]

每个 `enum` 类型都有对应的整型类型（称为 `enum` 类型的***基础类型***）。 如果 `enum` 类型未显式声明基础类型，则基础类型为 `int`。 `enum` 类型的存储格式和可取值范围由基础类型决定。 `enum` 类型需要使用的一组值不受其 `enum` 成员限制。 尤其是，基础类型的 `enum` 的任何值都可以显式转换成 `enum` 类型，并作为 `enum` 类型的不同有效值。

以下示例声明基础类型为 `sbyte` 且名为“`Alignment`”的 `enum` 类型。

[!code-csharp[EnumStorage](../../../samples/snippets/csharp/tour/enums/Program.cs#L38-L43)]

如上面的示例所示，`enum` 成员声明可以包含用于指定成员值的常数表达式。 每个 `enum` 成员的常量值都必须介于 `enum` 的基础类型范围内。 如果 `enum` 成员声明未显式指定值，那么会为成员指定值 0（如果是 `enum` 类型中的首个成员）或原文前一个 `enum` 成员的值加 1。

可使用类型显式转换功能将 `Enum` 值转换成整型值，反之亦然。 例如: 

[!code-csharp[EnumStorage](../../../samples/snippets/csharp/tour/enums/Program.cs#L49-L50)]

任何 `enum` 类型的默认值都是已转换成 `enum` 类型的整型值 0。 如果变量被自动初始化为默认值，这就是为 `enum` 类型的变量指定的值。 为了让 `enum` 类型的默认值可供方便使用，文本类型 `0` 隐式转换成任意 `enum` 类型。 因此，可以运行以下命令。

[!code-csharp[EnumZero](../../../samples/snippets/csharp/tour/enums/Program.cs#L58-L58)]

>[!div class="step-by-step"]
[上一页](interfaces.md)
[下一页](delegates.md)

