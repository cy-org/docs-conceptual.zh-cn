---
title: "join 子句（C# 参考）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- join
- join_CSharpKeyword
dev_langs:
- CSharp
helpviewer_keywords:
- join clause [C#]
- join keyword [C#]
ms.assetid: 76e9df84-092c-41a6-9537-c3f1cbd7f0fb
caps.latest.revision: 29
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
ms.openlocfilehash: 3368ba14101eda38ed8e3ee2bdc81bcab74a9b82
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="join-clause-c-reference"></a>join 子句（C# 参考）
`join` 子句可用于将来自不同源序列并且在对象模型中没有直接关系的元素相关联。 唯一的要求是每个源中的元素需要共享某个可以进行比较以判断是否相等的值。 例如，食品经销商可能拥有某种产品的供应商列表以及买主列表。 例如，可以使用 `join` 子句创建该产品同一指定地区供应商和买主的列表。  
  
 `join` 子句将 2 个源序列作为输入。 每个序列中的元素都必须是可以与其他序列中的相应属性进行比较的属性，或者包含一个这样的属性。 `join` 子句使用特殊 `equals` 关键字比较指定的键是否相等。 `join` 子句执行的所有联接都是同等联接。 `join` 子句的输出形式取决于执行的联接的具体类型。 以下是 3 种最常见的联接类型：  
  
-   内部联接  
  
-   分组联接  
  
-   左外部联接  
  
## <a name="inner-join"></a>内部联接  
 以下示例演示了一个简单的内部同等联接。 此查询生成一个“产品名称/类别”对平面序列。 同一类别字符串将出现在多个元素中。 如果 `categories` 中的某个元素不具有匹配的 `products`，则该类别不会出现在结果中。  
  
 [!code-cs[cscsrefQueryKeywords#24](../../../csharp/language-reference/keywords/codesnippet/CSharp/join-clause_1.cs)]  
  
 有关详细信息，请参阅[如何：执行内部联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md)。  
  
## <a name="group-join"></a>Group Join  
 含有 `into` 表达式的 `join` 子句称为分组联接。  
  
 [!code-cs[cscsrefQueryKeywords#25](../../../csharp/language-reference/keywords/codesnippet/CSharp/join-clause_2.cs)]  
  
 分组联接会生成分层的结果序列，该序列将左侧源序列中的元素与右侧源序列中的一个或多个匹配元素相关联。 分组联接没有等效的关系术语；它本质上是一个对象数组序列。  
  
 如果在右侧源序列中找不到与左侧源中的元素相匹配的元素，则 `join` 子句会为该项生成一个空数组。 因此，分组联接基本上仍然是一种内部同等联接，区别在于分组联接将结果序列组织为多个组。  
  
 如果只选择分组联接的结果，则可访问各项，但无法识别结果所匹配的项。 因此，通常更为有用的做法是：选择分组联接的结果并将其放入一个也包含该项名的新类型中，如上例所示。  
  
 当然，还可以将分组联接的结果用作其他子查询的生成器：  
  
 [!code-cs[cscsrefQueryKeywords#26](../../../csharp/language-reference/keywords/codesnippet/CSharp/join-clause_3.cs)]  
  
 有关详细信息，请参阅[如何：执行分组联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-grouped-joins.md)。  
  
## <a name="left-outer-join"></a>左外部联接  
 在左外部联接中，将返回左侧源序列中的所有元素，即使右侧序列中没有其匹配元素也是如此。 若要在 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 中执行左外部联接，请结合使用 `DefaultIfEmpty` 方法与分组联接，指定要在某个左侧元素不具有匹配元素时生成的默认右侧元素。 可以使用 `null` 作为任何引用类型的默认值，也可以指定用户定义的默认类型。 以下示例演示了用户定义的默认类型：  
  
 [!code-cs[cscsrefQueryKeywords#27](../../../csharp/language-reference/keywords/codesnippet/CSharp/join-clause_4.cs)]  
  
 有关详细信息，请参阅[如何：执行左外部联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-left-outer-joins.md)。  
  
## <a name="the-equals-operator"></a>等于运算符  
 `join` 子句执行同等联接。 换言之，只能基于 2 个项之间的相等关系进行匹配。 不支持其他类型的比较，例如“大于”或“不等于”。 为了表明所有联接都是同等联接，`join` 子句使用 `equals` 关键字而不是 `==` 运算符。 `equals` 关键字只能在 `join` 子句中使用，并且其与 `==` 运算符之间存在一个重要差别。 对于 `equals`，左键使用外部源序列，而右键使用内部源序列。 外部源仅在 `equals` 的左侧位于范围内，而内部源序列仅在其右侧位于范围内。  
  
## <a name="non-equijoins"></a>非同等联接  
 通过使用多个 `from` 子句将新序列单独引入查询，可以执行非同等联接、交叉联接和其他自定义联接操作。 有关详细信息，请参阅[如何：执行自定义联接操作](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-custom-join-operations.md)。  
  
## <a name="joins-on-object-collections-vs-relational-tables"></a>对象集合联接与关系表  
 在[!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询表达式中，联接操作是在对象集合上执行的。 不能使用与 2 个关系表完全相同的方式“联接”对象集合。 在 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 中，仅当 2 个源序列没有通过任何关系相互联系时，才需要使用显式 `join` 子句。 使用 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 时，外键表在对象模型中表示为主表的属性。 例如，在 Northwind 数据库中，Customer 表与 Orders 表之间具有外键关系。 将这两个表映射到对象模型时，Customer 类具有一个 Orders 属性，其中包含与该 Customer 相关联的 Orders 集合。 实际上，已经为你执行了联接。  
  
 若要深入了解如何在 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 的上下文中跨相关表执行查询，请参阅[如何：映射数据库关系](../../../framework/data/adonet/sql/linq/how-to-map-database-relationships.md)。  
  
## <a name="composite-keys"></a>组合键  
 可通过使用组合键测试多个值是否相等。 有关详细信息，请参阅[如何：使用组合键进行联接](../../../csharp/programming-guide/linq-query-expressions/how-to-join-by-using-composite-keys.md)。 还可以在 `group` 子句中使用组合键。  
  
## <a name="example"></a>示例  
 以下示例比较了使用相同的匹配键对相同数据源执行内部联接、分组联接和左外部联接的结果。 这些示例中添加了一些额外的代码，以便在控制台显示中阐明结果。  
  
 [!code-cs[cscsrefQueryKeywords#23](../../../csharp/language-reference/keywords/codesnippet/CSharp/join-clause_5.cs)]  
  
## <a name="remarks"></a>备注  
 后面未跟 `into` 的 `join` 子句转换为 <xref:System.Linq.Enumerable.Join%2A> 方法调用。 后面跟 `into` 的 `join` 子句转换为 <xref:System.Linq.Enumerable.GroupJoin%2A> 方法调用。  
  
## <a name="see-also"></a>另请参阅  
 [查询关键字 (LINQ)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [LINQ 查询表达式](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [联接运算](http://msdn.microsoft.com/library/442d176d-028c-4beb-8d22-407d4ef89107)   
 [group 子句](../../../csharp/language-reference/keywords/group-clause.md)   
 [如何：执行左外部联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-left-outer-joins.md)   
 [如何：执行内部联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-inner-joins.md)   
 [如何：执行分组联接](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-grouped-joins.md)   
 [如何：对 Join 子句的结果进行排序](../../../csharp/programming-guide/linq-query-expressions/how-to-order-the-results-of-a-join-clause.md)   
 [如何：使用组合键进行联接](../../../csharp/programming-guide/linq-query-expressions/how-to-join-by-using-composite-keys.md)   
 [如何：安装示例数据库](http://msdn.microsoft.com/library/ed1291f6-604c-4972-ae22-0345c6dea12e)

