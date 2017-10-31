---
title: "ref 返回值和 ref 局部变量（C# 指南）"
description: "了解如何定义和使用 ref 返回值和 ref 局部变量"
author: rpetrusha
ms.author: ronpet
ms.date: 05/30/2017
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 18cf7a4b-29f0-4b14-85b8-80af754aabd8
ms.translationtype: HT
ms.sourcegitcommit: 4582cb0ee091526423cce3fc1d8243029f34f59c
ms.openlocfilehash: 3f2ee35db5b77efcce629b6315060a723429b19c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/16/2017

---
# <a name="ref-returns-and-ref-locals"></a>ref 返回值和局部变量

从 C# 7 开始，C# 支持引用返回值（ref 返回值）。 引用返回值允许方法将对象的引用（而不是值）返回给调用方。 然后，调用方可以选择将返回的对象视为按值返回或按引用返回。 调用方作为引用（而非值）处理的引用返回值为 ref 局部变量。

## <a name="what-is-a-reference-return-value"></a>什么是引用返回值？

绝大多数开发者都很熟悉将参数按引用传递给被调用的方法。 被调用方法的参数列表包括按引用传递的值，并且被调用方法对值所做的任何更改均返回给调用方。 引用返回值则恰巧相反：

- 被调用方法的返回值（而非被传递给它的参数）是一个引用。

- 调用方（而非被调用的方法）可以修改由方法返回的值。

- 不是参数的修改反映在调用方上对象的状态中，而是调用方对方法返回值的修改反映在其方法被调用的对象的状态中。

引用返回值可生成更紧凑的代码，并允许对象仅公开个别数据项，例如对调用方有用的数组元素。 这可以降低调用方无意间修改对象状态的风险。

对于能作为引用返回值被方法返回的值，这里还存在一些限制。 这些方法包括：

- 返回值不可为 `void`。 尝试使用 `void` 定义方法时，引用返回值将生成编译器错误 CS1547：“关键字 "void" 不能在此上下文中使用”。
 
- 返回值不能是返回该值的方法中的局部变量；其范围必须超越返回它的方法。 它可以是实例或类的静态字段，也可是传递给方法的参数。 尝试返回局部变量将生成编译器错误 CS8168：“无法按引用返回局部 "obj"，因为它不是 ref 局部变量”。

- 返回值不可为 `null`。 尝试返回 `null` 将生成编译器错误 CS8156：“无法在此上下文中使用表达式，因为它可能没有按引用返回”。

   如果包含 ref 返回值的方法需要返回 null 值，则可为引用类型返回 null（未实例化）值，或为值类型返回[可以为 null 的类型](../nullable-types/index.md)。
 
- 返回值不能为常数或枚举成员，也不能是 `class` 或 `struct` 的属性。 尝试返回它们将生成编译器错误 CS8156：“无法在此上下文中使用表达式，因为它可能没有按引用返回”。

此外，由于异步方法可能在完成执行前就返回，虽然它的返回值仍未知，但也不允许对异步方法使用引用返回值。
 
## <a name="defining-a-ref-return-value"></a>定义 ref 返回值

通过向方法签名的返回类型添加 [ref](../../language-reference/keywords/ref.md) 关键字来定义 ref 返回值。 例如下列签名表示，`GetContactInformation` 属性将对 `Person` 对象的引用返回给调用方：

```csharp
public ref Person GetContactInformation(string fname, string lname);
```

此外，方法正文中每个 [return](../../language-reference/keywords/return.md) 语句所返回对象的名称前面须有 [ref](../../language-reference/keywords/ref.md) 关键字。 例如，下列 `return` 语句按引用返回名为 `p` 的 `Person` 对象：

```csharp
return ref p;
```

## <a name="consuming-a-ref-return-value"></a>使用 ref 返回值

调用方可通过以下任一方式来处理 ref 返回值：

- 作为从方法中按值返回的普通值。 调用方可选择忽略返回值是引用返回值。 在这种情况中，对方法调用所返回的值进行的任何更改都不会反映在被调用类型的状态中。 如果返回的值是一个值类型，对方法调用所返回的值进行的任何更改都不会反映在被调用类型的状态中。

- 作为引用返回值。 调用方必须定义作为 [ref 局部变量](#ref-local)被赋予引用返回值的变量，且对方法调用所返回的值进行的任何更改都将反映在被调用类型的状态中。 

## <a name="ref-locals"></a>ref 局部变量

若要将引用返回值作为引用来处理，调用方必须使用 `ref` 关键字将值声明为 ref 局部变量。 例如，如果 `Person.GetContactInfomation` 方法所返回的值被作为引用（而非值）来使用，则方法调用将显示为：

```csharp
ref Person p = ref contacts.GetContactInformation("Brandie", "Best");
```

注意，请同时在局部变量声明前和方法调用前使用 `ref` 关键字。 无法同时将 `ref` 关键字包含在变量声明和赋值将导致编译器错误 CS8172：“无法使用值对按引用变量进行初始化”。 
 
对方法所返回的 `Person` 对象的后续更改将反映在 `contacts` 对象中。

如果未使用 `ref` 关键字将 `p` 定义为 ref 局部变量，则调用方对 `p` 所做的任何更改都不会反映在 `contacts` 对象中。
 
## <a name="ref-returns-and-ref-locals-an-example"></a>ref 返回结果和 ref 局部变量：示例

下列示例定义存储整数值数组的 `NumberStore` 类。 `FindNumber` 方法按引用返回第一个大于或等于作为参数传递的数字的数字。 如果没有大于或等于该参数的数字，则方法返回索引 0 中的数字。 

[!CODE-cs[ref-returns](../../../../samples/snippets/csharp/programming-guide/ref-returns/ref-returns1.cs#1)]

下列示例调用 `NumberStore.FindNumber` 方法来检索大于或等于 16 的第一个值。 然后，调用方将该方法返回的值加倍。 如示例中的输出所示，此更改将反映在 `NumberStore` 实例的数组元素的值中。

[!CODE-cs[ref-returns](../../../../samples/snippets/csharp/programming-guide/ref-returns/ref-returns1.cs#2)]

在不支持引用返回值的情况下，此类操作通常通过返回数组元素的索引和它的值来执行。 然后，调用方可使用此索引修改单个方法调用中的值。 但调用方也可修改要访问的索引，还可修改其他数组值。  
 
## <a name="see-also"></a>另请参阅

[ref 关键字](../../language-reference/keywords/ref.md)

