---
title: "switch 关键字（C# 参考）"
ms.date: 2017-03-07
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- switch_CSharpKeyword
- switch
- case
- case_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- switch statement [C#]
- switch keyword [C#]
- case statement [C#]
- default keyword [C#]
ms.assetid: 44bae8b8-8841-4d85-826b-8a94277daecb
caps.latest.revision: 47
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 387c8c7e44ab818ca97e686330746f50df091bb9
ms.openlocfilehash: 5c151e3bbd46212f1234d46ff05d389f2384ca0e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="switch-c-reference"></a>switch（C# 参考）
`switch` 是一个选择语句，它根据与匹配表达式匹配的模式，从候选列表中选择单个开关部分进行执行。 
  
 [!code-cs[switch#1](../../../../samples/snippets/csharp/language-reference/keywords/switch/switch1.cs#1)]  

如果针对 3 个或更多条件测试单个表达式，`switch` 语句通常用作 [if-else](if-else.md) 构造的替代项。 例如，以下 `switch` 语句确定类型为 `Color` 的变量是否具有三个值之一： 

[!code-cs[switch#3](../../../../samples/snippets/csharp/language-reference/keywords/switch/switch3.cs#1)] 

它等效于使用 `if`- `else` 构造的以下示例。 

[!code-cs[switch#3a](../../../../samples/snippets/csharp/language-reference/keywords/switch/switch3a.cs#1)] 

## <a name="the-match-expression"></a>匹配表达式

匹配表达式提供与 `case` 标签中的模式相匹配的值。 语法为：

```csharp
   switch (expr)
```

在 C# 6 中，匹配表达式必须是返回以下类型值的表达式：

- [字符型](char.md)。
- [字符串](string.md)。
- [bool](bool.md)。 
- 整数值，例如 [int](int.md) 或 [long](long.md)。
- [枚举](enum.md)值。

从 C# 7 开始，匹配表达式可以是任何非 null 表达式。
 
## <a name="the-switch-section"></a>开关部分
 
 `switch` 语句包含一个或多个开关部分。 每个开关部分包含一个或多个 case 标签，后接一个或多个语句。 下面的示例展示了一个包含三个开关部分的简单 `switch` 语句。 每个开关部分各有一个 case 标签（例如 `case 1:`）和两个语句。
 
  `switch` 语句中可以包含任意数量的开关部分，每个开关部分可以具有一个或多个 case 标签，如以下示例所示。 但是，任何两个 case 标签不可包含相同的表达式。  

 [!code-cs[switch#2](../../../../samples/snippets/csharp/language-reference/keywords/switch/switch2.cs#1)]  

 switch 语句执行中只有一个开关部分。 C# 不允许从一个开关部分继续执行到下一个开关部分。 因此，以下代码将生成编译器错误 CS0163：“控件不能从一个 case 标签 (<case label>) 贯穿到另一个 case 标签。”   

```csharp  
switch (caseSwitch)  
{  
    // The following switch section causes an error.  
    case 1:  
        Console.WriteLine("Case 1...");  
        // Add a break or other jump statement here.  
    case 2:  
        Console.WriteLine("... and/or Case 2");  
        break;  
}  
```  
通常通过使用 [break](break.md)、[goto](goto.md) 或 [return](return.md) 语句显式退出开关部分来满足此要求。 但是，以下代码也有效，因为它确保程序控件不能贯穿 `default` 开关部分。
  
 [!code-cs[switch#4](../../../../samples/snippets/csharp/language-reference/keywords/switch/switch4.cs#1)]    
  
 在 case 标签与匹配表达式匹配的开关部分中执行语句列表时，先执行第一个语句，再执行整个语句列表，通常执行到跳转语句（如 `break`、`goto case`、`goto label`、`return` 或 `throw`）为止。 此时，控件在 `switch` 语句之外进行传输或传输到另一个 case 标签。 如果使用 `goto` 语句，必须将控制权移交给常数标签。 此限制是必要的，因为尝试将控制权移交给非常数标签可能会产生不良的副作用，如将控制权移交给代码中的意外位置，或创建无限循环。

## <a name="case-labels"></a>Case 标签

 每个 case 标签指定一个模式与匹配表达式（前面示例中的 `caseSwitch` 变量）进行比较。 如果它们匹配，则将控件传输到包含**首次**匹配 case 标签的开关部分。 如果没有与匹配表达式匹配的 case 标签模式，则将控件传输到带有 `default` case 标签的部分（若有）。 如果没有 `default` case，将不会执行任何开关部分中的语句，并且会将控件传输到 `switch` 语句之外。

 有关 `switch` 语句和模式匹配的信息，请参阅使用 `switch` 语句的 [模式匹配](#pattern)部分。

 因为 C# 6 仅支持常量模式并且不允许重复常量值，所以 case 标签定义了互斥值，而且仅有一个模式可与匹配表达式相匹配。 因此，`case` 语句显示的顺序并不重要。

 然而，在 C# 7 中，因为支持其他模式，所以 case 标签不需要定义互斥值，并且多个模式可以与匹配表达式相匹配。 因为仅执行包含首次匹配模式的开关部分中的语句，所以 `case` 语句显示的顺序很重要。 如果 C# 检测到开关部分的 case 语句或语句等效于或是先前语句的子集，它将生成编译错误 CS8120：“开关 case 已由先前 case 处理。” 

 以下示例说明了使用各种非互斥模式的 `switch` 语句。 如果移动 `case 0:` 开关部分，使其不再是 `switch` 语句中的第一部分，C# 会生成编译器错误，因为值为零的整数是所有整数的子集（由 `case int val` 语句定义的模式）。

 [!code-cs[switch#5](../../../../samples/snippets/csharp/language-reference/keywords/switch/switch5.cs#1)]    

你可以通过以下两种方法之一更正此问题并消除编译器警告：

- 更改开关部分的顺序。 
 
- 在 `case` 标签中</a>使用 </a name="when">when 子句。
 
## <a name="the-default-case"></a>`default` case

如果匹配表达式与任何其他 `case` 标签不匹配，则 `default` case 指定要执行的开关部分。 如果不存在 `default` case，并且匹配表达式与其他任何 `case` 标签都不匹配，则程序流将贯穿 `switch` 语句。

`default` case 可以在 `switch` 语句中以任何顺序显示。 无论其在源代码中的顺序如何，都将在对所有 `case` 标签进行计算之后，最后对其进行计算。

## <a name="a-namepattern--pattern-matching-with-the-switch-statement"></a>使用 `switch` 语句的 <a name="pattern" /> 模式匹配
  
每个 `case` 语句定义一个模式，如果它与匹配表达式相匹配，则会导致执行其包含的开关部分。 所有版本的 C# 都支持常量模式。 其余模式从 C# 7 开始支持。 
  
### <a name="constant-pattern"></a>常量模式 

常量模式测试匹配表达式是否等于指定常量。 语法为：

```csharp
   case constant:
```

其中 *constant* 是要测试的值。 *constant* 可以是以下任何常数表达式： 

- [bool](bool.md) 文本，为 `true` 或 `false`。
- 任何整数常量，例如 [int](int.md)、[long](long.md) 或[字节](byte.md)。 
- 已声明 `const` 变量的名称。
- 一个枚举常量。
- [字符型](char.md)文本。
- [字符串](string.md)文本。

常数表达式的计算方式如下：

- 如果 *expr* 和 *constant* 均为整型类型，则 C# 相等运算符确定表示式是否返回 `true`（即，是否为 `expr == constant`）。

- 否则，由对静态 [Object.Equals(expr, constant)](xref:System.Object.Equals(System.Object,System.Object)) 方法的调用确定表达式的值。  

以下示例使用常量模式来确定特定日期是否为周末、工作周的第一天、工作周的最后一天或工作周的中间日期。 它根据 @System.DayOfWeek 枚举的成员计算当前日期的 [DateTime.DayOfWeek](xref:System.DateTime.DayOfWeek) 属性。 

[!code-cs[switch#7](../../../../samples/snippets/csharp/language-reference/keywords/switch/const-pattern.cs#1)]

以下示例使用常量模式在模拟自动咖啡机的控制台应用程序中处理用户输入。
  
 [!code-cs[switch#6](../../../../samples/snippets/csharp/language-reference/keywords/switch/switch6.cs)]  

### <a name="type-pattern"></a>类型模式

类型模式可启用简洁类型计算和转换。 使用 `switch` 语句执行模式匹配时，会测试表达式是否可转换为指定类型，如果可以，则将其转换为该类型的一个变量。 语法为：

```csharp
   case type varname 
```
其中 *type* 是 *expr* 结果要转换到的类型的名称，*varname* 是 *expr* 结果要转换到的对象（如果匹配成功）。 

如果以下任一条件成立，则 `case` 表达式为 `true`：

- *expr* 是与 *type* 具有相同类型的一个实例。

- *expr* 是派生自 *type* 的类型的一个实例。 换言之，*expr* 结果可以向上转换为 *type* 的一个实例。

- *expr* 具有属于 *type* 的一个基类的编译时类型，*expr* 还具有属于 *type* 或派生自 *type* 的运行时类型。 变量的编译时类型是其类型声明中定义的变量类型。 变量的运行时类型是分配给该变量的实例类型。

- *expr* 是实现 *type* 接口的类型的一个实例。

如果 case 表达式为 true，将会明确分配 *varname*，并且仅在开关部分中具有本地作用域。

请注意，`null` 与任何类型都不匹配。 若要匹配 `null`，请使用以下 `case` 标签：

```csharp
case null:
```
 
以下示例使用类型模式来提供有关各种集合类型的信息。

[!code-cs[switch#5](../../../../samples/snippets/csharp/language-reference/keywords/switch/type-pattern.cs#1)]

如果没有模式匹配，则可能按以下方式编写此代码。 使用类型模式匹配可消除测试转换结果是否为 `null` 或执行重复转换的必要，从而生成更紧凑易读的代码。  

[!code-cs[switch#6](../../../../samples/snippets/csharp/language-reference/keywords/switch/type-pattern2.cs#1)]

## <a name="the-case-statement-and-the-when-clause"></a>`case` 语句和 `when` 子句

从 C# 7 开始，因为 case 语句不需要互相排斥，因此可以添加 `when` 子句来指定必须满足的附加条件使 case 语句计算为 true。 `when` 子句可以是返回布尔值的任何表达式。 `when` 子句的更常见用法之一是防止在匹配表达式的值为 `null` 时执行开关部分。 

 下面的示例定义了 `Shape` 基类、从 `Shape` 派生的 `Rectangle` 类以及从 `Rectangle` 派生的 `Square` 类。 它使用 `when` 子句来确保 `ShowShapeInfo` 将已分配相等长度和宽度的 `Rectangle` 对象作为 `Square` 来处理（即使未实例化为 `Square` 对象）。 该方法不会尝试显示关于值为 `null` 的对象或区域为零的形状的信息。 

[!code-cs[switch#8](../../../../samples/snippets/csharp/language-reference/keywords/switch/when-clause.cs#1)]
  
请注意，不会执行尝试测试 `Shape` 对象是否为 `null` 的示例中的 `when` 子句。 测试是否为 `null` 的正确类型模式是 `case null:`。

## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  

 [C# 参考](../index.md)   
 [C# 编程指南](../../programming-guide/index.md)   
 [C# 关键字](index.md)   
 [if-else](if-else.md)   
 [模式匹配](../../pattern-matching.md)   
 

 

