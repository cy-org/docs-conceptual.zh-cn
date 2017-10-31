---
title: "放弃 - C# 指南 | Microsoft Docs"
description: "介绍 C# 对放弃的支持（放弃是未赋值的可丢弃变量），以及放弃的使用方式。"
keywords: .NET,.NET Core
author: rpetrusha
ms.author: ronpet
ms.date: 07/21/2017
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.translationtype: HT
ms.sourcegitcommit: 6170e096e36f8d054fdfe9cbd8311e6492e32a04
ms.openlocfilehash: 3f8804f9b7522e385b145a9643dec942cc1aab9f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/28/2017

---
# <a name="discards---c-guide"></a>放弃 - C# 指南

从 C# 7 开始，C# 支持放弃，这是一种在应用程序代码中人为取消使用的临时虚拟变量。 放弃相当于未赋值的变量；它们没有值。 因为只有一个放弃变量，并且甚至不为该变量分配存储空间，所以放弃可减少内存分配。 因为它们使代码的意图清楚，增强了其可读性和可维护性。

通过将下划线 (`_`) 赋给一个变量作为其变量名，指示该变量为一个放弃。 例如，以下方法调用返回一个 3 元组，其中第一个和第二个值为放弃：

```csharp
(var _, _, area) = city.GetCityInformation(cityName);
```

在 C# 7 中，支持在以下上下文中的分配中使用放弃：

- 元组和对象[析构](deconstruct.md)。
- 使用 [is](language-reference/keywords/is.md) 和 [switch](language-reference/keywords/switch.md) 的模式匹配。
- 对具有 `out` 参数的方法的调用。
- 当范围内没有 `_` 时，独立的 `_`。

当 `_` 是有效放弃时，尝试检索其值或在赋值操作中使用它时会生成编译器错误 CS0301：当前上下文中不存在名称 "\_"。 这是因为 `_` 未赋值，甚至可能未分配存储位置。 如果它是一个实际变量，则不能像之前的示例那样放弃多个值。

## <a name="tuple-and-object-deconstruction"></a>元组和对象析构

如果应用程序代码使用某些元组元素但忽略其他元素，这时使用放弃来处理元组就会特别有用。 例如，以下的 `QueryCityDataForYears` 方法返回一个 6 元组，包含城市名称、城市面积、一个年份、该年份的城市人口、另一个年份及该年份的城市人口。 该示例显示了两个年份之间人口的变化。 对于元组提供的数据，我们不关注城市面积，并在一开始就知道城市名称和两个日期。 因此，我们只关注存储在元组中的两个人口数量值，可将其余值作为放弃处理。  

[!code-csharp[元组-放弃](../../samples/snippets/csharp/programming-guide/deconstructing-tuples/discard-tuple1.cs)]

有关使用放弃析构元组的详细信息，请参阅[析构元组和其他类型](deconstruct.md#deconstructing-tuple-elements-with-discards)。

类、结构或接口的 `Deconstruct` 方法还允许从对象中检索和析构一组特定的数据。 如果想只使用析构值的一个子集时，可使用放弃。 以下示例将 `Person` 对象析构为四个字符串（名字、姓氏、城市和省/市/自治区），但舍弃姓氏和省/市/自治区。

[!code-csharp[类-放弃](../../samples/snippets/csharp/programming-guide/deconstructing-tuples/class-discard1.cs)]

有关使用放弃析构用户定义的类型的详细信息，请参阅[析构元组和其他类型](deconstruct.md#deconstructing-a-user-defined-type-with-discards)。

## <a name="pattern-matching-with-switch-and-is"></a>使用 `switch` 和 `is` 的模式匹配

放弃模式可通过 [is](language-reference/keywords/is.md) 和 [switch](language-reference/keywords/switch.md) 关键字用于模式匹配。 每个表达式始终匹配放弃模式。

以下示例定义了一个 `ProvidesFormatInfo` 方法，该方法使用 [is](language-reference/keywords/is.md) 语句来确定对象是否提供 <xref:System.IFormatProvider> 实现并测试对象是否为 `null`。 它还使用放弃模式来处理任何其他类型的非 null 对象。

[!code-csharp[放弃-模式](../../samples/snippets/csharp/programming-guide/discards/discard-pattern2.cs)]

## <a name="calls-to-methods-with-out-parameters"></a>使用 out 参数调用方法

当调用 `Deconstruct` 方法来析构用户定义类型（类、结构或接口的实例）时，可放弃单个 `out` 参数的值。 但当使用 out 参数调用任何方法时，也可放弃 `out` 参数的值。 

以下示例调用 [DateTime.TryParse(String, out DateTime)](<xref:System.DateTime.TryParse(System.String,System.DateTime@)>) 方法来确定日期的字符串表示形式在当前区域性中是否有效。 因为该示例侧重验证日期字符串，而不是解析它来提取日期，所以方法的 `out` 参数为放弃。

[!code-csharp[放弃-使用 out](../../samples/snippets/csharp/programming-guide/discards/discard-out1.cs)]

## <a name="a-standalone-discard"></a>独立放弃

可使用独立放弃来指示要忽略的任何变量。 以下示例使用独立放弃来忽略异步操作返回的 <xref:System.Threading.Tasks.Task> 对象。 这一操作的效果等同于抑制操作即将完成时所引发的异常。

[!code-csharp[独立-放弃](../../samples/snippets/csharp/programming-guide/discards/standalone-discard1.cs)]

请注意，`_` 也是有效标识符。 当在支持的上下文之外使用时，`_` 不视为放弃，而视为有效变量。 如果名为 `_` 的标识符已在范围内，则使用 `_` 作为独立放弃可能导致：

- 将预期的放弃的值赋给范围内 `_` 变量，会导致该变量的值被意外修改。 例如: 

   [!code-csharp[独立-放弃](../../samples/snippets/csharp/programming-guide/discards/standalone-discard2.cs#1)]
 
- 因违反类型安全而发生的编译器错误。 例如: 

   [!code-csharp[独立-放弃](../../samples/snippets/csharp/programming-guide/discards/standalone-discard2.cs#2)]
 
- 编译器错误 CS0136：“无法在此范围中声明名为“_”的局部变量或参数，因为该名称用于在封闭的局部范围中定义局部变量或参数”。 例如: 

   [!code-csharp[独立-放弃](../../samples/snippets/csharp/programming-guide/discards/standalone-discard2.cs#3)]

## <a name="see-also"></a>请参阅
[解构元组和其他类型](deconstruct.md)   
[`is` 关键字](language-reference/keywords/is.md)   
[`switch` 关键字](language-reference/keywords/switch.md)   

