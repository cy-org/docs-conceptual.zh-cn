---
title: "LINQ 和泛型类型 (C#)"
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
- LINQ [C#], generic types
- generic types [LINQ]
- generics [LINQ]
ms.assetid: 660e3799-25ca-462c-8c4a-8bce04fbb031
caps.latest.revision: 18
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
ms.openlocfilehash: 177db64491d58b31ca50cef0bb2eda8c2cb65078
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="linq-and-generic-types-c"></a>LINQ 和泛型类型 (C#)
[!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询基于 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 2.0 版中引入的泛型类型。 无需深入了解泛型即可开始编写查询。 但是，可能需要了解 2 个基本概念：  
  
1.  创建泛型集合类（如 <xref:System.Collections.Generic.List%601>）的实例时，需将“T”替换为列表将包含的对象类型。 例如，字符串列表表示为 `List<string>`，`Customer` 对象列表表示为 `List<Customer>`。 泛型列表属于强类型，与将其元素存储为 <xref:System.Object> 的集合相比，泛型列表具备更多优势。 如果尝试将 `Customer` 添加到 `List<string>`，则会在编译时收到错误。 泛型集合易于使用的原因是不必执行运行时类型转换。  
  
2.  <xref:System.Collections.Generic.IEnumerable%601> 是一个接口，通过该接口，可以使用 `foreach` 语句来枚举泛型集合类。 泛型集合类支持 <xref:System.Collections.Generic.IEnumerable%601>，正如非泛型集合类（如 <xref:System.Collections.ArrayList>）支持 <xref:System.Collections.IEnumerable>。  
  
 有关泛型的详细信息，请参阅[泛型](../../../../csharp/programming-guide/generics/index.md)。  
  
## <a name="ienumerablet-variables-in-linq-queries"></a>LINQ 查询中的 IEnumerable<T\> 变量  
 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询变量被类型化为 <xref:System.Collections.Generic.IEnumerable%601> 或者派生类型（如 <xref:System.Linq.IQueryable%601>）。 看到类型化为 `IEnumerable<Customer>` 的查询变量时，这只意味着执行查询时，该查询将生成包含零个或多个 `Customer` 对象的序列。  
  
 [!code-cs[csLINQGettingStarted#34](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/linq-and-generic-types_1.cs)]  
  
 有关详细信息，请参阅 [LINQ 查询操作中的类型关系](../../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md)。  
  
## <a name="letting-the-compiler-handle-generic-type-declarations"></a>让编译器处理泛型类型声明  
 如果愿意，可以使用 [var](../../../../csharp/language-reference/keywords/var.md) 关键字来避免使用泛型语法。 `var` 关键字指示编译器通过查看在 `from` 子句中指定的数据源来推断查询变量的类型。 以下示例生成与上例相同的编译代码：  
  
 [!code-cs[csLINQGettingStarted#35](../../../../csharp/programming-guide/concepts/linq/codesnippet/CSharp/linq-and-generic-types_2.cs)]  
  
 变量的类型明显或显式指定嵌套泛型类型（如由组查询生成的那些类型）并不重要时，`var` 关键字很有用。 通常，我们建议如果使用 `var`，应意识到这可能使他人更难以理解代码。 有关详细信息，请参阅[隐式类型本地变量](../../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)。  
  
## <a name="see-also"></a>请参阅  
 [C# 中的 LINQ 入门](../../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [泛型](../../../../csharp/programming-guide/generics/index.md)

