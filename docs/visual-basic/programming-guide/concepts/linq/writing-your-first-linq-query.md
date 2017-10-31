---
title: "编写第一个 LINQ 查询 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- queries [LINQ in Visual Basic], writing
- LINQ queries [Visual Basic]
- LINQ [Visual Basic], writing queries
ms.assetid: 4affb732-3e9b-4479-aa31-1f9bd8183cbe
caps.latest.revision: 56
author: stevehoag
ms.author: shoag
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 48f1c5e15654580b6e4d060860a0d7001af5e2ef
ms.lasthandoff: 03/13/2017

---
# <a name="writing-your-first-linq-query-visual-basic"></a>编写第一个 LINQ 查询 (Visual Basic)
一个*查询*是从数据源检索数据的表达式。 查询用专用的查询语言表示。 随着时间推移，不同的语言已开发为不同类型的数据源，例如，用于关系数据库的 SQL 和用于 XML 的 XQuery。 这样，就需要为应用程序开发人员若要了解有关每种类型的数据源或数据格式，支持新的查询语言。  
  
 [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)]通过提供跨各种数据源和格式处理数据的一致模型，简化了这种情况。 在[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查询，则会始终处理的对象。 使用相同的基本编码模式来查询和将 XML 文档中的数据、 SQL 数据库、 ADO.NET 数据集和实体、.NET Framework 集合和任何其他源或格式转换为其[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]提供程序。 本文档介绍的三个阶段创建和使用基本[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查询。  
  
## <a name="three-stages-of-a-query-operation"></a>查询操作的三个阶段  
 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查询操作包含三个操作︰  
  
1.  获取数据源。  
  
2.  创建查询。  
  
3.  执行查询。  
  
 在[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]，执行的查询是不同于创建查询。 不要只需通过创建一个查询中检索任何数据。 此时将在本主题稍后部分详细讨论。  
  
 下面的示例说明了查询操作的三个部分。 该示例出于演示目的，作为方便的数据源使用整数的数组。 但是，相同的概念也适用于其他数据源。  
  
> [!NOTE]
>  在[编译页，项目设计器 (Visual Basic 中)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic)，确保**Option infer**设置为**上**。  
  
 [!code-vb[VbLINQFirstQuery #&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_1.vb)]  
  
 输出：  
  
 `0 2 4 6`  
  
## <a name="the-data-source"></a>数据源  
 由于前面的示例中的数据源是一个数组，它隐式支持泛型<xref:System.Collections.Generic.IEnumerable%601>接口。</xref:System.Collections.Generic.IEnumerable%601> 这一事实，您可以作为数据源使用数组[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查询。 类型支持<xref:System.Collections.Generic.IEnumerable%601>或派生的接口如通用<xref:System.Linq.IQueryable%601>称为*可查询类型*。</xref:System.Linq.IQueryable%601> </xref:System.Collections.Generic.IEnumerable%601>  
  
 作为隐式可查询的类型，该数组需要进行任何修改或特殊处理，就可以用作[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]数据源。 这同样适用于支持的所有集合类型<xref:System.Collections.Generic.IEnumerable%601>，包括泛型<xref:System.Collections.Generic.List%601>， <xref:System.Collections.Generic.Dictionary%602>，和.NET Framework 类库中的其他类。</xref:System.Collections.Generic.Dictionary%602> </xref:System.Collections.Generic.List%601> </xref:System.Collections.Generic.IEnumerable%601>  
  
 如果源数据未实现<xref:System.Collections.Generic.IEnumerable%601>、[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]实现的功能所需的提供程序*标准查询运算符*为该数据源。</xref:System.Collections.Generic.IEnumerable%601> 例如，[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]处理 XML 文档加载到可查询的工作<xref:System.Xml.Linq.XElement>类型，如下面的示例中所示。</xref:System.Xml.Linq.XElement> 有关标准查询运算符的详细信息，请参阅[标准查询运算符概述 (Visual Basic 中)](standard-query-operators-overview.md)。  
  
 [!code-vb[VbLINQFirstQuery #&2;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_2.vb)]  
  
 与[!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)]，您首先创建一个对象关系映射在设计时，手动或通过使用[LINQ to SQL 工具在 Visual Studio 中](https://docs.microsoft.com/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)Visual Studio 中。 编写查询针对的对象，而是在运行时[!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)]处理与数据库通信。 在下面的示例中，`customers`表示的特定表中的数据库，并<xref:System.Data.Linq.Table%601>支持泛型<xref:System.Linq.IQueryable%601>。</xref:System.Linq.IQueryable%601> </xref:System.Data.Linq.Table%601>  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 有关如何创建特定类型的数据源的详细信息，请参阅各种文档[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]提供程序。 (有关这些提供程序的列表，请参阅[LINQ （语言集成查询）](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)。)基本规则很简单︰[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]数据源是任何支持的泛型<xref:System.Collections.Generic.IEnumerable%601>接口或从其继承的接口</xref:System.Collections.Generic.IEnumerable%601>的对象  
  
> [!NOTE]
>  类型，如<xref:System.Collections.ArrayList>支持非泛型<xref:System.Collections.IEnumerable>接口也可以用作[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]数据源。</xref:System.Collections.IEnumerable> </xref:System.Collections.ArrayList> 有关使用示例， <xref:System.Collections.ArrayList>，请参阅[如何︰ 使用 (Visual Basic 中) 的 LINQ 查询 ArrayList](how-to-query-an-arraylist-with-linq.md)。</xref:System.Collections.ArrayList>  
  
## <a name="the-query"></a>查询  
 在查询中，您可以指定您想要从数据源中检索哪些的信息。 此外可以指定如何应排序、 分组，或结构化之前它将返回该信息。 若要启用查询创建，Visual Basic 已合并到该语言的新的查询语法。  
  
 下面的示例中的查询时执行，从整数数组中，返回所有偶数`numbers`。  
  
 [!code-vb[VbLINQFirstQuery #&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_1.vb)]  
  
 查询表达式包含三个子句︰ `From`， `Where`，和`Select`。 中所述的特定功能和用途的每个查询表达式子句[基本查询操作 (Visual Basic 中)](basic-query-operations.md)。 有关详细信息，请参阅[查询](../../../../visual-basic/language-reference/queries/queries.md)。 请注意，在[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]，查询定义通常存储在一个变量，并在以后执行。 查询变量，如`evensQuery`在上一示例中，必须为可查询类型。 一种`evensQuery`是`IEnumerable(Of Integer)`、 分配由编译器使用局部类型推理。  
  
 请务必请记住，则查询变量本身不执行任何操作，并且不返回任何数据。 它只存储查询定义。 在上例中，它是`For Each`执行查询的循环。  
  
## <a name="query-execution"></a>查询执行  
 从查询创建单独查询执行。 创建查询定义查询，但由不同的机制时将触发执行。 可以执行查询，只要它定义 (*立即执行*)，或定义可以存储和更高版本执行查询 (*延迟执行*)。  
  
### <a name="deferred-execution"></a>延迟执行  
 典型[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查询与在上一示例中，在其中一个示例相似`evensQuery`定义。 它创建了查询，但不立即执行查询。 相反，在查询变量中存储的查询定义`evensQuery`。 执行查询更高版本，通常需要使用`For Each`循环，它返回序列的值，或通过应用一个标准查询运算符，如`Count`或`Max`。 此过程称为*延迟执行*。  
  
 [!code-vb[VbLINQFirstQuery #&7;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_3.vb)]  
  
 通过使用中的迭代变量的检索到的数据访问的一系列值，`For Each`循环 (`number`在前面的示例)。 因为查询变量`evensQuery`，保存的查询定义，而不是查询结果中，您可以根据需要使用一次以上的查询变量的频繁执行查询。 例如，您可能会在单独的应用程序的持续更新的应用程序中有一个数据库。 创建从该数据库中检索数据的查询后，可以使用`For Each`循环反复执行查询，每次都检索最新的数据。  
  
 下面的示例演示如何延迟的执行的工作。 之后`evensQuery2`定义并的情况下执行`For Each`循环中，与前面的示例中，数据源中的某些元素`numbers`发生更改。 然后，另一个`For Each`循环运行`evensQuery2`再次。 结果将不同的第二个时间，因为`For Each`循环执行查询同样，使用中的新值`numbers`。  
  
 [!code-vb[VbLINQFirstQuery #&3;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_4.vb)]  
  
 输出：  
  
 `Evens in original array:`  
  
 `0  2  4  6`  
  
 `Evens in changed array:`  
  
 `0  10  2  22  8`  
  
### <a name="immediate-execution"></a>立即执行  
 在延迟执行的查询中，查询定义存储在查询变量中以供以后执行。 立即执行，而在其定义时执行查询。 当应用需要访问的各个元素的查询结果的方法时，将触发执行。 立即执行通常会强制使用返回单个值的标准查询运算符之一。 Examples are `Count`, `Max`, `Average`, and `First`. 这些标准查询运算符执行的查询，只要它们应用以便计算并返回单一实例结果。 有关返回单个值的标准查询运算符的详细信息，请参阅[聚合操作](aggregation-operations.md)，[元素操作](element-operations.md)，和[限定符操作](quantifier-operations.md)。  
  
 下面的查询返回一个整数数组中的偶数的计数。 查询定义不保存，和`numEvens`是一个简单`Integer`。  
  
 [!code-vb[VbLINQFirstQuery #&4;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_5.vb)]  
  
 可以通过使用实现相同的结果`Aggregate`方法。  
  
 [!code-vb[VbLINQFirstQuery #&5;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_6.vb)]  
  
 您也可以通过调用强制执行的查询`ToList`或`ToArray`（立即） 的查询或查询变量 （延迟），如下面的代码中所示的方法。  
  
 [!code-vb[VbLINQFirstQuery #&6;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_7.vb)]  
  
 在前面的示例中，`evensQuery3`是一个查询变量，而`evensList`是列表和`evensArray`是一个数组。  
  
 使用`ToList`或`ToArray`强制立即执行是在想要立即执行查询并将结果缓存在单个集合对象的方案中尤其有用。 有关这些方法的详细信息，请参阅[转换数据类型](converting-data-types.md)。  
  
 您也可以使查询以使用执行`IEnumerable`方法如<xref:Microsoft.VisualBasic.Collection.System%23Collections%23IEnumerable%23GetEnumerator%2A>方法。</xref:Microsoft.VisualBasic.Collection.System%23Collections%23IEnumerable%23GetEnumerator%2A>  
  
## <a name="see-also"></a>另请参阅  
 [在 Visual Basic 中的 LINQ 入门](getting-started-with-linq.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [标准查询运算符概述 (Visual Basic)](standard-query-operators-overview.md)   
 [在 Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [查询](../../../../visual-basic/language-reference/queries/queries.md)
