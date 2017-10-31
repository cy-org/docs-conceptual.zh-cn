---
title: "group 子句（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- group
- group_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- group keyword [C#]
- group clause [C#]
ms.assetid: c817242e-b12c-4baa-a57e-73ee138f34d1
caps.latest.revision: 24
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
ms.openlocfilehash: afd32358a406b2797059cf2b8d85d897c8737222
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="group-clause-c-reference"></a>group 子句（C# 参考）
`group` 子句返回一个 <xref:System.Linq.IGrouping%602> 对象序列，这些对象包含零个或更多与该组的键值匹配的项。 例如，可以按照每个字符串中的第一个字母对字符串序列进行分组。 在这种情况下，第一个字母就是键，类型为 [char](../../../csharp/language-reference/keywords/char.md)，并且存储在每个 <xref:System.Linq.IGrouping%602> 对象的 `Key` 属性中。 编译器可推断键的类型。  
  
 可以用 `group` 子句结束查询表达式，如以下示例所示：  
  
 [!code-cs[cscsrefQueryKeywords#10](../../../csharp/language-reference/keywords/codesnippet/CSharp/group-clause_1.cs)]  
  
 如果要对每个组执行附加查询操作，可使用上下文关键字 [into](../../../csharp/language-reference/keywords/into.md) 指定一个临时标识符。 使用 `into` 时，必须继续编写该查询，并最终使用一个`select` 语句或另一个 `group` 子句结束该查询，如以下代码摘录所示：  
  
 [!code-cs[cscsrefQueryKeywords#11](../../../csharp/language-reference/keywords/codesnippet/CSharp/group-clause_2.cs)]  
  
 对于含有和不含 `into` 的 `group`，本主题中的“示例”部分提供有关其用法的更完整示例。  
  
## <a name="enumerating-the-results-of-a-group-query"></a>枚举查询分组的结果  
 由于 `group` 查询产生的 <xref:System.Linq.IGrouping%602> 对象实质上是一个由列表组成的列表，因此必须使用嵌套的 [foreach](../../../csharp/language-reference/keywords/foreach-in.md) 循环来访问每一组中的各个项。 外部循环用于循环访问组键，内部循环用于循环访问组本身包含的每个项。 组可能具有键，但没有元素。 下面的 `foreach` 循环执行上述代码示例中的查询：  
  
 [!code-cs[cscsrefQueryKeywords#12](../../../csharp/language-reference/keywords/codesnippet/CSharp/group-clause_3.cs)]  
  
## <a name="key-types"></a>键类型  
 组键可以是任何类型，如字符串、内置数值类型、用户定义的命名类型或匿名类型。  
  
### <a name="grouping-by-string"></a>按字符串分组  
 上述代码示例使用 `char`。 可轻松改为指定字符串键，如完整的姓氏：  
  
 [!code-cs[cscsrefQueryKeywords#13](../../../csharp/language-reference/keywords/codesnippet/CSharp/group-clause_4.cs)]  
  
### <a name="grouping-by-bool"></a>按布尔值分组  
 下面的示例演示使用布尔值作为键将结果划分成两个组。 请注意，该值由 `group` 子句中的子表达式生成。  
  
 [!code-cs[cscsrefQueryKeywords#14](../../../csharp/language-reference/keywords/codesnippet/CSharp/group-clause_5.cs)]  
  
### <a name="grouping-by-numeric-range"></a>按数值范围分组  
 下一示例使用表达式创建表示百分比范围的数值组键。 请注意，该示例使用 [let](../../../csharp/language-reference/keywords/let-clause.md) 作为方法调用结果的方便存储位置，因此无需在 `group` 子句中调用该方法两次。 另请注意，在 `group` 子句中，为了避免发生“除以零”异常，代码会进行相应检查，确保学生的平均成绩不为零。 若要详细了解如何在查询表达式中安全使用方法，请参阅[如何：在查询表达式中处理异常](../../../csharp/programming-guide/linq-query-expressions/how-to-handle-exceptions-in-query-expressions.md)。  
  
 [!code-cs[cscsrefQueryKeywords#15](../../../csharp/language-reference/keywords/codesnippet/CSharp/group-clause_6.cs)]  
  
### <a name="grouping-by-composite-keys"></a>按复合键分组  
 希望按照多个键对元素进行分组时，可使用复合键。 使用匿名类型或命名类型来存储键元素，创建复合键。 在下面的示例中，假定已经使用名为 `surname` 和 `city` 的两个成员声明了类 `Person`。 `group` 子句会为每组姓氏和城市相同的人员创建一个单独的组。  
  
```csharp  
group person by new {name = person.surname, city = person.city};  
```  
  
 如果必须将查询变量传递给其他方法，请使用命名类型。 使用键的自动实现的属性创建一个特殊类，然后替代 <xref:System.Object.Equals%2A> 和 <xref:System.Object.GetHashCode%2A> 方法。 还可以使用结构，在此情况下，并不严格要求替代这些方法。 有关详细信息，请参阅[如何：使用自动实现的属性实现轻量类](../../../csharp/programming-guide/classes-and-structs/how-to-implement-a-lightweight-class-with-auto-implemented-properties.md)和[如何：查询目录树中的重复文件 (LINQ)](../../programming-guide/concepts/linq/how-to-query-for-duplicate-files-in-a-directory-tree-linq.md)。 后一个主题包含的代码示例演示了如何将复合键与命名类型结合使用。  
  
## <a name="example"></a>示例  
 下面的示例演示在没有向组应用附加查询逻辑时，将源数据按顺序放入组中的标准模式。 这称为不带延续的分组。 字符串数组中的元素按照它们的首字母进行分组。 查询的结果是 <xref:System.Linq.IGrouping%602> 类型（包含一个 `char` 类型的公共 `Key` 属性）和一个 <xref:System.Collections.Generic.IEnumerable%601> 集合（在分组中包含每个项）。  
  
 `group` 子句的结果是由序列组成的序列。 因此，若要访问返回的每个组中的单个元素，请在循环访问组键的循环内使用嵌套的 `foreach` 循环，如以下示例所示。  
  
 [!code-cs[cscsrefQueryKeywords#16](../../../csharp/language-reference/keywords/codesnippet/CSharp/group-clause_7.cs)]  
  
## <a name="example"></a>示例  
 此示例演示在创建组之后，如何使用通过 `into` 实现的延续对这些组执行附加逻辑。 有关详细信息，请参阅 [into](../../../csharp/language-reference/keywords/into.md)。 下面的示例查询每个组，仅选择键值为元音的元素。  
  
 [!code-cs[cscsrefQueryKeywords#17](../../../csharp/language-reference/keywords/codesnippet/CSharp/group-clause_8.cs)]  
  
## <a name="remarks"></a>备注  
 在编译时，`group` 子句转换为对 <xref:System.Linq.Enumerable.GroupBy%2A> 方法的调用。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Linq.IGrouping%602>   
 <xref:System.Linq.Enumerable.GroupBy%2A>   
 <xref:System.Linq.Enumerable.ThenBy%2A>   
 <xref:System.Linq.Enumerable.ThenByDescending%2A>   
 [查询关键字 (LINQ)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [如何：创建嵌套组](../../../csharp/programming-guide/linq-query-expressions/how-to-create-a-nested-group.md)   
 [如何：对查询结果进行分组](../../../csharp/programming-guide/linq-query-expressions/how-to-group-query-results.md)   
 [如何：对分组操作执行子查询](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-a-subquery-on-a-grouping-operation.md)

