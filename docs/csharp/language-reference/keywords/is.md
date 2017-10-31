---
title: "is（C# 参考）"
keywords: "is 关键字 (C#), is (C#)"
ms.date: 2017-02-17
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- is_CSharpKeyword
- is
dev_langs:
- CSharp
helpviewer_keywords:
- is keyword [C#]
ms.assetid: bc62316a-d41f-4f90-8300-c6f4f0556e43
caps.latest.revision: 20
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 81117b1419c2a9c3babd6a7429052e2b23e08a70
ms.openlocfilehash: 5aeb29a799ba24b5ab7db3eca62a91035b25b8f6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="is-c-reference"></a>is（C# 参考） #

检查对象是否与给定类型兼容，或（从 C# 7 开始）针对某个模式测试表达式。

## <a name="testing-for-type-compatibility"></a>类型兼容性测试 ##

`is` 关键字在运行时评估类型兼容性。 它确定对象实例或表达式结果是否可转换为指定类型。 语法如下：

```csharp
   expr is type
```

其中 *expr* 是计算结果为某个类型的实例的表达式，而 *type* 是 *expr* 结果要转换到的类型的名称。 如果 *expr* 非空，并且通过计算表达式得出的对象可转换为 *type*，则 `is` 语句为 `true`；否则返回 `false`。

例如，以下代码确定 `obj` 是否可转换为 `Person` 类型的实例：

[!code-cs[is#1](../../../../samples/snippets/csharp/language-reference/keywords/is/is1.cs#1)]

如果满足以下条件，则 `is` 语句为 true：

- *expr* 是与 *type* 具有相同类型的一个实例。

- *expr* 是派生自 *type* 的类型的一个实例。 换言之，*expr* 结果可以向上转换为 *type* 的一个实例。

- *expr* 具有属于 *type* 的一个基类的编译时类型，*expr* 还具有属于 *type* 或派生自 *type* 的运行时类型。 变量的编译时类型是其声明中定义的变量类型。 变量的运行时类型是分配给该变量的实例类型。

- *expr* 是实现 *type* 接口的类型的一个实例。

下例表明，对于所有这些转换，`is` 表达式的计算结果都为 `true`。

[!code-cs[is#3](../../../../samples/snippets/csharp/language-reference/keywords/is/is3.cs#3)]

如果已知表达式始终为 `true` 或 `false`，则 `is` 关键字会生成编译时警告。 它只考虑引用转换、装箱转换和取消装箱转换；不考虑用户定义的转换或由类型的[隐式](implicit.md)和[显式](explicit.md)运算符定义的转换。 下例生成警告，因为转换结果在编译时就已知。 请注意，`is` 表达式从 `int` 到 `long` 和 `double` 的转换会返回 false，因为这些转换由[隐式](implicit.md)运算符处理。

[!code-cs[is#2](../../../../samples/snippets/csharp/language-reference/keywords/is/is2.cs#2)]

`expr` 可以是返回值的任何表达式，匿名方法和 Lambda 表达式除外。 下例使用 `is` 来计算方法调用的返回值。   
[!code-cs[is#4](../../../../samples/snippets/csharp/language-reference/keywords/is/is4.cs#4)]

从 C# 7 开始，可以使用[类型模式](#type)的模式匹配来编写代码，代码使用 `is` 语句更为简洁。

## <a name="pattern-matching-with-is"></a>利用 `is` 的模式匹配 ##

从 C# 7 开始，`is` 和 [switch](../../../csharp/language-reference/keywords/switch.md) 语句支持模式匹配。 `is` 关键字支持以下模式：

- [类型模式](#type)，用于测试表达式是否可转换为指定类型，如果可以，则将其转换为该类型的一个变量。

- [常量模式](#constant)，用于测试表达式计算结果是否为指定的常数值。

- [var 模式](#var)，始终成功的匹配，可将表达式的值绑定到新局部变量。 

### <a name="type" />类型模式</a>

使用类型模式执行模式匹配时，`is` 会测试表达式是否可转换为指定类型，如果可以，则将其转换为该类型的一个变量。 它是 `is` 语句的直接扩展，可执行简单的类型计算和转换。 `is` 类型模式的一般形式为：

```csharp
   expr is type varname 
```

其中 *expr* 是计算结果为某个类型的实例的表达式，*type* 是 *expr* 结果要转换到的类型的名称，*varname* 是 *expr* 结果要转换到的对象（如果 `is` 测试为 `true`）。 

如果以下任一条件成立，则 `is` 表达式为 `true`：

- *expr* 是与 *type* 具有相同类型的一个实例。

- *expr* 是派生自 *type* 的类型的一个实例。 换言之，*expr* 结果可以向上转换为 *type* 的一个实例。

- *expr* 具有属于 *type* 的一个基类的编译时类型，*expr* 还具有属于 *type* 或派生自 *type* 的运行时类型。 变量的编译时类型是其声明中定义的变量类型。 变量的运行时类型是分配给该变量的实例类型。

- *expr* 是实现 *type* 接口的类型的一个实例。

如果 *exp* 为 `true`，且 `is` 与 `if` 语句一起使用，则会分配 *varname*，并且其仅在 `if` 语句中具有局部范围。

下列示例使用 `is` 类型模式为类型的 <xref:System.IComparable.CompareTo(System.Object)?displayProperty=nameWithType> 方法提供实现。

[!code-cs[is#5](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern5.cs#5)]

如果没有模式匹配，则可能按以下方式编写此代码。 使用类型模式匹配无需测试转换结果是否为 `null`，从而生成更紧凑易读的代码。  

[!code-cs[is#6](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern6.cs#6)]

确定值类型的类型时，`is` 类型模式也会生成更紧凑的代码。 下例在显示相应属性的值之前使用 `is` 类型模式来确定对象是 `Person` 还是 `Dog` 实例。 

[!code-cs[is#9](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern9.cs#9)]

对于无模式匹配的等效代码，需要为其单独分配显式转换。

[!code-cs[is#10](../../../../samples/snippets/csharp/language-reference/keywords/is/is-type-pattern10.cs#10)]

### <a name="a-nameconstant--constant-pattern"></a><a name="constant" />常量模式 ###

使用常量模式执行模式匹配时，`is` 会测试表达式结果是否等于指定常量。 在 C# 6 和更低版本中，[switch](switch.md) 语句支持常量模式。 从 C# 7 开始，`is` 语句也支持常量模式。 语法为：

```csharp
   expr is constant
```

其中 *expr* 是要计算的表达式，*constant* 是要测试的值。 *constant* 可以是以下任何常数表达式： 

- 一个文本值。

- 已声明 `const` 变量的名称。

- 一个枚举常量。

常数表达式的计算方式如下：

- 如果 *expr* 和 *constant* 均为整型类型，则 C# 相等运算符确定表示式是否返回 `true`（即，是否为 `expr == constant`）。

- 否则，由对静态 [Object.Equals(expr, constant)](xref:System.Object.Equals(System.Object,System.Object)) 方法的调用来确定表达式的值。  

下例同时使用了类型模式和常量模式来测试对象是否为 `Dice` 实例，如果是，则确定骰子的值是否为 6。

[!code-cs[is#7](../../../../samples/snippets/csharp/language-reference/keywords/is/is-const-pattern7.cs#7)]
 
### <a name="var" />var 模式</a>

具有 var 模式的模式匹配始终成功。 语法为

```csharp 
   expr is var varname
```

其中，*expr* 的值始终分配给名为 *varname* 的局部变量。 *varname* 是一个与 *expr* 具有相同类型的静态变量。 下例使用 var 模式向名为 `obj` 的变量分配表达式。 然后，显示 `obj` 的值和类型。

[!code-cs[is#8](../../../../samples/snippets/csharp/language-reference/keywords/is/is-var-pattern8.cs#8)]

请注意，如果 *expr* 为 `null`，则 `is` 表达式仍为 true 并向 *varname* 分配 `null`。 

# <a name="c-language-specification"></a>C# 语言规范
  
[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [typeof](../../../csharp/language-reference/keywords/typeof.md)   
 [as](../../../csharp/language-reference/keywords/as.md)   
 [运算符关键字](../../../csharp/language-reference/keywords/operator-keywords.md)

