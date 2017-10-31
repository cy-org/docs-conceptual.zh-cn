---
title: "可重载运算符（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- C# language, operator overloading
- operator overloading [C#]
ms.assetid: 390d9d01-79fc-40ab-9ed3-0bf448da1b6a
caps.latest.revision: 18
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
ms.sourcegitcommit: 1e548df4de2c07934313311a7ffcfae82be76000
ms.openlocfilehash: 9e4f54f3a5b461be267301a2b8bc8de52ef9f776
ms.contentlocale: zh-cn
ms.lasthandoff: 08/29/2017

---
# <a name="overloadable-operators-c-programming-guide"></a>可重载运算符（C# 编程指南）

C# 通过使用 [operator](../../../csharp/language-reference/keywords/operator.md) 关键字定义静态成员函数，来允许用户定义的类型重载运算符。 不过并非所有运算符都可以进行重载，并且其他运算符具有限制，如下表所列：

| 运算符 | 可重载性 |
| --------- | --------------- |
|[+](../../../csharp/language-reference/operators/addition-operator.md)、[-](../../../csharp/language-reference/operators/subtraction-operator.md)、[!](../../../csharp/language-reference/operators/logical-negation-operator.md)、[~](../../../csharp/language-reference/operators/bitwise-complement-operator.md)、[++](../../../csharp/language-reference/operators/increment-operator.md)、[--](../../../csharp/language-reference/operators/decrement-operator.md)、[true](../../../csharp/language-reference/keywords/true.md)、[false](../../../csharp/language-reference/keywords/false.md)|这些一元运算符可以进行重载。|
|[+](../../../csharp/language-reference/operators/addition-operator.md), [-](../../../csharp/language-reference/operators/subtraction-operator.md), [\*](../../../csharp/language-reference/operators/multiplication-operator.md), [/](../../../csharp/language-reference/operators/division-operator.md), [%](../../../csharp/language-reference/operators/modulus-operator.md), [&](../../../csharp/language-reference/operators/and-operator.md), [&#124;](../../../csharp/language-reference/operators/or-operator.md), [^](../../../csharp/language-reference/operators/xor-operator.md), [\<\<](../../../csharp/language-reference/operators/left-shift-operator.md), [>>](../../../csharp/language-reference/operators/right-shift-operator.md)|这些二元运算符可以进行重载。|
|[==](../../../csharp/language-reference/operators/equality-comparison-operator.md), [!=](../../../csharp/language-reference/operators/not-equal-operator.md), [\<](../../../csharp/language-reference/operators/less-than-operator.md), [>](../../../csharp/language-reference/operators/greater-than-operator.md), [\<=](../../../csharp/language-reference/operators/less-than-equal-operator.md), [>=](../../../csharp/language-reference/operators/greater-than-equal-operator.md)|比较运算符可以进行重载（但是请参阅此表后面的备注）。|
|[&&](../../../csharp/language-reference/operators/conditional-and-operator.md), [&#124;&#124;](../../../csharp/language-reference/operators/conditional-or-operator.md)|条件逻辑运算符无法进行重载，但是它们使用 `&` 和 <code>&#124;</code>（可以进行重载）来计算。|
|[&#91;&#93;](../../../csharp/language-reference/operators/index-operator.md)|数组索引运算符无法进行重载，但是可以定义索引器。|
|[(T)x](../../../csharp/language-reference/operators/invocation-operator.md)|强制转换运算符无法进行重载，但是可以定义新转换运算符（请参阅 [explicit](../../../csharp/language-reference/keywords/explicit.md) 和 [implicit](../../../csharp/language-reference/keywords/implicit.md)）。|
|[+=](../../../csharp/language-reference/operators/addition-assignment-operator.md), [-=](../../../csharp/language-reference/operators/subtraction-assignment-operator.md), [\*=](../../../csharp/language-reference/operators/multiplication-assignment-operator.md), [/=](../../../csharp/language-reference/operators/division-assignment-operator.md), [%=](../../../csharp/language-reference/operators/modulus-assignment-operator.md), [&=](../../../csharp/language-reference/operators/and-assignment-operator.md), [&#124;=](../../../csharp/language-reference/operators/or-assignment-operator.md), [^=](../../../csharp/language-reference/operators/xor-assignment-operator.md), [\<\<=](../../../csharp/language-reference/operators/left-shift-assignment-operator.md), [>>=](../../../csharp/language-reference/operators/right-shift-assignment-operator.md)|赋值运算符无法进行重载，但是 `+=`（举例）使用 `+`（可以进行重载）来计算。|
|[=](../../../csharp/language-reference/operators/assignment-operator.md)、[.](../../../csharp/language-reference/operators/member-access-operator.md)、[?:](../../../csharp/language-reference/operators/conditional-operator.md)、[??](../../../csharp/language-reference/operators/null-conditional-operator.md)、[->](../../../csharp/language-reference/operators/dereference-operator.md)、[=>](../../../csharp/language-reference/operators/lambda-operator.md)、[f(x)](../../../csharp/language-reference/operators/invocation-operator.md)、[as](../../../csharp/language-reference/keywords/as.md)、[checked](../../../csharp/language-reference/keywords/checked.md)、[unchecked](../../../csharp/language-reference/keywords/unchecked.md)、[default](../../../csharp/programming-guide/statements-expressions-operators/default-value-expressions.md)、[delegate](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)、[is](../../../csharp/language-reference/keywords/is.md)、[new](../../../csharp/language-reference/keywords/new.md)、[sizeof](../../../csharp/language-reference/keywords/sizeof.md)、[typeof](../../../csharp/language-reference/keywords/typeof.md)|这些运算符无法进行重载。|

> [!NOTE]
> 如果进行重载，则比较运算符必须成对进行重载；也就是说，如果 `==` 进行重载，则 `!=` 也必须进行重载。 反过来也成立，其中重载 `!=` 需要重载 `==`。 对于比较运算符 `<` 和 `>`，以及 `<=` 和 `>=`，也成立。

若要在自定义类上重载运算符，需要在该类上创建具有正确签名的方法。 该方法必须命名为“运算符 X”，其中 X 是重载的运算符的名称或符号。 一元运算符具有一个参数，二元运算符具有两个参数。 在每种情况下，都必须有一个参数与声明运算符的类或结构的类型相同。

```csharp
public static Complex operator +(Complex c1, Complex c2)
{
    return new Complex(c1.real + c2.real, c1.imaginary + c2.imaginary);
}
```

直接只返回表达式结果的定义很常见。  对于这些情况，有一种使用 `=>` 的语法快捷方式。

```csharp
public static Complex operator +(Complex c1, Complex c2) =>
        new Complex(c1.real + c2.real, c1.imaginary + c2.imaginary);
  
// Override ToString() to display a complex number in the traditional format:
public override string ToString() => $"{this.real} + {this.imaginary}";
```

有关详细新，请参阅[如何：使用运算符重载创建复数类](../../../csharp/programming-guide/statements-expressions-operators/how-to-use-operator-overloading-to-create-a-complex-number-class.md)。

## <a name="see-also"></a>请参阅

[C# 编程指南](../../../csharp/programming-guide/index.md)  
[语句、表达式和运算符](../../../csharp/programming-guide/statements-expressions-operators/index.md)  
[运算符](../../../csharp/programming-guide/statements-expressions-operators/operators.md)  
[C# 运算符](../../../csharp/language-reference/operators/index.md)  
[重载运算符为何在 C# 中始终是静态的？](http://go.microsoft.com/fwlink/?LinkId=112383)

