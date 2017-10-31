---
title: "基本 LINQ 查询操作 (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- orderby clause [LINQ in C#]
- ordering data [LINQ in C#]
- selecting data [LINQ in C#]
- queries [LINQ in C#], basic operations
- grouping data [LINQ in C#]
- data sources [LINQ in C#]
- sorting data [LINQ in C#]
- projections [LINQ in C#]
- filtering data [LINQ in C#]
- joining data [LINQ in C#]
- select clause [LINQ in C#]
- LINQ [C#], basic query operations
- join clause [LINQ in C#]
- group clause [LINQ in C#]
ms.assetid: a7ea3421-1cf4-4df7-832a-aa22fe6379e9
caps.latest.revision: 39
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
ms.openlocfilehash: e5dbebb7950678a0f40ec774d23b42dfe89cff49
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="basic-linq-query-operations-c"></a>基本 LINQ 查询操作 (C#)
本主题简要介绍了 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询表达式和一些在查询中执行的典型操作。 下面各主题中提供了更具体的信息：  
  
 [LINQ 查询表达式](../../../../csharp/programming-guide/linq-query-expressions/index.md)  
  
 [标准查询运算符概述 (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)  
  
 [演练：用 C# 编写查询](../../../../csharp/programming-guide/concepts/linq/walkthrough-writing-queries-linq.md)  
  
> [!NOTE]
>  如果你已熟悉查询语言（如 SQL 或 XQuery），则可以跳过本主题的大部分内容。 请参阅下一节中的“`from` 子句”部分，了解 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询表达式中的子句顺序。  
  
## <a name="obtaining-a-data-source"></a>获取数据源  
 在 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询中，第一步是指定数据源。 和大多数编程语言相同，在使用 C# 时也必须先声明变量，然后才能使用它。 在 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询中，先使用 `from` 子句引入数据源 (`customers`) 和范围变量 (`cust`)。  
  
 [!code-cs[csLINQGettingStarted#23](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_1.cs)]  
  
 范围变量就像 `foreach` 循环中的迭代变量，但查询表达式中不会真正发生迭代。 当执行查询时，范围变量将充当对 `customers` 中每个连续的元素的引用。 由于编译器可以推断 `cust` 的类型，因此无需显式指定它。 可通过 `let` 子句引入其他范围变量。 有关详细信息，请参阅 [let 子句](../../../../csharp/language-reference/keywords/let-clause.md)。  
  
> [!NOTE]
>  对于非泛型数据源（例如 <xref:System.Collections.ArrayList>），必须显式键入范围变量。 有关详细信息，请参阅[如何：使用 LINQ (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md) 和 [From 子句](../../../../csharp/language-reference/keywords/from-clause.md)查询 ArrayList。  
  
## <a name="filtering"></a>筛选  
 或许，最常见的查询操作是以布尔表达式的形式应用筛选器。 筛选器使查询仅返回表达式为 true 的元素。 将通过使用 `where` 子句生成结果。 筛选器实际指定要从源序列排除哪些元素。 在下列示例中，仅返回地址位于“London”的 `customers`。  
  
 [!code-cs[csLINQGettingStarted#24](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_2.cs)]  
  
 可使用熟悉的 C# 逻辑 `AND` 和 `OR` 运算符，在 `where` 子句中根据需要应用尽可能多的筛选器表达式。 例如，若要仅返回来自“London”的客户 `AND` 该客户名称为“Devon”，可编写以下代码：  
  
 [!code-cs[csLINQGettingStarted#25](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_3.cs)]  
  
 要返回来自 London 或 Paris 的客户，可编写以下代码：  
  
 [!code-cs[csLINQGettingStarted#26](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_4.cs)]  
  
 有关详细信息，请参阅 [where 子句](../../../../csharp/language-reference/keywords/where-clause.md)。  
  
## <a name="ordering"></a>订购  
 对返回的数据进行排序通常很方便。 `orderby` 子句根据要排序类型的默认比较器，对返回序列中的元素排序。 例如，基于 `Name` 属性，可将下列查询扩展为对结果排序。 由于 `Name` 是字符串，默认比较器将按字母顺序从 A 到 Z 进行排序。  
  
 [!code-cs[csLINQGettingStarted#27](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_5.cs)]  
  
 要对结果进行从 Z 到 A 的逆序排序，请使用 `orderby…descending` 子句。  
  
 有关详细信息，请参阅 [orderby 子句](../../../../csharp/language-reference/keywords/orderby-clause.md)。  
  
## <a name="grouping"></a>分组  
 `group` 子句用于对根据您指定的键所获得的结果进行分组。 例如，可指定按 `City` 对结果进行分组，使来自 London 或 Paris 的所有客户位于单独的组内。 在这种情况下，`cust.City` 是键。  
  
 [!code-cs[csLINQGettingStarted#28](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_6.cs)]  
  
 使用 `group` 子句结束查询时，结果将以列表的形式列出。 列表中的每个元素都是具有 `Key` 成员的对象，列表中的元素根据该键被分组。 在循环访问生成组序列的查询时，必须使用嵌套 `foreach` 循环。 外层循环循环访问每个组，内层循环循环访问每个组的成员。  
  
 如果必须引用某个组操作的结果，可使用 `into` 关键字创建能被进一步查询的标识符。 下列查询仅返回包含两个以上客户的组：  
  
 [!code-cs[csLINQGettingStarted#29](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_7.cs)]  
  
 有关详细信息，请参阅 [group 子句](../../../../csharp/language-reference/keywords/group-clause.md)。  
  
## <a name="joining"></a>联接  
 联接操作在不同序列间创建关联，这些序列在数据源中未被显式模块化。 例如，可通过执行联接来查找所有位置相同的客户和分销商。 在 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 中，`join` 子句始终作用于对象集合，而非直接作用于数据库表。  
  
 [!code-cs[csLINQGettingStarted#36](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/basic-linq-query-operations_8.cs)]  
  
 在 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 中，不必像在 SQL 中那样频繁使用 `join`，因为 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 中的外键在对象模型中表示为包含项集合的属性。 例如 `Customer` 对象包含 `Order` 对象的集合。 不必执行联接，只需使用点表示法访问订单：  
  
```  
from order in Customer.Orders...  
```  
  
 有关详细信息，请参阅 [join 子句](../../../../csharp/language-reference/keywords/join-clause.md)。  
  
## <a name="selecting-projections"></a>选择（投影）  
 `select` 子句生成查询结果并指定每个返回的元素的“形状”或类型。 例如，可以指定结果包含的是整个 `Customer` 对象、仅一个成员、成员的子集，还是某个基于计算或新对象创建的完全不同的结果类型。 当 `select` 子句生成除源元素副本以外的内容时，该操作称为投影。 使用投影转换数据是 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询表达式的一种强大功能。 有关详细信息，请参阅[使用 LINQ (C#)](../../../../csharp/programming-guide/concepts/linq/data-transformations-with-linq.md) 和 [select 子句](../../../../csharp/language-reference/keywords/select-clause.md)进行数据转换。  
  
## <a name="see-also"></a>另请参阅  
 [C# 中的 LINQ 入门](../../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [LINQ 查询表达式](../../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [演练：用 C# 编写查询](../../../../csharp/programming-guide/concepts/linq/walkthrough-writing-queries-linq.md)   
 [查询关键字 (LINQ)](../../../../csharp/language-reference/keywords/query-keywords.md)   
 [匿名类型](../../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)

