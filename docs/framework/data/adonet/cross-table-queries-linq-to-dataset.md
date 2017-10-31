---
title: "交叉表查询 (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6819a16f-8656-41af-a54d-dfec0cb66366
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 交叉表查询 (LINQ to DataSet)
除了查询单个表外，也可以在 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 中执行交叉表查询。这可以通过使用联接来完成。  联接就是将一个数据源中的对象与另一个数据源中具有相同公共属性的对象（例如产品或联系人 ID）相关联。  在面向对象的编程中，由于每个对象都有引用另一个对象的成员，所以对象间的关系相对较容易导航。但在外部数据库表中，导航关系不像这样简单。  数据库表不包含内置关系。在这些情况下，可以通过联接操作来匹配每个源中的元素。  例如，假设有两个分别包含产品信息和销售信息的表，您可以使用联接操作来匹配同一销售订单的销售信息和产品。  
  
 [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] 框架提供两个联接运算符：<xref:System.Linq.Enumerable.Join%2A> 和 <xref:System.Linq.Enumerable.GroupJoin%2A>。这些运算符执行同等联接：即仅在键相等时匹配两个数据源的联接。  （相对而言，[!INCLUDE[tsql](../../../../includes/tsql-md.md)] 支持 `equals` 以外的其他连接运算符，如 `less than` 运算符）。  
  
 对于关系数据库，<xref:System.Linq.Enumerable.Join%2A> 实现内部联接。  内部联接是仅返回在相对数据集中具有匹配对象的那些对象的一种联接类型。  
  
 对于关系数据库，<xref:System.Linq.Enumerable.GroupJoin%2A> 运算符没有直接等效项，它们实现内部联接和左外部联接的超集。左外部联接是一种即使在第二个集合中没有关联元素的情况下也会返回第一个（左侧）集合中每个元素的联接。  
  
 有关联接的更多信息，请参见[Join Operations](../../../../ocs/visual-basic/programming-guide/concepts/linq/join-operations.md)。  
  
## 示例  
 下面的示例对 AdventureWorks 示例数据库中的 `SalesOrderHeader` 和 `SalesOrderDetail` 表执行传统联接以获取 8 月份以来的在线订单。  
  
 [!code-csharp[DP LINQ to DataSet Examples#Join](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#join)]
 [!code-vb[DP LINQ to DataSet Examples#Join](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#join)]  
  
## 请参阅  
 [查询数据集](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md)   
 [单表查询](../../../../docs/framework/data/adonet/single-table-queries-linq-to-dataset.md)   
 [查询类型化数据集](../../../../docs/framework/data/adonet/querying-typed-datasets.md)   
 [Join Operations](../../../../ocs/visual-basic/programming-guide/concepts/linq/join-operations.md)   
 [LINQ to DataSet 示例](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md)