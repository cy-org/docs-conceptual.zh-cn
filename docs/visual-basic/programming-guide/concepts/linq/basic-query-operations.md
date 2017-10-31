---
title: "基本查询操作 (Visual Basic 中) |Microsoft 文档"
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
- data sources [LINQ in Visual Basic]
- Join clause [LINQ in Visual Basic]
- ordering data [LINQ in Visual Basic]
- projections [LINQ in Visual Basic]
- LINQ [Visual Basic], query operations
- Order By clause [LINQ in Visual Basic]
- joining data [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], basic operations
- selecting data [LINQ in Visual Basic]
- Group By clause [LINQ in Visual Basic]
- grouping data [LINQ in Visual Basic]
- Select clause [LINQ in Visual Basic]
ms.assetid: 1146f6d0-fcb8-4f4d-8223-c9db52620d21
caps.latest.revision: 37
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: 87ff9173b5ff72385c8ecdc3ff13735e7be2a21d
ms.lasthandoff: 03/13/2017

---
# <a name="basic-query-operations-visual-basic"></a>基本查询操作 (Visual Basic)
本主题提供了简要介绍了[!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)]表达式在 Visual Basic 和一些典型的一种在查询中执行的操作。 有关详细信息，请参阅下列主题：  
  
 [在 Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)  
  
 [查询](../../../../visual-basic/language-reference/queries/queries.md)  
  
 [演练︰ 在 Visual Basic 中编写查询](../../../../visual-basic/programming-guide/concepts/linq/walkthrough-writing-queries.md)  
  
## <a name="specifying-the-data-source-from"></a>指定数据源 （从）  
 在[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查询中，第一步是指定您想要查询的数据源。 因此，`From`查询中的子句始终最先出现。 查询运算符选择和形状基于源的类型的结果。  
  
 [!code-vb[VbLINQBasicOps #&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_1.vb)]  
  
 `From`子句指定数据源， `customers`，和一个*范围变量*， `cust`。 范围变量循环迭代与变量一样，只是在查询表达式中，实际上不发生迭代。 执行查询时，通常使用`For Each`循环中，作为对中的每个后续元素的引用的范围变量`customers`。 因为编译器可以推断的一种`cust`，无需显式指定。 有关编写显式超时和没有显式类型化的查询的示例，请参阅[查询操作 (Visual Basic 中) 中的类型关系](../../../../visual-basic/programming-guide/concepts/linq/type-relationships-in-query-operations.md)。  
  
 有关如何使用`From`子句在 Visual Basic 中，请参阅[From 子句](../../../../visual-basic/language-reference/queries/from-clause.md)。  
  
## <a name="filtering-data-where"></a>筛选数据 （位置）  
 可能最常见的查询操作应用布尔表达式的窗体中的筛选器。 然后，查询将返回仅对表达式为 true 的元素。 一个`Where`子句用来执行筛选。 筛选器指定要包括在结果序列中的数据源中的哪些元素。 在下面的示例中，只有这些地址位于伦敦的客户是包括在内。  
  
 [!code-vb[VbLINQBasicOps #&2;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_2.vb)]  
  
 您可以使用逻辑运算符，如`And`和`Or`组合中的筛选器表达式`Where`子句。 例如，若要返回的客户，只有那些来自伦敦，并姓名为 Devon，使用下面的代码︰  
  
```vb  
Where cust.City = "London" And cust.Name = "Devon"   
```  
  
 若要返回客户位于伦敦或巴黎，请使用下面的代码︰  
  
```vb  
Where cust.City = "London" Or cust.City = "Paris"   
```  
  
 有关如何使用`Where`子句在 Visual Basic 中，请参阅[Where 子句](../../../../visual-basic/language-reference/queries/where-clause.md)。  
  
## <a name="ordering-data-order-by"></a>对数据 (Order By) 进行排序  
 它通常很方便地对返回的数据按特定顺序进行排序。 `Order By`子句将使返回的序列进行排序的指定的字段或字段中的元素。 例如，下面的查询进行排序的结果基于`Name`属性。 因为`Name`是一个字符串，返回的数据将从 A 到 Z 的按字母顺序排序。  
  
 [!code-vb[VbLINQBasicOps #&3;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_3.vb)]  
  
 对结果进行排序以相反顺序，从 Z 到 A，使用`Order By...Descending`子句。 默认值是`Ascending`当没有`Ascending`，也不`Descending`指定。  
  
 有关如何使用`Order By`子句在 Visual Basic 中，请参阅[Order By 子句](../../../../visual-basic/language-reference/queries/order-by-clause.md)。  
  
## <a name="selecting-data-select"></a>选择数据 （选择）  
 `Select`子句指定窗体和返回的元素的内容。 例如，可以指定您的结果将包含的是整个`Customer`对象时，只是一个`Customer`根据计算的属性、 属性的子集、 从各种数据源或某些新的结果类型的属性的组合。 当`Select`子句生成以外的源元素的副本，则调用该操作*投影*。  
  
 检索集合，其中包含的是整个`Customer`对象，选择范围变量本身︰  
  
 [!code-vb[VbLINQBasicOps #&4;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_4.vb)]  
  
 如果`Customer`实例是一个大型对象，有很多字段和您想要检索的就是名称，则可以选择`cust.Name`，如在下面的示例所示。 局部类型推理知道这会从集合中更改的结果类型`Customer`对象与字符串的集合。  
  
 [!code-vb[VbLINQBasicOps #&5;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_5.vb)]  
  
 若要从数据源选择多个字段，您有两个选择︰  
  
-   在`Select`子句中，指定你想要在结果中包括的字段。 编译器将定义这些字段作为其属性的匿名类型。 有关详细信息，请参阅[匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
     在下面的示例返回的元素是匿名类型的实例，因为您不能为类型名称来引用在其他地方在代码中。 该编译器指定类型的名称包含在普通 Visual Basic 代码中无效的字符。 在下面的示例中的查询返回的集合中的元素`londonCusts4`是匿名类型的实例  
  
     [!code-vb[VbLINQBasicOps #&6;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_6.vb)]  
  
     - 或 -  
  
-   定义包含您想要包括在结果中，创建并初始化中的类型的实例的特定字段的已命名的类型`Select`子句。 仅当您需要使用各个结果集合外部的顺序返回它们，或者如果您必须将它们作为方法调用中的参数传递，请使用此选项。 一种`londonCusts5`在下面的示例是 IEnumerable (Of NamePhone)。  
  
     [!code-vb[VbLINQBasicOps #&7;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_7.vb)]  
  
     [!code-vb[VbLINQBasicOps #&8;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_8.vb)]  
  
 有关如何使用`Select`子句在 Visual Basic 中，请参阅[Select 子句](../../../../visual-basic/language-reference/queries/select-clause.md)。  
  
## <a name="joining-data-join-and-group-join"></a>联接数据 （联接和分组联接）  
 您可以组合使用多个数据源中的`From`子句中有多种。 例如，下面的代码使用两个数据源并隐式将从这两个结果中的属性进行合并。 该查询用于选择的学生以元音开头的姓氏和名字。  
  
 [!code-vb[VbLINQBasicOps #&9;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_9.vb)]  
  
> [!NOTE]
>  您可以运行此代码中创建的学生列表[如何︰ 创建列表项](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)。  
  
 `Join`关键字等效于`INNER JOIN`SQL 中。 它结合了基于两个集合中的元素之间的匹配项的值的两个集合。 查询将返回具有匹配的键值对集合元素的全部或部分。 例如，下面的代码重复项上一个隐式联接的操作。  
  
 [!code-vb[VbLINQBasicOps #&10;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_10.vb)]  
  
 `Group Join`将集合组合为单个的分层集合，就像`LEFT JOIN`在 SQL 中。 有关详细信息，请参阅[Join 子句](../../../../visual-basic/language-reference/queries/join-clause.md)和[Group Join 子句](../../../../visual-basic/language-reference/queries/group-join-clause.md)。  
  
## <a name="grouping-data-group-by"></a>对数据进行分组 (Group By)  
 您可以添加`Group By`子句进行分组元素的一个或多个字段根据查询结果中的元素。 例如，下面的代码进行分组的学生类年度。  
  
 [!code-vb[VbLINQBasicOps #&11;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_11.vb)]  
  
 如果您运行此代码中使用的列表中创建的学生[如何︰ 创建列表项](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)，从输出`For Each`语句是︰  
  
 年份︰ 初级  
  
 Tucker Michael  
  
 Garcia Hugo  
  
 Garcia Debra  
  
 Tucker Lance  
  
 年份︰ 高级  
  
 Omelchenko Svetlana  
  
 Osada Michiko  
  
 Ä Fadi  
  
 Feng 汉英  
  
 Terry Adams  
  
 年份︰ 新生  
  
 Mortensen Sven  
  
 Garcia Cesar  
  
 在下面的代码所示的变体年级，并按姓氏进行每年内然后排序学生。  
  
 [!code-vb[VbLINQBasicOps #&12;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_12.vb)]  
  
 有关详细信息`Group By`，请参阅[组 By 子句](../../../../visual-basic/language-reference/queries/group-by-clause.md)。  
  
## <a name="see-also"></a>请参见  
 <xref:System.Collections.Generic.IEnumerable%601></xref:System.Collections.Generic.IEnumerable%601>   
 [在 Visual Basic 中的 LINQ 入门](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [查询](../../../../visual-basic/language-reference/queries/queries.md)   
 [标准查询运算符概述 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)
