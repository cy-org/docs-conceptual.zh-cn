---
title: "LINQ to DataSet 概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dc20a8fb-03f6-4b68-9c2b-7f7299e3070b
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# LINQ to DataSet 概述
<xref:System.Data.DataSet> 是更为广泛使用的 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 组件之一。 它是 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 所基于的断开连接式编程模型的关键元素，使用它可以显式缓存不同数据源中的数据。 在表示层上，<xref:System.Data.DataSet> 与 GUI 控件紧密集成，以进行数据绑定。 在中间层上，它提供保留数据关系形状的缓存并包括快速简单查询和层次结构导航服务。  用于减少对数据库的请求数的常用技术是使用 <xref:System.Data.DataSet> 以便在中间层进行缓存。  例如，考虑数据驱动的 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Web 应用程序。  通常，应用程序的绝大部分数据不会经常更改，属于会话之间或用户之间的公共数据。  此数据可以保存在 Web 服务器的内存中，这会减少对数据库的请求数并加速用户的交互。  <xref:System.Data.DataSet> 的另一个有用特征是允许应用程序将数据子集从一个或多个数据源导入应用程序空间。  然后，应用程序可以在内存中操作这些数据，同时保留其关系形状。  
  
 <xref:System.Data.DataSet> 虽然具有突出的优点，但其查询功能也存在限制。  <xref:System.Data.DataTable.Select%2A> 方法可用于筛选和排序，<xref:System.Data.DataRow.GetChildRows%2A> 和 <xref:System.Data.DataRow.GetParentRow%2A> 方法可用于层次结构导航。  但对于更复杂的情况，开发人员必须编写自定义查询。  这会使应用程序性能低下并且难以维护。  
  
 使用 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 可以更快更容易地查询在 <xref:System.Data.DataSet> 对象中缓存的数据。  这些查询用编程语言本身表示，而不表示为嵌入在应用程序代码中的字符串。  这意味着开发人员不必学习单独的查询语言。  此外，[!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 可使 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 开发人员的工作效率更高，因为 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] IDE 提供编译时语法检查、静态类型化和对 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 的 IntelliSense 支持。  [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 也可用于查询从一个或多个数据源合并的数据。  这可以使许多需要灵活表示和处理数据的方案能够实现。  具体地说，一般报告、分析和业务智能应用程序将需要这种操作方法。  
  
## 使用 LINQ to DataSet 查询数据集  
 只有在填充 <xref:System.Data.DataSet> 后，您才能开始使用 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 来查询 <xref:System.Data.DataSet> 对象。 向 <xref:System.Data.DataSet> 中加载数据有多种方法，如使用 <xref:System.Data.Common.DataAdapter> 类或 [LINQ to SQL](../../../../docs/framework/data/adonet/sql/linq/index.md)。  将数据加载到 <xref:System.Data.DataSet> 对象后，可以开始查询数据。  使用 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 来表述查询类似于对其他启用 [!INCLUDE[vbteclinqext](../../../../includes/vbteclinqext-md.md)] 的数据源使用 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)]。  [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 查询可以对 <xref:System.Data.DataSet> 中的单个表执行，也可以通过使用 <xref:System.Linq.Enumerable.Join%2A> 和 <xref:System.Linq.Enumerable.GroupJoin%2A> 标准查询运算符对多个表执行。  
  
 支持对类型化和非类型化 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 对象执行 <xref:System.Data.DataSet> 查询。  如果在应用程序设计时已知 <xref:System.Data.DataSet> 的架构，则建议使用类型化 <xref:System.Data.DataSet>。 在类型化 <xref:System.Data.DataSet> 中，表和行对每个列都具有类型化成员，从而使查询更简单并且更具可读性。  
  
 除了 System.Core.dll 中实现的标准查询运算符外，[!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 还添加了多种 <xref:System.Data.DataSet> 特定扩展，从而可以更容易地查询一组 <xref:System.Data.DataRow> 对象。  这些 <xref:System.Data.DataSet> 特定扩展包括用于比较行序列的运算符以及用于访问 <xref:System.Data.DataRow> 的列值的方法。  
  
## N 层应用程序和 LINQ to DataSet  
 N 层数据应用程序是以数据为中心的应用程序，分为多个逻辑层（或层）。  典型的 N 层应用程序包括一个表示层、一个中间层和一个数据层。  将应用程序组件分离到不同的层可提高应用程序的可维护性和可伸缩性。  有关 N 层数据应用程序的更多信息，请参见 [在 N 层应用程序中使用数据集](../Topic/Work%20with%20datasets%20in%20n-tier%20applications.md)。  
  
 在 N 层应用程序中，<xref:System.Data.DataSet> 通常用于中间层以缓存 Web 应用程序的信息。  [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询功能通过扩展方法实现，并扩展现有的 ADO.NET 2.0 <xref:System.Data.DataSet>。  
  
## 请参阅  
 [查询数据集](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [LINQ to SQL](../../../../docs/framework/data/adonet/sql/linq/index.md)