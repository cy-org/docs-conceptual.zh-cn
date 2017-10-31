---
title: "如何：比较字符串（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- strings [C#], comparison
- comparing strings [C#]
ms.assetid: e1268e28-ee98-4695-98e9-92280f1c33c0
caps.latest.revision: 23
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 70bd8f52971115a36626961c2c605f2f93c1ae6b
ms.openlocfilehash: ed376960e0b3bb793b377cc8fac2fdefa030dcc0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/19/2017

---
# <a name="how-to-compare-strings-c-programming-guide"></a>如何：比较字符串（C# 编程指南）

比较字符串时，产生的结果会是一个字符串大于或小于另一个字符串，或者两个字符串相等。 根据执行的是序号比较还是区分区域性比较，确定结果时依据的规则会有所不同。 请务必对特定任务使用正确的比较类型。

 需要对两个字符串的值进行比较或排序而不需要考虑语言惯例时，请使用基本的序号比较。 基本的序号比较 (`System.StringComparison.Ordinal`) 区分大小写，这意味着两个字符串的字符必须完全匹配：“and”不等于“And”或“AND”。 常用的变量有 `System.StringComparison.OrdinalIgnoreCase`，其可匹配“and”、“And”和“AND”。 `StringComparison.OrdinalIgnoreCase` 常用于比较文件名、路径名和网络路径，以及其值不随用户计算机的区域设置的更改而变化的任何其他字符串。 有关详细信息，请参阅<xref:System.StringComparison?displayProperty=fullName>。

 区分区域性比较通常用于对最终用户输入的字符串进行比较和排序，因为这些字符串的字符和排序约定可能因用户计算机的区域设置而异。 即使是包含相同字符的字符串，也可能因当前线程的区域性而具有不同的排序。

> [!NOTE]
> 比较字符串时，使用的方法应显式指定要执行的比较类型。 这可增强代码的可维护性和可读性。 应尽可能使用具有 <xref:System.StringComparison> 枚举参数的 <xref:System.String?displayProperty=fullName> 和 <xref:System.Array?displayProperty=fullName> 类的方法重载，以便可以指定要执行的比较类型。 比较字符串时，最好避免使用 `==` 和 `!=` 运算符。 此外，还应避免使用 <xref:System.String.CompareTo%2A?displayProperty=fullName> 实例方法，因为这些重载没有 <xref:System.StringComparison>。

## <a name="example"></a>示例

下例演示了如何正确比较其值不随用户计算机的区域设置的改变而变化的字符串。 此外，此示例还演示了 C# 中的字符串集中功能。 如果程序声明了 2 个或多个相同的字符串变量，则编译器会将其存储在同一位置。 通过调用 <xref:System.Object.ReferenceEquals%2A> 方法，可以看到这两个字符串实际上引用的是内存中的同一对象。 使用 <xref:System.String.Copy%2A?displayProperty=fullName> 方法可避免集中，如下面的示例所示。

[!code-csharp[csProgGuideStrings#11](../../../../samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStrings/CS/Strings.cs#11)]

## <a name="example"></a>示例

下面的示例演示了如何通过首选方式比较字符串，该首选方式使用具有 <xref:System.StringComparison> 枚举的 <xref:System.String?displayProperty=fullName> 方法。 请注意，此处没有使用 <xref:System.String.CompareTo%2A?displayProperty=fullName> 实例方法，因为这些重载没有 <xref:System.StringComparison>。

[!code-csharp[csProgGuideStrings#31](../../../../samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStrings/CS/Strings.cs#31)]

## <a name="example"></a>示例

下面的示例演示了如何使用具有 <xref:System.StringComparer?displayProperty=fullName> 参数的静态 <xref:System.Array> 方法以区分区域性的方式对数组中的字符串进行排序和搜索。

[!code-csharp[csProgGuideStrings#32](../../../../samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStrings/CS/Strings.cs#32)]

元素或键的类型为 `string` 时，<xref:System.Collections.Hashtable?displayProperty=fullName>、<xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> 和 <xref:System.Collections.Generic.List%601?displayProperty=fullName> 等集合类的构造函数具有 <xref:System.StringComparer?displayProperty=fullName> 参数。 通常，应尽可能使用这些构造函数，并指定 `Ordinal` 或 `OrdinalIgnoreCase`。

## <a name="see-also"></a>请参阅
 <xref:System.Globalization.CultureInfo?displayProperty=fullName>   
 <xref:System.StringComparer?displayProperty=fullName>   
 [字符串](../../../csharp/programming-guide/strings/index.md)   
 [比较字符串](../../../standard/base-types/comparing.md)   
 [对应用程序进行全球化和本地化](/visualstudio/ide/globalizing-and-localizing-applications)
