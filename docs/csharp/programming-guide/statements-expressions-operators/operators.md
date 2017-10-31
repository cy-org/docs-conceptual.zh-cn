---
title: "运算符（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- operators [C#]
- C# language, operators
- operators [C#], about operators
ms.assetid: 214e7b83-1a41-4f7c-9867-64e9c0bab39f
caps.latest.revision: 42
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
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 22d2f6b93a18fcacbeea10ab60a1d078c632b0af
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="operators-c-programming-guide"></a>运算符（C# 编程指南）
在 C# 中，运算符  是应用于表达式或语句中的一个或多个操作数  的程序元素。 接受一个操作数的运算符称为`++`一元 `new`运算符，例如递增运算符 ( *) 或* 。 接受两个操作数的运算符称为`+`二元`-`运算符，例如算术运算符（`*`、`/`、 *、* ）。 条件运算符`?:`接受三个操作数，是 C# 中唯一的三元运算符。  
  
 下面的 C# 语句包含一个一元运算符和一个操作数。 递增运算符 `++` 修改操作数 `y` 的值。  
  
 [!code-cs[csProgGuideStatements#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/operators_1.cs)]  
  
 下面的 C# 语句包含两个二元运算符，它们分别有两个操作数。 赋值运算符 `=` 将一个整数变量 `y` 和一个表达式 `2 + 3` 作为操作数。 表达式 `2 + 3` 本身由加法运算符和两个操作数 `2` 和 `3` 组成。  
  
 [!code-cs[csProgGuideStatements#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/operators_2.cs)]  
  
## <a name="operators-evaluation-and-operator-precedence"></a>运算符、计算和运算符优先级  
 操作数可以是由任何长度的代码组成的有效表达式，且可包含任意数量的子表达式。 在包含多个运算符的表达式中，运算符的应用顺序由运算符优先级 、关联性 和括号确定。  
  
 每个运算符都具有已定义的优先级。 在包含具有不同优先级级别的多个运算符的表达式中，运算符的优先级确定运算符的计算顺序。 例如，下列语句将 3 赋给 `n1`。  
  
 `n1 = 11 - 2 * 4;`  
  
 因为乘法的优先级高于减法，所以首先执行乘法。  
  
 下表根据运算符执行的操作类型将它们划分到不同的类别中。 类别按优先级顺序列出。  
  
 **主要运算符**  
  
|Expression|描述|  
|----------------|-----------------|  
|x[.](../../../csharp/language-reference/operators/member-access-operator.md)y<br /><br /> x?.y|成员访问<br /><br /> 条件成员访问|  
|f[(x)](../../../csharp/language-reference/operators/invocation-operator.md)|方法和委托调用|  
|a[&#91;x&#93;](../../../csharp/language-reference/operators/index-operator.md)<br /><br /> a?[x]|数组和索引器访问<br /><br /> 条件数组和索引器访问|  
|x[++](../../../csharp/language-reference/operators/increment-operator.md)|后递增|  
|x[--](../../../csharp/language-reference/operators/decrement-operator.md)|后递减|  
|[new](../../../csharp/language-reference/keywords/new-operator.md) T(...)|对象和委托创建|  
|`new` T(...){...}|具有初始值设定项的对象创建。 请参阅[对象和集合初始值设定项](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)。|  
|`new` {...}|匿名对象初始值设定项。 请参阅[匿名类型](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)。|  
|`new` T[...]|数组创建。 请参阅[数组](../../../csharp/programming-guide/arrays/index.md)。|  
|[typeof](../../../csharp/language-reference/keywords/typeof.md)(T)|获取 T 的 System.Type 对象|  
|[checked](../../../csharp/language-reference/keywords/checked.md)(x)|在已检查的上下文中计算表达式|  
|[unchecked](../../../csharp/language-reference/keywords/unchecked.md)(x)|在未检查的上下文中计算表达式|  
|[default](../../../csharp/language-reference/keywords/default.md) (T)|获取类型 T 的默认值|  
|[delegate](../../../csharp/language-reference/keywords/delegate.md) {}|匿名函数（匿名方法）|  
  
 **一元运算符**  
  
|Expression|描述|  
|----------------|-----------------|  
|[+](../../../csharp/language-reference/operators/addition-operator.md)x|标识|  
|[-](../../../csharp/language-reference/operators/subtraction-operator.md)x|求反|  
|[!](../../../csharp/language-reference/operators/logical-negation-operator.md)x|逻辑求反|  
|[~](../../../csharp/language-reference/operators/bitwise-complement-operator.md)x|按位求反|  
|[++](../../../csharp/language-reference/operators/increment-operator.md)x|前递增|  
|[--](../../../csharp/language-reference/operators/decrement-operator.md)x|前递减|  
|[(T)](../../../csharp/language-reference/operators/invocation-operator.md)x|将 x 显式转换为类型 T|  
  
 **乘法运算符**  
  
|Expression|描述|  
|----------------|-----------------|  
|[*](../../../csharp/language-reference/operators/multiplication-operator.md)|乘法|  
|[/](../../../csharp/language-reference/operators/division-operator.md)|除号|  
|[%](../../../csharp/language-reference/operators/modulus-operator.md)|余数|  
  
 **相加运算符**  
  
|Expression|描述|  
|----------------|-----------------|  
|x [+](../../../csharp/language-reference/operators/addition-operator.md) y|相加、字符串串联、委托组合|  
|x [-](../../../csharp/language-reference/operators/subtraction-operator.md) y|相减、委托移除|  
  
 **移位运算符**  
  
|Expression|描述|  
|----------------|-----------------|  
|x [<\<](../../../csharp/language-reference/operators/left-shift-operator.md) y|左移|  
|x [>>](../../../csharp/language-reference/operators/right-shift-operator.md) y|右移|  
  
 **关系和类型运算符**  
  
|Expression|描述|  
|----------------|-----------------|  
|x [\<](../../../csharp/language-reference/operators/less-than-operator.md) y|小于|  
|x [>](../../../csharp/language-reference/operators/greater-than-operator.md) y|大于|  
|x [\<=](../../../csharp/language-reference/operators/less-than-equal-operator.md) y|小于或等于|  
|x [>=](../../../csharp/language-reference/operators/greater-than-equal-operator.md) y|大于或等于|  
|x [is](../../../csharp/language-reference/keywords/is.md) T|如果 x 为 T，则返回 True；否则返回 False。|  
|x [as](../../../csharp/language-reference/keywords/as.md) T|返回类型为 T 的 x，如果 x 不是 T，则返回 null|  
  
 **相等运算符**  
  
|Expression|描述|  
|----------------|-----------------|  
|x [==](../../../csharp/language-reference/operators/equality-comparison-operator.md) y|等于|  
|x [!=](../../../csharp/language-reference/operators/not-equal-operator.md) y|不等于|  
  
 **逻辑、条件和 Null 运算符**  
  
|类别|Expression|描述|  
|--------------|----------------|-----------------|  
|逻辑“与”|x [&](../../../csharp/language-reference/operators/and-operator.md) y|整型按位“与”，布尔型逻辑“与”|  
|逻辑 XOR|x [^](../../../csharp/language-reference/operators/xor-operator.md) y|整型按位 XOR，布尔型逻辑 XOR|  
|逻辑“或”|x [&#124;](../../../csharp/language-reference/operators/or-operator.md) y|整型按位“或”，布尔型逻辑“或”|  
|条件“与”|x [&&](../../../csharp/language-reference/operators/conditional-and-operator.md) y|仅当 x 为 True 时计算 y|  
|条件“或”|x [&#124;&#124;](../../../csharp/language-reference/operators/conditional-or-operator.md) y|仅当 x 为 False 时计算 y|  
|null 合并|x [??](../../../csharp/language-reference/operators/null-conditional-operator.md) y|如果 x 为 Null，则计算结果为 y，否则计算结果为 x|  
|条件运算|x [?](../../../csharp/language-reference/operators/conditional-operator.md) y : z|如果 x 为 True，则计算结果为 y；如果 x 为 False 则计算结果为 z|  
  
 **赋值和匿名运算符**  
  
|Expression|描述|  
|----------------|-----------------|  
|[=](../../../csharp/language-reference/operators/assignment-operator.md)|赋值|  
|x op= y|复合赋值。 支持以下这些运算符：[+=](../../../csharp/language-reference/operators/addition-assignment-operator.md)、[-=](../../../csharp/language-reference/operators/subtraction-assignment-operator.md)、[*=](../../../csharp/language-reference/operators/multiplication-assignment-operator.md)、[/=](../../../csharp/language-reference/operators/division-assignment-operator.md)、[%=](../../../csharp/language-reference/operators/modulus-assignment-operator.md)、[&=](../../../csharp/language-reference/operators/and-assignment-operator.md)、[&#124;=](../../../csharp/language-reference/operators/or-assignment-operator.md)、[!=](../../../csharp/language-reference/operators/not-equal-operator.md)、[<\<=](../../../csharp/language-reference/operators/left-shift-assignment-operator.md)、[>>=](../../../csharp/language-reference/operators/right-shift-assignment-operator.md)|  
|(T x) [=>](../../../csharp/language-reference/operators/lambda-operator.md) y|匿名函数（lambda 表达式）|  
  
## <a name="associativity"></a>结合性  
 当表达式中出现两个或两个以上具有相同优先级的运算符时，将根据结合性计算它们。 左结合运算符按从左到右的顺序计算。 例如，`x * y / z` 将计算为 `(x * y) / z`。 右结合运算符按从右到左的顺序计算。 例如，赋值运算符是右关联的。 如果不是，下面的代码将导致错误。  
  
```csharp  
int a, b, c;  
c = 1;  
// The following two lines are equivalent.  
a = b = c;  
a = (b = c);  
  
// The following line, which forces left associativity, causes an error.  
//(a = b) = c;  
```  
  
 再举一个例子，三元运算符 ([?:](../../../csharp/language-reference/operators/conditional-operator.md)) 是右结合运算符。 大多数的二元运算符是左结合运算符。  
  
 无论表达式中的运算符是左结合运算符还是右结合运算符，都将先从左至右评估各表达式的操作数。 以下示例显示运算符和操作数的计算顺序。  
  
|语句|计算顺序|  
|---------------|-------------------------|  
|`a = b`|a、b、=|  
|`a = b + c`|a、b、c、+、=|  
|`a = b + c * d`|a、b、c、d、*、+、=|  
|`a = b * c + d`|a、b、c、*、d、+、=|  
|`a = b - c + d`|a、b、c、-、d、+、=|  
|`a += b -= c`|a、b、c、-=、+=|  
  
## <a name="adding-parentheses"></a>添加括号  
 可通过使用圆括号更改运算符优先级和相关性。 例如，`2 + 3 * 2` 通常计算结果为 8，因为乘法运算符的优先级高于加法运算符。 但是，如果你将表达式编写为 `(2 + 3) * 2`，则先计算加法，再计算乘法，且结果为 10。 以下示例显示括号表达式中的计算顺序。 如前面的示例中所示，计算操作数之前会应用运算符。  
  
|语句|计算顺序|  
|---------------|-------------------------|  
|`a = (b + c) * d`|a、b、c、+、d、*、=|  
|`a = b - (c + d)`|a、b、c、d、+、-、=|  
|`a = (b + c) * (d - e)`|a、b、c、+、d、e、-、*、=|  
  
## <a name="operator-overloading"></a>运算符重载  
 对于自定义类和结构，你可以更改运算符的行为。 此过程称为“运算符重载” 。 有关详细信息，请参阅[可重载运算符](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md)。  
  
## <a name="related-sections"></a>相关章节  
 有关详细信息，请参阅[运算符关键字](../../../csharp/language-reference/keywords/operator-keywords.md)和 [C# 运算符](../../../csharp/language-reference/operators/index.md)。  
  
## <a name="see-also"></a>请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [语句、表达式和运算符](../../../csharp/programming-guide/statements-expressions-operators/index.md)

