---
title: "类型查询操作 (Visual Basic 中) 中的关系 |Microsoft 文档"
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
- variable relationships [LINQ in Visual Basic]
- type information inferred [LINQ in Visual Basic]
- type relationships [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], type relationships
- data sources [LINQ in Visual Basic], type relationships
- LINQ [Visual Basic], type relationships
- inferring type information [LINQ in Visual Basic]
- relationships [LINQ in Visual Basic]
ms.assetid: b5ff4da5-f3fd-4a8e-aaac-1cbf52fa16f6
caps.latest.revision: 34
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
ms.openlocfilehash: a966b69feca7a7021cafbccb7971913ea781c479
ms.lasthandoff: 03/13/2017

---
# <a name="type-relationships-in-query-operations-visual-basic"></a>查询操作中的类型关系 (Visual Basic)
在中使用变量[!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)]查询操作都强类型，并且必须是相互兼容。 数据源、 查询本身，以及执行查询，都使用强类型。 下图列出术语用于描述[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查询。 有关查询的部件的详细信息，请参阅[基本查询操作 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/basic-query-operations.md)。  
  
 ![具有突出显示的元素的伪代码查询。](../../../../visual-basic/programming-guide/concepts/linq/media/sjltyperels.png "SJLtypeRels")  
LINQ 查询的各个部分  
  
 在查询中的范围变量的类型必须与数据源中的元素的类型兼容。 查询变量的类型必须与在中定义的序列元素兼容`Select`子句。 最后，序列元素的类型也必须与使用中的循环控制变量的类型兼容`For Each`执行查询的语句。 此强类型便于在编译时识别类型错误。  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]使强类型方便通过实现局部类型推理，也称为*隐式类型化*。 在上一示例中，使用功能，您将看到在整个[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]示例和文档。 在 Visual Basic 中，局部类型推理通过只需使用`Dim`语句而不进行`As`子句。 在下面的示例中，`city`强类型化为字符串。  
  
 [!code-vb[VbLINQTypeRels #&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/type-relationships-in-query-operations_1.vb)]  
  
> [!NOTE]
>  局部类型推理时才起作用`Option Infer`设置为`On`。 有关详细信息，请参阅[Option Infer 语句](../../../../visual-basic/language-reference/statements/option-infer-statement.md)。  
  
 但是，即使在查询中使用局部类型推理，是在数据源中的变量、 查询变量和查询执行循环之间存在相同的类型关系。 可用于进行基本的了解对这些类型关系，在编写时[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查询或使用示例和文档中的代码示例。  
  
 您可能需要指定显式类型从数据源返回的类型不匹配的范围变量。 可以通过使用指定的范围变量的类型`As`子句。 但是，这会导致一个错误如果转换，则[收缩转换](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)和`Option Strict`设置为`On`。 因此，我们建议您从数据源检索的值上执行转换。 您可以将值转换从数据源为显式范围变量类型使用<xref:System.Linq.Enumerable.Cast%2A>方法。</xref:System.Linq.Enumerable.Cast%2A> 也可以显式转换中选定的值`Select`范围变量的类型不同的显式类型的子句。 在下面的代码阐释了这些点。  
  
 [!code-vb[VbLINQTypeRels #&4;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/type-relationships-in-query-operations_2.vb)]  
  
## <a name="queries-that-return-entire-elements-of-the-source-data"></a>查询返回的源数据的整个元素  
 下面的示例演示[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查询返回的源数据中的选定元素的序列的操作。 源， `names`，包含数组的字符串，并且查询输出是包含以字母 M 开头的字符串的序列。  
  
 [!code-vb[VbLINQTypeRels #&2;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/type-relationships-in-query-operations_3.vb)]  
  
 这等效于下面的代码，但它更简短、 更易于编写。 依赖于在查询中的局部类型推理是在 Visual Basic 中的首选的样式。  
  
 [!code-vb[VbLINQTypeRels #&3;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/type-relationships-in-query-operations_4.vb)]  
  
 在这两个前面的代码示例中，情况下，隐式或显式类型确定是否存在下面的关系。  
  
1.  数据源中的元素的类型`names`，是一种范围变量`name`，在查询中。  
  
2.  选择后，该对象的类型`name`，确定查询变量的类型`mNames`。 此处`name`是一个字符串，因此查询变量是在 Visual Basic 中的 IEnumerable (Of String)。  
  
3.  中定义的查询`mNames`中执行`For Each`循环。 循环将循环访问查询的执行结果。 因为`mNames`，它在执行时，将返回一个字符串，循环迭代变量序列`nm`，也是一个字符串。  
  
## <a name="queries-that-return-one-field-from-selected-elements"></a>返回从所选元素的一个字段的查询  
 下面的示例演示[!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)]查询返回包含从数据源中选择每个元素的只有一个部件的序列的操作。 查询采用集合`Customer`对象作为其数据源并仅投射`Name`结果中的属性。 客户名称是字符串，因为此查询将生成一个字符串序列作为输出。  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 变量之间的关系是类似于更简单的示例中。  
  
1.  数据源中的元素的类型`customers`，是一种范围变量`cust`，在查询中。 在此示例中，该类型为`Customer`。  
  
2.  `Select`语句返回`Name`每个属性`Customer`对象而不是整个对象。 因为`Name`是一个字符串，该查询变量， `custNames`，再次将 IEnumerable (Of String)，不属于`Customer`。  
  
3.  因为`custNames`代表一个字符串，序列`For Each`循环的迭代变量`custName`，必须为字符串。  
  
 而无需局部类型推理，前面的示例将很难编写和理解，如以下示例所示。  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
## <a name="queries-that-require-anonymous-types"></a>需要匿名类型的查询  
 下面的示例演示更复杂的情况。 在上一示例中，不是很方便显式指定类型的所有变量。 在此示例中，不可能。 而不是选择整个`Customer`元素从数据源或从每个元素的单个字段`Select`子句在此查询将返回两个属性的原始`Customer`对象︰`Name`和`City`。 在响应`Select`子句中，编译器会定义包含这两个属性的匿名类型。 执行的结果`nameCityQuery`中`For Each`循环是新的匿名类型的实例的集合。 因为匿名类型中没有可用的名称，不能指定的一种`nameCityQuery`或`custInfo`显式。 也就是说，使用匿名类型，有没有类型名称来代替了`String`中`IEnumerable(Of String)`。 有关详细信息，请参阅[匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
 尽管不能为指定类型的变量上一示例中，关系保持不变。  
  
1.  数据源中的元素的类型同样是在查询中的范围变量的类型。 在此示例中，`cust`的一个实例`Customer`。  
  
2.  因为`Select`语句生成一个匿名类型，则查询变量， `nameCityQuery`，必须以匿名类型隐式类型。 匿名类型没有可用的名称，并因此无法显式指定它。  
  
3.  中的迭代变量的类型`For Each`循环是在步骤 2 中创建的匿名类型。 因为该类型没有可用的名称，则必须隐式确定循环迭代变量的类型。  
  
## <a name="see-also"></a>另请参阅  
 [在 Visual Basic 中的 LINQ 入门](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [在 Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [查询](../../../../visual-basic/language-reference/queries/queries.md)
