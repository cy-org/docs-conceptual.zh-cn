---
title: "使用可以为 null 的类型（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- nullable types [C#], about nullable types
ms.assetid: 0bacbe72-ce15-4b14-83e1-9c14e6380c28
caps.latest.revision: 31
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
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 0721d9f60abc4e158135d6b050953b3e63ab8cb5
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="using-nullable-types-c-programming-guide"></a>使用可以为 null 的类型（C# 编程指南）
可以为 null 的类型可表示一个基础类型的所有值，还可以再表示一个 [null](../../../csharp/language-reference/keywords/null.md) 值。 可通过以下两种方式之一声明可为 null 的类型：  
  
 `System.Nullable<T> variable`  
  
 - 或 -  
  
 `T? variable`  
  
 `T` 是可以为 null 的类型的基础类型。 `T` 可以是包括 `struct` 在内的任意值类型；它不能是引用类型。  
  
 有关可为 null 的类型的使用示例，可思考一个普通布尔变量如何能够具有两个值：true 和 false。 没有值表示“未定义”的意思。 在许多编程应用程序中，尤其是数据库交互中，变量可能处于未定义的状态。 例如，数据库中的字段可能包含值 true 或 false，但它也可能根本不包含任何值。 同样，可以将引用类型设置为 `null` 以指示它们未初始化。  
  
 这种不一致可能会导致额外的编程工作，包括使用更多变量来存储状态信息以及使用特殊值等。 通过使用可为 null 的类型修饰符，C# 能够创建指示未定义值的值类型变量。  
  
## <a name="examples-of-nullable-types"></a>可为 null 的类型的示例  
 任何值类型都可用作可为 null 的类型的基础。 例如：  
  
 [!code-cs[csProgGuideTypes#4](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_1.cs)]  
  
## <a name="the-members-of-nullable-types"></a>可为 null 的类型的成员  
 可以为 null 的类型的每个实例都有两个公共只读属性：  
  
-   `HasValue`  
  
     `HasValue` 的类型为 `bool`。 如果该变量包含非 null 值，则将其设置为 `true`。  
  
-   `Value`  
  
     `Value` 的类型与基础类型相同。 如果 `HasValue` 为 `true`，则 `Value` 包含有意义的值。 如果 `HasValue` 是 `false`，则访问 `Value` 将引发 <xref:System.InvalidOperationException>。  
  
 在此示例中，`HasValue` 成员用于在显示变量之前测试变量是否包含值。  
  
 [!code-cs[csProgGuideTypes#5](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_2.cs)]  
  
 也可按以下示例所示进行值测试：  
  
 [!code-cs[csProgGuideTypes#6](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_3.cs)]  
  
## <a name="explicit-conversions"></a>显式转换  
 可通过显式转换或使用 `Value` 属性将可为 null 的类型转换为常规类型。 例如：  
  
 [!code-cs[csProgGuideTypes#7](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_4.cs)]  
  
 如果定义了（用户定义的）两种数据类型之间的转换，还可将同一转换用于这些数据类型的可为 null 的版本。  
  
## <a name="implicit-conversions"></a>隐式转换  
 可以使用 `null` 关键字将可为 null 的类型的变量设置为 null，如以下示例所示：  
  
 [!code-cs[csProgGuideTypes#8](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_5.cs)]  
  
 普通类型到可为 null 的类型的转换是隐式的。  
  
 [!code-cs[csProgGuideTypes#9](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_6.cs)]  
  
## <a name="operators"></a>运算符  
 可为 null 的类型还可使用预定义的一元运算符和二元运算符以及任何用于值类型的用户定义的运算符。 如果操作数为 null，则这些运算符将产生一个 null 值；否则，运算符使用所包含的值来计算结果。 例如：  
  
 [!code-cs[csProgGuideTypes#10](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_7.cs)]  
  
 将可为 null 的类型进行比较时，如果其中一个可以为 null 的类型的值为 null，而另一个为非 null，则除 `!=`（不等于）外，所有比较的计算结果均为 `false`。 请勿假定由于某个特定的比较返回 `false`，则相反的情况下便会返回 `true`。 在下面的示例中，10 不大于、小于或等于 null。 仅 `num1 != num2` 的计算结果为 `true`。  
  
 [!code-cs[csProgGuideTypes#11](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_8.cs)]  
  
 对两个均为 null 的可为 null 的类型进行相等比较，其计算结果为 `true`。  
  
## <a name="the--operator"></a>?? 运算符  
 `??` 运算符定义一个默认值，若将一个可为 null 的类型赋给不可为 null 的类型，则会返回该值。  
  
 [!code-cs[csProgGuideTypes#12](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_9.cs)]  
  
 此运算符还可与多个可为 null 的类型一起使用。 例如：  
  
 [!code-cs[csProgGuideTypes#13](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-nullable-types_10.cs)]  
  
## <a name="the-bool-type"></a>bool? 类型  
 可以为 null 的类型 `bool?` 可包含三个不同的值：[true](../../../csharp/language-reference/keywords/true.md)、[false](../../../csharp/language-reference/keywords/false.md) 和 [null](../../../csharp/language-reference/keywords/null.md)。 若要了解如何将 bool? 转换为 bool，请参阅[如何：安全地将 bool? 转换为 bool](../../../csharp/programming-guide/nullable-types/how-to-safely-cast-from-bool-to-bool.md)。  
  
 可为 null 的布尔值类似于在 SQL 中使用的布尔值变量类型。 为确保 `&` 和 `|` 运算符产生的结果与 SQL 中具有三个值的布尔值类型一致，在此提供以下预定义运算符：  
  
 `bool? operator &(bool? x, bool? y)`  
  
 `bool? operator |(bool? x, bool? y)`  
  
 下表列出了这些运算符的结果：  
  
|X|y|x 和 y|x&#124;y|  
|-------|-------|---------|--------------|  
|true|true|true|true|  
|true|false|false|true|  
|true|null|null|true|  
|false|true|false|true|  
|false|false|false|false|  
|false|null|false|null|  
|null|true|null|true|  
|null|false|false|null|  
|null|null|null|null|  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)   
 [装箱可以为 null 的类型](../../../csharp/programming-guide/nullable-types/boxing-nullable-types.md)   
 [可以为 null 的值类型](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)

