---
title: "概念和术语（函数转换）(C#)"
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
ms.assetid: 03defb3a-7e17-4ab1-8efa-4dd66621e860
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: ba05385b4cf686ac7bf8a203140338d31da80680
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="concepts-and-terminology-functional-transformation-c"></a>概念和术语（函数转换）(C#)
本主题介绍纯函数转换的概念和术语。 与更加传统的命令性编程方式相比，用来转换数据的函数转换方法所生成的代码往往编程速度更快、含义更明确、更易于调试和维护。  
  
 请注意，本节中的主题并不是要透彻解释函数编程。 这些主题只是介绍函数编程的一些功能，这些功能降低了将 XML 从一种形状转换为另一种形状的难度。  
  
## <a name="what-is-pure-functional-transformation"></a>什么是纯函数转换？  
 在纯函数转换中，称为“纯函数”的一组函数定义如何将一组结构化数据从其原始格式转换为另一种格式。 “纯”表示这些函数是可组合的，这要求这些函数具有以下特点：  
  
-   独立，这样函数就可以自由排序和重新排列，而不会与程序的其他部分相互牵连和依赖。 纯转换不了解其环境，对环境也没有任何影响。 也就是说，用在转换中的函数没有负作用。  
  
-   无状态，因而对相同输入执行相同的函数或特定的一组函数将始终产生相同的输出。 纯转换对于先前对它的使用没有记忆。  
  
> [!IMPORTANT]
>  在本教程的其余部分，术语“纯函数”用于概括表示编程方法，而不是具体的语言功能。  
>   
>  请注意，纯函数在 C# 中必须实现为方法。  
>   
>  此外，不要将纯函数与 C++ 中的纯虚方法混淆。 后者表示包含类是抽象的，并且不提供方法体。  
  
### <a name="functional-programming"></a>函数编程  
 函数编程是一种编程方法，直接支持纯函数转换。  
  
 学术团体对诸如 ML、Scheme、Haskell 和 F# 等通用函数编程语言一直抱有浓厚的兴趣。 虽然 C# 一直可以用来编写纯函数转换，然而实际操作的困难使之对大多数程序员来说不具吸引力。 但是在最新版本的 C# 中，像 Lambda 表达式和类型推理这样的新语言构造大大降低了函数编程的难度，也提高了函数编程的效率。  
  
 有关函数编程的详细信息，请参阅[函数编程与命令式编程 (C#)](../../../../csharp/programming-guide/concepts/linq/functional-programming-vs-imperative-programming.md)。  
  
#### <a name="domain-specific-fp-languages"></a>特定于域的 FP 语言  
 虽然通用函数编程语言并未得到广泛采用，但特定于域的函数编程语言却得到了较为成功的应用。 例如，级联样式表 (CSS) 用于确定许多网页的外观，可扩展样式表转换语言 (XSLT) 样式表广泛应用于 XML 数据操作中。 有关 XSLT 的详细信息，请参阅 [XSLT 转换](../../../../standard/data/xml/xslt-transformations.md)。  
  
## <a name="terminology"></a>术语  
 下表定义了一些与函数转换相关的术语。  
  
 高阶（第一类）函数  
 可作为编程对象的一种函数。 例如，高阶函数可以传递到其他函数或从其他函数返回。 在 C# 中，委托和 Lambda 表达式是支持高阶函数的语言功能。 若要编写高阶函数，需要声明一个或多个自变量来接受委托，而在调用该函数时通常使用 lambda 表达式。 许多标准查询运算符都属于高阶函数。  
  
 有关详细信息，请参阅[标准查询运算符概述 (C#)](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)。  
  
 lambda 表达式  
 实质上是一个匿名的内联函数，可用在任何需要委托类型的地方。 这是对 lambda 表达式的一个简化的定义，但足以满足本教程的需要。  
  
 有关 Lambda 表达式的详细信息，请参阅 [Lambda 表达式](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)。  
  
 集合  
 结构化的一组数据，通常具有统一的类型。 若要与 LINQ 兼容，集合必须实现 <xref:System.Collections.IEnumerable> 接口或 <xref:System.Linq.IQueryable> 接口（或它们对应的泛型接口 <xref:System.Collections.Generic.IEnumerator%601> 或 <xref:System.Linq.IQueryable%601> 之一）。  
  
 元组（匿名类型）  
 一个数学概念，元组是一个有限的对象序列，每个对象具有特定的类型。 元组也称为有序列表。 匿名类型是此概念的语言实现，支持在声明未命名类类型的同时实例化该类型的对象。  
  
 有关详细信息，请参阅[匿名类型](../../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)。  
  
 类型推理（隐式确定类型）  
 在没有显式类型声明的情况下编译器确定变量类型的能力。  
  
 有关详细信息，请参阅[隐式类型本地变量](../../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)。  
  
 延迟执行和迟缓计算  
 延迟表达式的计算，直到实际需要它的求解值。 集合中支持延迟执行。  
  
 有关详细信息，请参阅 [LINQ 查询简介 (C#)](../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md) 和 [LINQ to XML 中的延迟执行和迟缓计算 (C#)](../../../../csharp/programming-guide/concepts/linq/deferred-execution-and-lazy-evaluation-in-linq-to-xml.md)。  
  
 本节各处的代码示例中将使用这些语言功能。  
  
## <a name="see-also"></a>另请参阅  
 [纯函数转换简介 (C#)](../../../../csharp/programming-guide/concepts/linq/introduction-to-pure-functional-transformations.md)   
 [函数编程与命令式编程 (C#)](../../../../csharp/programming-guide/concepts/linq/functional-programming-vs-imperative-programming.md)

