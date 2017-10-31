---
title: "支持 LINQ 的 Visual Basic 功能 |Microsoft 文档"
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
- Visual Basic, LINQ features
- LINQ [Visual Basic], features supporting LINQ
ms.assetid: c821bb50-b6f6-4cf9-8aba-2717e465bd3a
caps.latest.revision: 51
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
ms.openlocfilehash: 3bca15a07a88195589b9c9de5f9842eea42912f1
ms.lasthandoff: 03/13/2017

---
# <a name="visual-basic-features-that-support-linq"></a>支持 LINQ 的 Visual Basic 功能
名称[!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)]是指在 Visual Basic 中支持查询语法和其他语言构造直接在语言中的技术。 与[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]，无需学习新语言对外部数据源执行查询。 可以通过使用 Visual Basic 查询针对关系数据库、 XML 存储或对象中的数据。 此集成到该语言的查询功能使编译时检查有语法错误和类型安全。 这一集成还可确保您已经知道您需要了解在 Visual Basic 中编写丰富的、 不同的查询的大部分。  
  
 以下各节描述了足够的详细信息，以使您能够开始阅读介绍性文档、 代码示例和示例应用程序中支持 LINQ 的语言构造。 您还可以单击链接，以了解如何语言功能组合在一起以启用对语言集成查询的更详细的解释。 是一个好启动[演练︰ 在 Visual Basic 中编写查询](../../../../visual-basic/programming-guide/concepts/linq/walkthrough-writing-queries.md)。  
  
## <a name="query-expressions"></a>查询表达式  
 在 Visual Basic 中的查询表达式可以用类似于 SQL 或 XQuery 的声明性语法来表示。 在编译时，查询语法转换为对标准查询运算符扩展方法的 LINQ 提供程序实现的方法调用。 应用程序来控制它们在作用域内是通过指定具有适当的命名空间的标准查询运算符`Imports`语句。 Visual Basic 查询表达式的语法如下所示︰  
  
 [!code-vb[VbLINQVbFeatures #&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_1.vb)]  
  
 有关详细信息，请参阅[在 Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)。  
  
## <a name="implicitly-typed-variables"></a>隐式类型化的变量  
 而不是在显式指定类型声明和初始化变量时，可以使编译器能够推断并分配类型。 这被称为*局部类型推理*。  
  
 变量推断其类型强类型，就像您显式指定其类型的变量一样。 局部类型推理仅用于定义在方法体内的本地变量。 有关详细信息，请参阅[Option Infer 语句](../../../../visual-basic/language-reference/statements/option-infer-statement.md)和[本地类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)。  
  
 下面的示例说明了局部类型推理。 若要使用此示例，必须设置`Option Infer`到`On`。  
  
 [!code-vb[VbLINQVbFeatures #&2;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_2.vb)]  
  
 局部类型推理还使可以创建匿名类型，也不能在本部分稍后介绍 LINQ 查询所必需的。  
  
 在下面的 LINQ 示例中，会发生类型推理如果`Option Infer`是`On`或`Off`。 如果发生编译时错误`Option Infer`是`Off`和`Option Strict`是`On`。  
  
 [!code-vb[VbLINQVbFeatures #&3;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_3.vb)]  
  
## <a name="object-initializers"></a>对象初始值设定项  
 当您必须创建一个匿名类型来保存查询的结果时，将在查询表达式中使用对象初始值设定项。 它们还可用于初始化外部查询的命名类型的对象。 通过使用对象初始值设定项，可以无需显式调用构造函数初始化单个行中的对象。 假设有一个名为类`Customer`该类具有公共`Name`和`Phone`属性，以及其他属性，可以按照此方式使用对象初始值设定项︰  
  
 [!code-vb[VbLINQVbFeatures #&4;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_4.vb)]  
  
 有关详细信息，请参阅[对象初始值设定项︰ 命名类型和匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)。  
  
## <a name="anonymous-types"></a>匿名类型  
 匿名类型提供了方便地暂时你想要在查询结果中包含的元素进行分组的一组属性。 这使您在查询中，按任意顺序选择可用的字段的任意组合，而不定义该元素的已命名的数据类型。  
  
 *匿名类型*由编译器动态构造。 由该编译器中，分配的类型的名称，它可能会更改与每个新的编译。 因此，不能直接使用该名称。 按以下方式初始化匿名类型︰  
  
 [!code-vb[VbLINQVbFeatures #&5;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_5.vb)]  
  
 有关详细信息，请参阅[匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
## <a name="extension-methods"></a>扩展方法  
 扩展方法，可以将方法添加到数据类型或接口的定义之外的位置。 此功能使您能够，实际上，向现有类型添加新方法，而无需实际修改该类型。 标准查询运算符本身就是扩展方法，它们提供了一组[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查询实现<xref:System.Collections.Generic.IEnumerable%601>。</xref:System.Collections.Generic.IEnumerable%601>的任何类型的功能 对其他扩展<xref:System.Collections.Generic.IEnumerable%601>包括<xref:System.Linq.Enumerable.Count%2A>， <xref:System.Linq.Enumerable.Union%2A>，和<xref:System.Linq.Enumerable.Intersect%2A>。</xref:System.Linq.Enumerable.Intersect%2A> </xref:System.Linq.Enumerable.Union%2A> </xref:System.Linq.Enumerable.Count%2A> </xref:System.Collections.Generic.IEnumerable%601>  
  
 下面的扩展方法将 print 方法添加到<xref:System.String>类。</xref:System.String>  
  
 [!code-vb[VbLINQVbFeatures #&6;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_6.vb)]  
  
 该方法的调用方式类似<xref:System.String>::</xref:System.String>的普通实例方法  
  
 [!code-vb[VbLINQVbFeatures #&7;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_7.vb)]  
  
 有关详细信息，请参阅[扩展方法](../../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)。  
  
## <a name="lambda-expressions"></a>Lambda 表达式  
 Lambda 表达式是函数，而不计算并返回单个值的名称。 命名与函数不同，可以定义并在同一时间执行 lambda 表达式。 下面的示例显示 4。  
  
 [!code-vb[VbLINQVbFeatures #&8;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_8.vb)]  
  
 您可以将 lambda 表达式定义分配给变量的名称，然后使用名称才能调用该函数。 下面的示例还显示 4。  
  
 [!code-vb[VbLINQVbFeatures #&12;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_9.vb)]  
  
 在[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]，lambda 表达式是许多标准查询运算符的基础。 编译器将创建 lambda 表达式，以捕获等基本查询方法中定义的计算`Where`， `Select`， `Order By`， `Take While`，和其他人。  
  
 例如，下面的代码定义一个查询，返回所有高级学员的学生列表中。  
  
 [!code-vb[VbLINQVbFeatures #&9;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_10.vb)]  
  
 查询定义编译为类似于下面的示例使用两个 lambda 表达式来指定的参数的代码`Where`和`Select`。  
  
 [!code-vb[VbLINQVbFeatures #&10;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_11.vb)]  
  
 可以使用运行任何一个版本`For Each`循环︰  
  
 [!code-vb[VbLINQVbFeatures #&11;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/features-that-support-linq_12.vb)]  
  
 有关详细信息，请参阅[Lambda 表达式](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)。  
  
## <a name="see-also"></a>另请参阅  
 [语言集成查询 (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/index.md)   
 [在 Visual Basic 中的 LINQ 入门](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [LINQ 和字符串 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)   
 [Option Infer 语句](../../../../visual-basic/language-reference/statements/option-infer-statement.md)   
 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)
