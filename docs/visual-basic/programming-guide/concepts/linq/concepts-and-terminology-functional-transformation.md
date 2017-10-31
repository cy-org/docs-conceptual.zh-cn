---
title: "概念和术语 （功能转换） (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 24fd244d-ebae-4721-8858-89bb544aea0b
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9c4716765199798e50c4318b290f8a2d76ef5841
ms.lasthandoff: 03/13/2017


---
# <a name="concepts-and-terminology-functional-transformation-visual-basic"></a>概念和术语 （功能转换） (Visual Basic)
本主题介绍纯函数转换的概念和术语。 与更加传统的命令性编程方式相比，用来转换数据的函数转换方法所生成的代码往往编程速度更快、含义更明确、更易于调试和维护。  
  
 请注意，本节中的主题并不是要透彻解释函数编程。 这些主题只是介绍函数编程的一些功能，这些功能降低了将 XML 从一种形状转换为另一种形状的难度。  
  
## <a name="what-is-pure-functional-transformation"></a>什么是纯函数转换？  
 在*纯函数转换*，一组函数，称为*纯函数*，定义如何将一组结构化数据从其原始格式转换为另一种形式。 "纯"一词表示的函数是*可组合*，这要求它们是︰  
  
-   *自包含*，以便它们可以自由排序和重新排列，而不牵连和与该程序的其余部分相互依赖关系。 纯转换不了解其环境，对环境也没有任何影响。 也就是说，用在转换中的函数没有*副作用*。  
  
-   *无状态*，因而对相同输入执行相同的函数或组特定的函数将始终产生相同的输出。 纯转换对于先前对它的使用没有记忆。  
  
> [!IMPORTANT]
>  在本教程的其余部分，术语“纯函数”用于概括表示编程方法，而不是具体的语言功能。  
>   
>  请注意，必须为在 Visual Basic 中的函数实现纯函数。  
>   
>  此外，不要将纯函数与 C++ 中的纯虚方法混淆。 后者表示包含类是抽象的，并且不提供方法体。  
  
### <a name="functional-programming"></a>函数编程  
 *函数编程*是一种直接支持纯函数转换编程方法。  
  
 从历史上看，通用函数编程语言，如 ML、 方案、 Haskell 和 F # 中，已经浓厚的兴趣学术团体。 尽管它一直可以用来在 Visual Basic 中编写纯函数转换，但这样做的困难使之不具它对大多数程序员来说一个不错的选择。 有更高版本的 Visual Basic 中，但是，新语言构造如 lambda 表达式和类型推理降低了函数编程可以更简单、 提高工作效率。  
  
 有关函数编程的详细信息，请参阅[功能性编程 vs。(Visual Basic 中) 的命令性编程](../../../../visual-basic/programming-guide/concepts/linq/functional-programming-vs-imperative-programming.md)。  
  
#### <a name="domain-specific-fp-languages"></a>特定于域的 FP 语言  
 虽然通用函数编程语言并未得到广泛采用，但特定于域的函数编程语言却得到了较为成功的应用。 例如，级联样式表 (CSS) 用于确定许多网页的外观，可扩展样式表转换语言 (XSLT) 样式表广泛应用于 XML 数据操作中。 有关 XSLT 的详细信息，请参阅[XSLT 转换](http://msdn.microsoft.com/library/202f8820-224c-494f-b61e-cd127eac6e03)。  
  
## <a name="terminology"></a>术语  
 下表定义了一些与函数转换相关的术语。  
  
 高阶（第一类）函数  
 可作为编程对象的一种函数。 例如，高阶函数可以传递到其他函数或从其他函数返回。 在 Visual Basic 中，委托和 lambda 表达式是支持高阶函数的语言功能。 若要编写高阶函数，需要声明一个或多个自变量来接受委托，而在调用该函数时通常使用 lambda 表达式。 许多标准查询运算符都属于高阶函数。  
  
 有关详细信息，请参阅[标准查询运算符概述 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)。  
  
 lambda 表达式  
 实质上是一个匿名的内联函数，可用在任何需要委托类型的地方。 这是对 lambda 表达式的一个简化的定义，但足以满足本教程的需要。  
  
 有关详细信息，请参阅[Lambda 表达式](../../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)。  
  
 集合  
 结构化的一组数据，通常具有统一的类型。 若要与 LINQ 兼容，集合必须实现<xref:System.Collections.IEnumerable>接口或<xref:System.Linq.IQueryable>接口 (或它们对应的泛型之一<xref:System.Collections.Generic.IEnumerator%601>或<xref:System.Linq.IQueryable%601>)。</xref:System.Linq.IQueryable%601> </xref:System.Collections.Generic.IEnumerator%601> </xref:System.Linq.IQueryable> </xref:System.Collections.IEnumerable>  
  
 元组（匿名类型）  
 一个数学概念，元组是一个有限的对象序列，每个对象具有特定的类型。 元组也称为有序列表。 匿名类型是此概念的语言实现，支持在声明未命名类类型的同时实例化该类型的对象。  
  
 有关详细信息，请参阅[匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
 类型推理（隐式确定类型）  
 在没有显式类型声明的情况下编译器确定变量类型的能力。  
  
 有关详细信息，请参阅[本地类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)。  
  
 延迟执行和迟缓计算  
 延迟表达式的计算，直到实际需要它的求解值。 集合中支持延迟执行。  
  
 有关详细信息，请参阅[基本查询操作 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/basic-query-operations.md)和[延迟执行和迟缓计算 LINQ to XML (Visual Basic 中) 中](../../../../visual-basic/programming-guide/concepts/linq/deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)。  
  
 本节各处的代码示例中将使用这些语言功能。  
  
## <a name="see-also"></a>另请参阅  
 [介绍纯函数转换 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/introduction-to-pure-functional-transformations.md)   
 [函数编程与命令式编程 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/functional-programming-vs-imperative-programming.md)
