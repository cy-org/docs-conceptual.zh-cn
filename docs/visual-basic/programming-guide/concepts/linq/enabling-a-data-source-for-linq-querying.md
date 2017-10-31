---
title: "LINQ Querying2 上启用了数据源 |Microsoft 文档"
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
ms.assetid: c412f0cf-ff0e-4993-ab3d-1b49e23f00f8
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 34bdc4e056d982799eac35eb2398dd3f23f6f351
ms.lasthandoff: 03/13/2017

---
# <a name="enabling-a-data-source-for-linq-querying"></a>启用数据源以进行 LINQ 查询
有多种方法来扩展[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]若要启用任何数据源进行查询[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]模式。 数据源可以是数据结构、Web 服务、文件系统或数据库等。 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 模式使客户端可以轻松地查询能够进行 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询的数据源，因为查询的语法和模式没有更改。 在哪些方面[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]可以扩展到这些数据源，其中包括︰  
  
-   实现<xref:System.Collections.Generic.IEnumerable%601>界面中键入内容以启用[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]向对象查询该类型。</xref:System.Collections.Generic.IEnumerable%601>  
  
-   创建标准查询运算符方法如<xref:System.Linq.Enumerable.Where%2A>和<xref:System.Linq.Enumerable.Select%2A>可扩展某个类型，以使自定义[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查询该类型。</xref:System.Linq.Enumerable.Select%2A> </xref:System.Linq.Enumerable.Where%2A>  
  
-   创建的提供程序的数据源中实现<xref:System.Linq.IQueryable%601>接口。</xref:System.Linq.IQueryable%601> 实现此接口的提供程序以表达式树的形式接收 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询，提供程序能够以自定义方式（例如以远程方式）执行该查询。  
  
-   创建一个您充分利用现有的数据源提供[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]技术。 这种提供程序不仅能够进行查询，而且能够为用户定义的类型插入、更新和删除操作及映射。  
  
 本主题将讨论这些选项。  
  
## <a name="how-to-enable-linq-querying-of-your-data-source"></a>如何使 LINQ 能够查询您的数据源  
  
### <a name="in-memory-data"></a>内存中的数据  
 有两种方法可以启用[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]内存中数据的查询。 如果数据类型实现的<xref:System.Collections.Generic.IEnumerable%601>，您可以通过查询数据[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]的对象。</xref:System.Collections.Generic.IEnumerable%601> 如果它不会毫无意义，若要通过实现启用类型枚举<xref:System.Collections.Generic.IEnumerable%601>接口，您可以定义[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]标准查询运算符方法，该类型中的，或者创建[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]可扩展该类型的标准查询运算符方法。</xref:System.Collections.Generic.IEnumerable%601> 标准查询运算符的自定义实现应使用延迟执行来返回结果。  
  
### <a name="remote-data"></a>远程数据  
 启用的最佳选项[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查询远程数据源是实现<xref:System.Linq.IQueryable%601>接口。</xref:System.Linq.IQueryable%601> 但是，这与为数据源扩展提供程序（比如 [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)]）有所不同。 没有用于扩展现有的提供程序模型[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]技术，如[!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)]为其他类型的数据源位于[!INCLUDE[vs_orcas_long](../../../../csharp/misc/includes/vs_orcas_long_md.md)]。  
  
## <a name="iqueryable-linq-providers"></a>IQueryable LINQ 提供程序  
 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]提供程序实现<xref:System.Linq.IQueryable%601>范围很广的其复杂程度。</xref:System.Linq.IQueryable%601> 本节讨论这些不同程度的复杂性。  
  
 复杂性较低的 `IQueryable` 提供程序可与 Web 服务的一个方法交互。 这种类型的提供程序非常具体，因为它需要所处理的查询中有具体信息。 它有封闭的类型系统，可能会公开单一结果类型。 执行查询的大多数都是在本地，例如通过使用<xref:System.Linq.Enumerable>标准查询运算符的实现。</xref:System.Linq.Enumerable> 复杂性较低的提供程序可能只会检查表示查询的表达式树中的一个方法调用表达式，并允许在其他地方处理查询的其余逻辑。  
  
 中等复杂性的 `IQueryable` 提供程序可能针对具有部分可表达查询语言的数据源。 如果该提供程序针对 Web 服务，它可以与 Web 服务的多个方法进行交互，并基于查询提出的问题选择要调用的方法。 与简单提供程序相比，中等复杂性的提供程序的类型系统较丰富，但它仍然是固定类型系统。 例如，提供程序可以公开具有可遍历的一对多关系的类型，但将不会为用户定义的类型提供映射技术。  
  
 复杂的 `IQueryable` 提供程序（如 [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)] 提供程序）可将完整的 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 查询转换为可表达查询语言（如 SQL）。 与复杂性较低的提供程序相比，复杂的提供程序更为全面，因为它能在查询中处理各种各样的问题。 它还具有开放的类型系统，因而必须包含广泛的基础结构来映射用户定义的类型。 开发复杂的提供程序需要耗费大量的精力。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Linq.IQueryable%601></xref:System.Linq.IQueryable%601>   
 <xref:System.Collections.Generic.IEnumerable%601></xref:System.Collections.Generic.IEnumerable%601>   
 <xref:System.Linq.Enumerable></xref:System.Linq.Enumerable>   
 [标准查询运算符概述 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [LINQ to Objects (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)
