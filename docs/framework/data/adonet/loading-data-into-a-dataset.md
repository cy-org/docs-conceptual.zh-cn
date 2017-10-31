---
title: "向数据集中加载数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a53e5dc1-9669-49d4-828d-efa633237066
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 向数据集中加载数据
<xref:System.Data.DataSet> 对象只有在填充后才能使用 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 进行查询。  填充 <xref:System.Data.DataSet> 有多种不同的方式。  例如，您可以使用 [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] 来查询数据库并将结果加载到 <xref:System.Data.DataSet> 中。  有关详细信息，请参阅[LINQ to SQL](../../../../docs/framework/data/adonet/sql/linq/index.md)。  
  
 另一种将数据加载到 <xref:System.Data.DataSet> 中的常见方式是使用 <xref:System.Data.Common.DataAdapter> 类从数据库中检索数据。  下面的示例阐释了这一过程。  
  
## 示例  
 此示例使用 <xref:System.Data.Common.DataAdapter> 查询 AdventureWorks 数据库中从 2002 年起的销售信息，并将结果加载到 <xref:System.Data.DataSet> 中。  填充 <xref:System.Data.DataSet> 以后，可以通过使用 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 对其编写查询。  [LINQ to DataSet 示例](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md)的示例查询中使用了本示例中的 `FillDataSet` 方法。  有关详细信息，请参阅[查询数据集](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md)。  
  
 [!code-csharp[DP LINQ to DataSet Examples#FillDataSet](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#filldataset)]
 [!code-vb[DP LINQ to DataSet Examples#FillDataSet](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#filldataset)]  
  
## 请参阅  
 [LINQ to DataSet 概述](../../../../docs/framework/data/adonet/linq-to-dataset-overview.md)   
 [查询数据集](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md)   
 [LINQ to DataSet 示例](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md)