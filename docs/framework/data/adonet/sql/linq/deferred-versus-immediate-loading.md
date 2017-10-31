---
title: "延迟加载与立即加载 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d1d7247f-a3b7-460b-b342-5c1a2365aa1a
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 延迟加载与立即加载
查询某对象时，实际上您只检索请求的对象。  不会同时自动获取相关对象。  （有关详细信息，请参阅 [跨关系查询](../../../../../../docs/framework/data/adonet/sql/linq/querying-across-relationships.md)。）您无法看到相关对象尚未加载这一事实，原因是尝试访问它们时将产生检索它们的请求。  
  
 例如，您可能需要查询一组特定的订单，然后偶而向特定客户发送电子邮件通知。  您最初不一定需要检索与每个订单有关的所有客户数据。  您可以使用延迟加载将额外信息的检索操作延迟到您确实需要检索它们时再进行。  请看下面的示例：  
  
 [!code-csharp[DLinqQueryConcepts#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#1)]
 [!code-vb[DLinqQueryConcepts#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#1)]  
  
 反过来也可能是可行的。  您的应用程序可能必须同时查看客户数据和订单数据。  您了解同时需要这两组数据。  您了解一旦获得结果，您的应用程序就需要每个客户的订单信息。  您不希望一个一个地提交对每个客户的订单的查询。  您真正想要的是将订单数据与客户信息一起检索出来。  
  
 [!code-csharp[DLinqQueryConcepts#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQueryConcepts/cs/Program.cs#2)]
 [!code-vb[DLinqQueryConcepts#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQueryConcepts/vb/Module1.vb#2)]  
  
 您还可以在查询中联接客户和订单，方法是构建叉积并将所有相关数据位作为一个大型投影检索出来。  但这些结果并非实体。  有关更多信息，请参见 [LINQ to SQL 对象模型](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)。  实体是具有标识且您可以修改的对象，而这些结果将是无法更改和持久化的投影。  更糟的是，您将检索到大量的冗余数据，因为在平展联接输出中，对于每个订单，每个客户将重复出现。  
  
 您真正需要的是同时检索相关对象的集合的方法。  此集合是关系图的精确剖面，因此您检索到的数据绝不会比您所需要的数据多或少。  为此，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 提供了 <xref:System.Data.Linq.DataLoadOptions>，用以立即加载对象模型的某一区域。  方法包括：  
  
-   <xref:System.Data.Linq.DataLoadOptions.LoadWith%2A> 方法，用于立即加载与主目标相关的数据。  
  
-   <xref:System.Data.Linq.DataLoadOptions.AssociateWith%2A> 方法，用于筛选为特定关系检索到的对象。  
  
## 请参阅  
 [查询概念](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)