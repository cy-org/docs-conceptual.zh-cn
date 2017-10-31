---
title: "默认值表达式（C# 编程指南）"
description: "默认值表达式生成任何引用类型或值类型的默认值"
ms.date: 2017-08-23
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- generics [C#], default keyword
- default keyword [C#], generic programming
ms.assetid: b9daf449-4e64-496e-8592-6ed2c8875a98
caps.latest.revision: 22
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 1e548df4de2c07934313311a7ffcfae82be76000
ms.openlocfilehash: 7b5b53d7ed92c6f6377a3e494daf1d02a4cf0934
ms.contentlocale: zh-cn
ms.lasthandoff: 08/29/2017

---
# <a name="default-value-expressions-c-programming-guide"></a>默认值表达式（C# 编程指南）

默认值表达式生成类型的默认值。 默认值表达式在泛型类和泛型方法中非常有用。 使用泛型类和泛型方法时出现的一个问题是，如何在无法提前知道以下内容的情况下将默认值赋值给参数化类型 `T`：

- `T` 是引用类型还是值类型。
- 如果 `T` 是值类型，它是数值还是用户定义的结构。

 已知参数化类型 `T` 的变量 `t`，仅当 `T` 为引用类型时，语句 `t = null` 才有效。 赋值 `t = 0` 仅对数值类型有效，对结构无效。 解决方案是使用默认值表达式，该表达式对引用类型（类类型和接口类型）返回 `null`，对数值类型返回零。 对于用户定义的结构，返回初始化为零位模式的结构，该结构根据成员是值还是引用类型，为每个成员生成 0 或 `null`。 对于可为 NULL 的值类型，`default` 返回像任何结构一样初始化的 <xref:System.Nullable%601?displayProperty=fullName>。

`default(T)` 表达式不限于泛型类和泛型方法。 默认值表达式可用于任何托管类型。 以下任一表达式都是有效的：

 [!code-cs[csProgGuideGenerics#1](../../../../samples/snippets/csharp/programming-guide/statements-expressions-operators/default-value-expressions.cs)]

 `GenericList<T>` 类的以下示例演示如何在泛型类中使用 `default(T)` 运算符。 有关详细信息，请参阅[泛型概述](../generics/introduction-to-generics.md)。

 [!code-cs[csProgGuideGenerics#2](../../../../samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideGenerics/CS/Generics.cs#Snippet41)]

## <a name="default-literal-and-type-inference"></a>默认文本和类型推理

从 C# 7.1 开始，当编译器可以推断表达式的类型时，文本 `default` 可用于默认值表达式。 文本 `default` 生成与等效项 `default(T)`（其中，`T` 是推断的类型）相同的值。 这可减少多次声明类型的冗余，从而使代码更加简洁。 文本 `default` 可用于以下任一位置：

- 变量初始值设定项
- 变量赋值
- 声明可选参数的默认值
- 为方法调用参数提供值
- 返回语句（或 expression bodied 成员中的表达式）

以下示例展示了文本 `default` 在默认值表达式中的多种用法：

[!code-cs[csProgGuideGenerics#3](../../../../samples/snippets/csharp/programming-guide/statements-expressions-operators/default-literal.cs)]

## <a name="see-also"></a>请参阅

 <xref:System.Collections.Generic> [C# 编程指南](../index.md)   
 [泛型](../generics/index.md)   
 [泛型方法](../generics/generic-methods.md)   
 [泛型](~/docs/standard/generics/index.md)   

