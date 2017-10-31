---
title: "enum（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- enum
- enum_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- enum keyword [C#]
ms.assetid: bbeb9a0f-e9b3-41ab-b0a6-c41b1a08974c
caps.latest.revision: 36
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
ms.openlocfilehash: fbadbcf92a6ac8ed46c3e81fa9eda1ceac8f6631
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="enum-c-reference"></a>enum（C# 参考）
`enum` 关键字用于声明枚举，一种包含一组被称为枚举数列表的已命名常数的不同类型。  
  
 通常最好是直接在命名空间内定义枚举，以便命名空间中的所有类都可以同样方便地访问它。 但是，也可能会在类或结构中嵌套枚举。  
  
 默认情况下，第一个枚举数具有值 0，并且每个连续枚举数的值将增加 1。 例如，在以下枚举中， `Sat` 的值为 `0`， `Sun` 的值为 `1`， `Mon` 的值为 `2`，依次类推。  
  
```  
enum Days {Sat, Sun, Mon, Tue, Wed, Thu, Fri};  
```  
  
 枚举数可以使用初始值设定项来替代默认值，如下面的示例中所示。  
  
```  
enum Days {Sat=1, Sun, Mon, Tue, Wed, Thu, Fri};  
```  
  
 在此枚举中，强制元素的序列从 `1` 开始，而不是 `0`。 但建议包括一个值为 0 的常量。 有关详细信息，请参阅[枚举类型](../../../csharp/programming-guide/enumeration-types.md)。  
  
 每个枚举类型都有一个基础类型，该基础类型可以是除 [char](../../../csharp/language-reference/keywords/char.md) 外的任何整型类型。 枚举元素的默认基础类型是 [int](../../../csharp/language-reference/keywords/int.md)。若要声明另一整型的枚举（如 [byte](../../../csharp/language-reference/keywords/byte.md)），则请在后跟该类型的标识符后使用冒号，如以下示例所示。  
  
```  
enum Days : byte {Sat=1, Sun, Mon, Tue, Wed, Thu, Fri};  
```  
  
 枚举的已批准类型有 `byte`、 [sbyte](../../../csharp/language-reference/keywords/sbyte.md)、 [short](../../../csharp/language-reference/keywords/short.md)、 [ushort](../../../csharp/language-reference/keywords/ushort.md)、 [int](../../../csharp/language-reference/keywords/int.md)、 [uint](../../../csharp/language-reference/keywords/uint.md)、 [long](../../../csharp/language-reference/keywords/long.md)或 [ulong](../../../csharp/language-reference/keywords/ulong.md)。  
  
 类型 `Days` 的变量可在基本类型范围内分配到任何值；该值不限于已命名常数。  
  
 `enum E` 的默认值是由表达式 `(E)0`生成的值。  
  
> [!NOTE]
>  枚举数名称中不能含有空格。  
  
 基础类型指定为每个枚举数分配多少存储空间。 但要将 `enum` 类型转换为整型，则必须使用显示转换。 例如，以下语句通过使用转换将 `Sun` 转换为 [，从而将枚举数](../../../csharp/language-reference/keywords/int.md) 赋值为 `enum` int `int`类型的变量。  
  
```  
int x = (int)Days.Sun;  
```  
  
 当你将 <xref:System.FlagsAttribute?displayProperty=nameWithType> 应用到包含可与按位 `OR` 运算组合的元素的枚举中时，该特性与某些工具一起使用时会影响 `enum` 的行为。 当你使用工具（如 <xref:System.Console> 类方法和表达式计算器）时，你可以注意到这些更改。 （请参阅第三个示例。）  
  
## <a name="robust-programming"></a>可靠编程  
 正如任何常量一样，对枚举的各项值的所有引用在编译时都会转换为数字参数。 这可能会造成如[常量](../../../csharp/programming-guide/classes-and-structs/constants.md)中所述的潜在版本问题。  
  
 将其他值分配到枚举的新版本，或者在新版本中更改枚举成员的值，会导致出现相关源代码问题。 通常在 [switch](../../../csharp/language-reference/keywords/switch.md) 语句中使用枚举值。 如果已将其他元素添加到 `enum` 类型，则 switch 语句的默认部分可被意外地选中。  
  
 如果其他开发人员使用你的代码，则在将新元素添加到任何 `enum` 类型时应提供有关他们的代码应该如何响应的准则。  
  
## <a name="example"></a>示例  
 在下面的示例中，已声明枚举 `Days`。 已将两个枚举数显式转换为整数，并赋值为整数变量。  
  
 [!code-cs[csrefKeywordsTypes#10](../../../csharp/language-reference/keywords/codesnippet/CSharp/enum_1.cs)]  
  
## <a name="example"></a>示例  
 以下示例中，使用基类型选项来声明其成员是 `enum` 类型的 `long`。 请注意，即使该枚举的基础类型是 `long`，仍然需通过使用转换将枚举成员显式转换为类型 `long` 。  
  
 [!code-cs[csrefKeywordsTypes#11](../../../csharp/language-reference/keywords/codesnippet/CSharp/enum_2.cs)]  
  
## <a name="example"></a>示例  
 下面的代码示例说明了 <xref:System.FlagsAttribute?displayProperty=nameWithType> 声明中 `enum` 特性的使用和作用。  
  
 [!code-cs[csrefKeywordsTypes#12](../../../csharp/language-reference/keywords/codesnippet/CSharp/enum_3.cs)]  
  
## <a name="comments"></a>注释  
 如果删除 `Flags`，则示例将显示以下值：  
  
 `5`  
  
 `5`  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [枚举类型](../../../csharp/programming-guide/enumeration-types.md)   
 [C# 关键字](../../../csharp/language-reference/keywords/index.md)   
 [整型类型表](../../../csharp/language-reference/keywords/integral-types-table.md)   
 [内置类型表](../../../csharp/language-reference/keywords/built-in-types-table.md)   
 [隐式数值转换表](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)   
 [显式数值转换表](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)

