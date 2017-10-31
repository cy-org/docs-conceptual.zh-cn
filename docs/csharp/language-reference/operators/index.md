---
title: "C# 运算符"
ms.date: 2017-03-09
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- cs.operators
dev_langs:
- CSharp
helpviewer_keywords:
- boolean operators [C#]
- expressions [C#], operators
- logical operators [C#]
- operators [C#]
- Visual C#, operators
- indirection operators [C#]
- assignment operators [C#]
- shift operators [C#]
- relational operators [C#]
- bitwise operators [C#]
- address operators [C#]
- keywords [C#], operators
- arithmetic operators [C#]
ms.assetid: 0301e31f-22ad-49af-ac3c-d5eae7f0ac43
caps.latest.revision: 40
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
ms.sourcegitcommit: 9bb64ea7199f5699ff166d1affb7f8126dcc6612
ms.openlocfilehash: eb8c4f11e540aa2685989ef11b2515a32d8d1fd6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/02/2017

---
# <a name="c-operators"></a>C# 运算符
C# 提供了许多运算符，这些运算符是指定要在表达式中执行哪些操作（数学、索引、函数调用等等）的符号。  可以[重载](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md)许多应用于用户定义类型的运算符，从而更改其含义。  
  
 对整数类型执行的运算（如 `==`、`!=`、`<`、`>`、`&`、`|`）通常也可对枚举 (`enum`) 类型执行。  
  
 以下章节按最高优先级到最低优先级的顺序列示 C# 运算符。  各章节内运算符的优先级相同。  
  
## <a name="primary-operators"></a>主要运算符  
 以下是具有最高优先级的运算符。  请注意，你可以单击运算符转到包含示例的详细页面。  
  
 [x.y](../../../csharp/language-reference/operators/member-access-operator.md)：成员访问。  
  
 [x?.y](../../../csharp/language-reference/operators/null-conditional-operators.md)：null 条件成员访问。  如果左操作数为 `null`，则返回 `null`。  
 
 [x?[y]](../../../csharp/language-reference/operators/null-conditional-operators.md)：null 条件索引访问。 如果左操作数为 `null`，则返回 `null`。
 
 [f(x)](../../../csharp/language-reference/operators/invocation-operator.md)：函数调用。  
  
 [a&#91;x&#93;](../../../csharp/language-reference/operators/index-operator.md)：聚合对象索引。  
   
 [x++](../../../csharp/language-reference/operators/increment-operator.md)：后缀递增。  先返回 x 值，然后用加 1（通常加整数 1）后的 x 值更新存储位置。  
  
 [x--](../../../csharp/language-reference/operators/decrement-operator.md)：后缀递减。  先返回 x 值，然后用减 1（通常减整数 1）后的 x 值更新存储位置。  
  
 [new](../../../csharp/language-reference/keywords/new-operator.md)：类型实例化。  
  
 [typeof](../../../csharp/language-reference/keywords/typeof.md)：返回表示操作数的 System.Type 对象。  
  
 [checked](../../../csharp/language-reference/keywords/checked.md)：对整数运算启用溢出检查。  
  
 [unchecked](../../../csharp/language-reference/keywords/unchecked.md)：对整数运算禁用溢出检查。  这是默认的编译器行为。  
  
 [default(T)](../../../csharp/programming-guide/statements-expressions-operators/default-value-expressions.md)：返回类型 T 的默认值，引用类型的默认值为 `null`，数值类型的默认值为 0，结构类型成员的默认填充值为 0/`null`。  
  
 [delegate](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)：声明并返回委托实例。  
  
 [sizeof](../../../csharp/language-reference/keywords/sizeof.md)：返回类型操作数的大小（以字节为单位）。  
  
 [->](../../../csharp/language-reference/operators/dereference-operator.md)：指针取消引用与成员访问相结合。  
  
## <a name="unary-operators"></a>一元运算符  
 这些运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击运算符转到包含示例的详细页面。  
  
 [+x](../../../csharp/language-reference/operators/addition-operator.md)：返回 x 的值。  
  
 [-x](../../../csharp/language-reference/operators/subtraction-operator.md)：数值取反。  
  
 [!x](../../../csharp/language-reference/operators/logical-negation-operator.md)：逻辑取反。  
  
 [~x](../../../csharp/language-reference/operators/bitwise-complement-operator.md)：按位求补。  
  
 [++x](../../../csharp/language-reference/operators/increment-operator.md)：前缀递增。  先用加 1（通常加整数 1）后的 x 值更新存储位置，然后返回 x 值。  
  
 [--x](../../../csharp/language-reference/operators/decrement-operator.md)：前缀递减。  先用减 1（通常减整数 1）后的 x 值更新存储位置，然后返回 x 值。  
  
 [(T)x](../../../csharp/language-reference/operators/invocation-operator.md)：类型显式转换。  
  
 [await](../../../csharp/language-reference/keywords/await.md)：等待 `Task`。  
  
 [&x](../../../csharp/language-reference/operators/and-operator.md)：地址。  
  
 [*x](../../../csharp/language-reference/operators/multiplication-operator.md)：取消引用。  
  
## <a name="multiplicative-operators"></a>乘法运算符  
 这些运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击运算符转到包含示例的详细页面。  
  
 [x * y](../../../csharp/language-reference/operators/multiplication-operator.md)：乘法。  
  
 [x / y](../../../csharp/language-reference/operators/division-operator.md)：除法。  如果操作数均为整数，则结果为整数，舍去小数（例如，`-7 / 2 is -3`）。  
  
 [x % y](../../../csharp/language-reference/operators/modulus-operator.md)：取模。  如果操作数均为整数，则返回 x 除以 y 后的余数。  如果 `q = x / y` 且 `r = x % y`，则 `x = q * y + r`。  
  
## <a name="additive-operators"></a>相加运算符  
 这些运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击运算符转到包含示例的详细页面。  
  
 [x + y](../../../csharp/language-reference/operators/addition-operator.md)：加法。  
  
 [x：y](../../../csharp/language-reference/operators/subtraction-operator.md)：减法。  
  
## <a name="shift-operators"></a>移位运算符  
 这些运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击运算符转到包含示例的详细页面。  
  
 [x <\<  y](../../../csharp/language-reference/operators/left-shift-operator.md)：左移位，右侧用 0 填充。  
  
 [x >> y](../../../csharp/language-reference/operators/right-shift-operator.md)：右移位。  如果左操作数是 `int` 或 `long`，则左位数补符号位。  如果左操作数是 `uint` 或 `ulong`，则左位数补零。  
  
## <a name="relational-and-type-testing-operators"></a>关系和类型测试运算符  
 这些运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击运算符转到包含示例的详细页面。  
  
 [x \< y](../../../csharp/language-reference/operators/less-than-operator.md)：小于（如果 x 小于 y，则为 true）。  
  
 [x > y](../../../csharp/language-reference/operators/greater-than-operator.md)：大于（如果 x 大于 y，则为 true）。  
  
 [x \<= y](../../../csharp/language-reference/operators/less-than-equal-operator.md)：小于或等于。  
  
 [x >= y](../../../csharp/language-reference/operators/greater-than-equal-operator.md)：大于或等于。  
  
 [is](../../../csharp/language-reference/keywords/is.md)：类型兼容性。  如果求值后的左操作数可以转换为右操作数中指定的类型（静态类型），则返回 true。  
  
 [as](../../../csharp/language-reference/keywords/as.md)：类型转换。  返回左操作数并转换为右操作数中指定的类型（静态类型），但 `as` 返回 `null`，其中 `(T)x` 会引发异常。  
  
## <a name="equality-operators"></a>相等运算符  
 这些运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击运算符转到包含示例的详细页面。  
  
 [x == y](../../../csharp/language-reference/operators/equality-comparison-operator.md)：相等。  默认情况下，对于 `string` 以外的引用类型，此运算符返回引用相等（标识测试）。  但是，类型可以重载 `==`，因此，如果你想测试标识，最好对 `object` 使用 `ReferenceEquals` 方法。  
  
 [x != y](../../../csharp/language-reference/operators/not-equal-operator.md)：不相等。  请参阅有关 `==` 的注释。  如果某个类型重载 `==`，则它必须重载 `!=`。  
  
## <a name="logical-and-operator"></a>逻辑 AND 运算符  
 此运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击该运算符转到包含示例的详细页面。  
  
 [x & y](../../../csharp/language-reference/operators/and-operator.md)：逻辑或位 AND。  与整数类型一起使用，并且通常允许 `enum` 类型。  
  
## <a name="logical-xor-operator"></a>逻辑 XOR 运算符  
 此运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击该运算符转到包含示例的详细页面。  
  
 [x ^ y](../../../csharp/language-reference/operators/xor-operator.md)：逻辑或位 XOR。  通常可以将此运算符与整数类型和 `enum` 类型一起使用。  
  
## <a name="logical-or-operator"></a>逻辑 OR 运算符  
 此运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击该运算符转到包含示例的详细页面。  
  
 [x &#124; y](../../../csharp/language-reference/operators/or-operator.md)：逻辑或位 OR。  与整数类型一起使用，并且通常允许 `enum` 类型。  
  
## <a name="conditional-and-operator"></a>条件 AND 运算符  
 此运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击该运算符转到包含示例的详细页面。  
  
 [x && y](../../../csharp/language-reference/operators/conditional-and-operator.md)：逻辑 AND。  如果第一个操作数为 false，则 C# 不对第二个操作数求值。  
  
## <a name="conditional-or-operator"></a>条件 OR 运算符  
 此运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击该运算符转到包含示例的详细页面。  
  
 [x &#124;&#124; y](../../../csharp/language-reference/operators/conditional-or-operator.md)：逻辑 OR。  如果第一个操作数为 true，则 C# 不对第二个操作数求值。  
  
## <a name="null-coalescing-operator"></a>Null 合并运算符  
 此运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击该运算符转到包含示例的详细页面。  
  
 [x ?? y](../../../csharp/language-reference/operators/null-conditional-operator.md)：如果不为 `null`，则返回 `x`；否则返回 `y`。  
  
## <a name="conditional-operator"></a>条件运算符  
 此运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击该运算符转到包含示例的详细页面。  
  
 [t ? x : y](../../../csharp/language-reference/operators/conditional-operator.md)：如果测试 `t` 为 true，则计算并返回 `x`；否则，计算并返回 `y`。  
  
## <a name="assignment-and-lambda-operators"></a>赋值和 Lambda 运算符  
 这些运算符的优先级比下一章节高，比上一章节低。  请注意，你可以单击运算符转到包含示例的详细页面。  
  
 [x = y](../../../csharp/language-reference/operators/assignment-operator.md)：赋值。  
  
 [x += y](../../../csharp/language-reference/operators/addition-assignment-operator.md)：递增。  `x` 值加 `y` 值，结果存储在 `x` 中，并返回新值。  如果 `x` 指定 `event`，则 `y` 必须是 C# 作为事件处理程序添加的相应函数。  
  
 [x -= y](../../../csharp/language-reference/operators/subtraction-assignment-operator.md)：递减。  `x` 值减 `y` 值，结果存储在 `x` 中，并返回新值。  如果 `x` 指定 `event`，则 `y` 必须是 C# 作为事件处理程序删除的相应函数  
  
 [x *= y](../../../csharp/language-reference/operators/multiplication-assignment-operator.md)：乘法赋值。  `x` 值乘以 `y` 值，结果存储在 `x` 中，并返回新值。  
  
 [x /= y](../../../csharp/language-reference/operators/division-assignment-operator.md)：除法赋值。  `x` 值除以 `y` 值，结果存储在 `x` 中，并返回新值。  
  
 [x %= y](../../../csharp/language-reference/operators/modulus-assignment-operator.md)：取模赋值。  `x` 值除以 `y` 值，余数存储在 `x` 中，并返回新值。  
  
 [x &= y](../../../csharp/language-reference/operators/and-assignment-operator.md)：AND 赋值。  `y` 值和 `x` 值相与，结果存储在 `x` 中，并返回新值。  
  
 [x &#124;= y](../../../csharp/language-reference/operators/or-assignment-operator.md)：OR 赋值。  `y` 值和 `x` 值相或，结果存储在 `x` 中，并返回新值。  
  
 [x ^= y](../../../csharp/language-reference/operators/xor-assignment-operator.md)：XOR 赋值。  `y` 值和 `x` 值相异或，结果存储在 `x` 中，并返回新值。  
  
 [x <<= y](../../../csharp/language-reference/operators/left-shift-assignment-operator.md)：左移赋值。  将 `x` 值向左移动 `y` 位，结果存储在 `x` 中，并返回新值。  
  
 [x >>= y](../../../csharp/language-reference/operators/right-shift-assignment-operator.md)：右移赋值。  将 `x` 值向右移动 `y` 位，结果存储在 `x` 中，并返回新值。  
  
 [=>](../../../csharp/language-reference/operators/lambda-operator.md)：lambda 声明。  
  
## <a name="arithmetic-overflow"></a>算术溢出  
 算术运算符（[+](../../../csharp/language-reference/operators/addition-operator.md)、[-](../../../csharp/language-reference/operators/subtraction-operator.md)、[*](../../../csharp/language-reference/operators/multiplication-operator.md)、[/](../../../csharp/language-reference/operators/division-operator.md)）的计算结果可能会超出所涉数值类型的可取值范围。 详细信息应参考特定运算符的相关章节，而一般情况下：  
  
- 整数算术溢出或者引发 <xref:System.OverflowException>，或者放弃结果的最高有效位。 整数被零除总是引发 @System.DivideByZeroException。  

   发生整数溢出时，具体影响视执行上下文而定，上下文可为 [checked 或 unchecked](../../../csharp/language-reference/keywords/checked-and-unchecked.md)。 在 checked 上下文中引发 <xref:System.OverflowException>。 在 unchecked 上下文中，放弃结果的最高有效位并继续执行。 因此，C# 让你有机会选择处理或忽略溢出。 默认情况下，算术运算发生在 *unchecked* 上下文中。 

   除算术运算以外，整型类型之间的显式转换也会导致溢出（例如，将 [long](../../../csharp/language-reference/keywords/long.md) 显式转换成 [int](../../../csharp/language-reference/keywords/int.md)），并受到 checked 或 unchecked 执行的约束。 但是，位运算符和移位运算符永远不会导致溢出。  
   
-   浮点算术溢出或被零除从不引发异常，因为浮点类型基于 IEEE 754，因此可以表示无穷大和 NaN（非数值）。  
  
-   [小数](../../../csharp/language-reference/keywords/decimal.md)算术溢出总是引发 <xref:System.OverflowException>。 小数被零除总是引发 <xref:System.DivideByZeroException>。  
  
  
## <a name="see-also"></a>另请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [C#](../../../csharp/index.md) [可重载运算符](../../../csharp/programming-guide/statements-expressions-operators/overloadable-operators.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)

