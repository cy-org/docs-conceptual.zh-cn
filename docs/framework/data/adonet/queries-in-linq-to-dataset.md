---
title: "LINQ to DataSet 中的查询 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c1a78fa8-9f0c-40bc-a372-5575a48708fe
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# LINQ to DataSet 中的查询
查询是一种从数据源检索数据的表达式。  查询通常用专用查询语言表示，如用于关系数据库的 SQL 和用于 XML 的 XQuery。  因此，开发人员对于他们查询的每种类型的数据源或数据格式，都不得不学习一种新的查询语言。  [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] 提供了一种较为简单的一致模型，适用于各种数据源和格式的数据。  在 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 查询中，您始终使用编程对象。  
  
 一个 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 查询操作包含三个操作：获取数据源、创建查询和执行查询。  
  
 实现 <xref:System.Collections.Generic.IEnumerable%601> 泛型接口的数据源可以通过 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 进行查询。  对 <xref:System.Data.DataTable> 调用 <xref:System.Data.DataTableExtensions.AsEnumerable%2A> 将返回实现泛型 <xref:System.Collections.Generic.IEnumerable%601> 接口的对象，作为 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询的数据源。  
  
 在查询中，您可以确切指定要从数据源检索哪些信息。  查询也可以指定返回信息之前信息的排序、分组和表现方式。  在 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 中，查询存储在变量中。  如果查询旨在返回一系列值，则查询变量本身也必须为可枚举类型。  此查询变量不执行任何操作，也不返回任何数据；它只存储查询信息。  创建查询后必须执行该查询以检索任何数据。  
  
 在返回一系列值的查询中，查询变量本身从不保存查询结果，它只存储查询命令。  查询的执行将推迟到在 `foreach` 或 `For Each` 循环中循环访问查询变量之后进行。  这称为“延迟执行”；也就是说，查询将会在构造之后的某个时间执行。  这意味着您可以根据需要频繁地执行查询。  例如，当您的数据库由其他应用程序不断更新时，此功能将会很有用。  在您的应用程序中，您可以创建查询以检索最新信息并重复执行查询，每次返回更新的信息。  
  
 与返回一系列值的延迟查询相反，返回单一实例值的查询将立即执行。  <xref:System.Linq.Enumerable.Count%2A>、<xref:System.Linq.Enumerable.Max%2A>、<xref:System.Linq.Enumerable.Average%2A> 和 <xref:System.Linq.Enumerable.First%2A> 是单一实例查询的一些示例。  因为需要查询结果来计算单一实例结果，因此这些查询将会立即执行。  例如，若要计算查询结果的平均值，则必须执行查询，以便求平均值函数具有要使用的输入数据。  您也可以对查询使用 <xref:System.Linq.Enumerable.ToList%2A> 或 <xref:System.Linq.Enumerable.ToArray%2A> 方法以强制立即执行不生成单一实例值的查询。  当想要缓存查询结果时，这些强制立即执行的技术可能会很有用。  有关延迟和立即执行查询的更多信息，请参见 [Getting Started with LINQ](http://msdn.microsoft.com/zh-cn/6cc9af04-950a-4cc3-83d4-2aeb4abe4de9)。  
  
## 查询  
 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询可以使用两种不同的语法进行表述：查询表达式语法和基于方法的查询语法。  
  
### 查询表达式语法  
 查询表达式是一种声明性查询语法。  此语法使开发人员能够以类似于 SQL 的格式用 C\# 或 Visual Basic 编写查询。  通过使用查询表达式语法，您可以用最少的代码对数据源执行复杂的筛选、排序和分组操作。  有关详细信息，请参阅[LINQ 查询表达式](../Topic/LINQ%20Query%20Expressions%20\(C%23%20Programming%20Guide\).md)和[基本查询操作 \(Visual Basic\)](../Topic/Basic%20Query%20Operations%20\(Visual%20Basic\).md)。  
  
 查询表达式语法是 C\# 3.0 和 [!INCLUDE[vb_orcas_long](../../../../includes/vb-orcas-long-md.md)] 中的新功能。  不过，[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 公共语言运行库 \(CLR\) 无法读取查询表达式语法本身。  因此，在编译时，查询表达式将转换为 CLR 能理解的形式，即方法调用。  这些方法称为“标准查询运算符”。  作为开发人员，您可以选择使用方法语法而不使用查询语法直接调用这些方法。  有关详细信息，请参阅[Query Syntax and Method Syntax in LINQ](../Topic/Query%20Syntax%20and%20Method%20Syntax%20in%20LINQ%20\(C%23\).md)。  有关如何使用标准查询运算符的更多信息，请参见 [NOT IN BUILD: LINQ General Programming Guide](http://msdn.microsoft.com/zh-cn/609c7a6b-cbdd-429d-99f3-78d13d3bc049)。  
  
 下面的示例使用 <xref:System.Linq.Enumerable.Select%2A> 返回 `Product` 表中的所有行并显示产品名称。  
  
 [!code-csharp[DP LINQ to DataSet Examples#SelectSimple1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#selectsimple1)]
 [!code-vb[DP LINQ to DataSet Examples#SelectSimple1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#selectsimple1)]  
  
### 基于方法的查询语法  
 表述 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询的另一种方法是使用基于方法的查询。  基于方法的查询语法是对 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 运算符方法的一系列直接方法调用，将 Lambda 表达式作为参数进行传递。  有关详细信息，请参阅[Lambda 表达式](../Topic/Lambda%20Expressions%20\(C%23%20Programming%20Guide\).md)。  
  
 此示例使用 <xref:System.Linq.Enumerable.Select%2A> 返回 `Product` 中的所有行并显示产品名称。  
  
 [!code-csharp[DP LINQ to DataSet Examples#SelectAnonymousTypes_MQ](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#selectanonymoustypes_mq)]
 [!code-vb[DP LINQ to DataSet Examples#SelectAnonymousTypes_MQ](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#selectanonymoustypes_mq)]  
  
## 编写查询  
 如本主题前面所述，当查询旨在返回一系列值时，查询变量本身只存储查询命令。  如果查询不包含可使查询立即执行的方法，则查询的实际执行将会推迟，直到在 `foreach` 或 `For Each` 循环中循环访问查询变量。  延迟执行可使多个查询组合在一起或使查询得到扩展。  扩展查询时，将修改查询以包括新操作，最终执行将反映这些更改。  在下面的示例中，第一个查询返回所有产品。  第二个查询通过使用 `Where` 扩展第一个查询，以返回大小为“L”的所有产品：  
  
 [!code-csharp[DP LINQ to DataSet Examples#Composing](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#composing)]
 [!code-vb[DP LINQ to DataSet Examples#Composing](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#composing)]  
  
 执行一个查询后，不会再编写其他查询，并且所有后续查询都将使用驻留在内存中的 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 运算符。  当在 `foreach` 或 `For Each` 语句中循环访问查询变量或通过调用可导致立即执行的 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 转换运算符之一时，查询将会开始执行。  这些运算符包括：<xref:System.Linq.Enumerable.ToList%2A>、<xref:System.Linq.Enumerable.ToArray%2A>、<xref:System.Linq.Enumerable.ToLookup%2A> 和 <xref:System.Linq.Enumerable.ToDictionary%2A>。  
  
 在下面的示例中，第一个查询返回按定价排序的所有产品。  <xref:System.Linq.Enumerable.ToArray%2A> 方法用于强制立即执行查询：  
  
 [!code-csharp[DP LINQ to DataSet Examples#ToArray2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#toarray2)]
 [!code-vb[DP LINQ to DataSet Examples#ToArray2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#toarray2)]  
  
## 请参阅  
 [编程指南](../../../../docs/framework/data/adonet/programming-guide-linq-to-dataset.md)   
 [查询数据集](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md)   
 [Getting Started with LINQ in C\#](../Topic/Getting%20Started%20with%20LINQ%20in%20C%23.md)   
 [Getting Started with LINQ in Visual Basic](../Topic/Getting%20Started%20with%20LINQ%20in%20Visual%20Basic.md)