---
title: "链接的查询 (LINQ to XML) 的性能 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 589f2adc-69f9-404d-b9d6-4c28dabea7f7
caps.latest.revision: 4
author: dotnet-bot
ms.author: dotnetcontent
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: dd5b63f255107c5864108cfbb87bef6e53a971a0
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017


---
# <a name="performance-of-chained-queries-linq-to-xml-visual-basic"></a>链接的查询 (LINQ to XML) 的性能 (Visual Basic)
LINQ（以及 LINQ to XML）的一个最重要优点是，链接查询的执行性能与单个更大更复杂的查询一样好。  
  
 链接查询是一种将另一个查询作为其源的查询。 例如，在下面的简单代码中，`query2` 使用 `query1` 作为其源：  
  
```vb  
Dim root As New XElement("Root", New XElement("Child", 1), New XElement("Child", 2), New XElement("Child", 3), New XElement("Child", 4))  
  
Dim query1 = From x In root.Elements("Child") Where CInt(x) >= 3x  
  
Dim query2 = From e In query1 Where CInt(e) Mod 2 = 0e  
  
For Each i As var In query2  
    Console.WriteLine("{0}", CInt(i))  
Next  
```  
  
 该示例产生下面的输出：  
  
```  
4  
```  
  
 此链接查询提供与循环访问链接列表相同的性能配置文件。  
  
-   <xref:System.Xml.Linq.XContainer.Elements%2A>轴具有与循环访问链接列表基本相同的性能。</xref:System.Xml.Linq.XContainer.Elements%2A> <xref:System.Xml.Linq.XContainer.Elements%2A>作为具有延迟执行的迭代器实现。</xref:System.Xml.Linq.XContainer.Elements%2A> 这意味着它除了循环访问链接列表外还执行一些操作，例如分配迭代器对象和跟踪执行状态。 此项工作可以分为两类：设置迭代器时完成的工作和每次迭代过程中完成的工作。 设置工作是固定的少量工作，而每次迭代过程中完成的工作与源集合中的项数成正比。  
  
-   在`query1`、`Where`子句将使查询调用<xref:System.Linq.Enumerable.Where%2A>方法。</xref:System.Linq.Enumerable.Where%2A> 此方法也作为迭代器实现。 设置工作包括实例化将引用 lambda 表达式的委托和对迭代器的常规设置。 每次迭代时，都将调用该委托以执行谓词。 设置工作和每次迭代过程中完成的工作类似于循环访问轴期间完成的工作。  
  
-   在`query1`，select 子句将使查询调用<xref:System.Linq.Enumerable.Select%2A>方法。</xref:System.Linq.Enumerable.Select%2A> 此方法具有相同的性能配置文件作为<xref:System.Linq.Enumerable.Where%2A>方法。</xref:System.Linq.Enumerable.Where%2A>  
  
-   `query2` 中的 `Where` 子句和 `Select` 子句与 `query1` 中的相应语句具有相同的性能配置文件。  
  
 因此，通过 `query2` 执行的迭代与第一个查询源中的项数（即，线形时间）成正比。  
  
## <a name="see-also"></a>另请参阅  
 [性能 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/performance-linq-to-xml.md)

