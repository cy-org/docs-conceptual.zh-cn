---
title: "使用 Web 服务的 LINQ to SQL N 层 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9cb10eb8-957f-4beb-a271-5f682016fed2
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 使用 Web 服务的 LINQ to SQL N 层
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 特别针对在松耦合数据访问层 \(DAL\) 的中间层（如 Web 服务）上使用而设计。  如果表示层为 ASP.NET 网页，则使用 <xref:System.Web.UI.WebControls.LinqDataSource> Web 服务器控件管理用户界面与中间层上的 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 之间的数据传输。  如果表示层不是 ASP.NET 页，则中间层和表示层都必须执行一些附加工作以管理数据的序列化和反序列化。  
  
## 在中间层上设置 LINQ to SQL  
 在 Web 服务或 n 层应用程序中，中间层包含数据上下文和实体类。  可以手动创建这些类，或是按照文档中其他部分的说明使用 SQLMetal.exe 或[!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)]创建。  在设计时，您可以选择使实体类可序列化。  有关详细信息，请参阅[如何：使实体可序列化](../../../../../../docs/framework/data/adonet/sql/linq/how-to-make-entities-serializable.md)。  也可以选择创建包装要序列化的数据的一组单独类，然后当在 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 查询中返回数据时投射到这些可序列化类型中。  
  
 随后可以使用客户端为进行检索、插入和更新数据而调用的方法来定义接口。  这些接口方法包装 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 查询。  可以使用任何类型的序列化机制处理远程方法调用和数据的序列化。  唯一的要求是如果您的对象模型中具有循环或双向关系（如标准 Northwind 对象模型中的 Customers 与 Orders 之间的关系），则必须使用支持这种关系的序列化程序。  Windows Communication Foundation \(WCF\) <xref:System.Runtime.Serialization.DataContractSerializer> 支持双向关系，但是使用非 WCF Web 服务的 XmlSerializer 不支持这种关系。如果您选择使用 XmlSerializer，则必须确保您的对象模型没有循环关系。  
  
 有关 Windows Communication Foundation 的更多信息，请参见 [Windows Communication Foundation Services and WCF Data Services in Visual Studio](../Topic/Windows%20Communication%20Foundation%20Services%20and%20WCF%20Data%20Services%20in%20Visual%20Studio.md)。  
  
 通过使用 <xref:System.Data.Linq.DataContext> 和实体类上的分部类和方法挂钩到 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 运行时事件，来实现您的业务规则或其他特定于域的逻辑。  有关详细信息，请参阅[实现 N 层业务逻辑](../../../../../../docs/framework/data/adonet/sql/linq/implementing-business-logic-linq-to-sql.md)。  
  
## 定义可序列化类型  
 客户端或表示层必须具有将从中间层接收的用于类的类型定义。  这些类型可能为实体类本身，或是仅包装实体类中的特定字段以进行远程处理的特殊类。  在任何情况下，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 都完全不涉及表示层获取这些类型定义的方式。  例如，表示层可以使用 WCF 自动生成类型，也可以具有在其中定义这些类型的 DLL 的副本，还可以仅定义其自己的类型版本。  
  
## 检索和插入数据  
 中间层会定义一个接口，用于指定表示层访问数据的方式。  例如 `GetProductByID(int productID)` 或 `GetCustomers()`。  在中间层上，方法体通常创建 <xref:System.Data.Linq.DataContext> 的新实例，对其一个或多个表执行查询。  随后中间层会返回结果作为 <xref:System.Collections.Generic.IEnumerable%601>，其中 `T` 为实体类或用于序列化的另一个类型。  表示层从不直接向中间层发送查询变量，也从不直接从中间层接收查询变量。  这两个层交换值、对象和具体数据的集合。  在已接收到一个集合后，如有必要，表示层可以使用 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] to Objects 查询该集合。  
  
 在插入数据时，表示层可以构造一个新的对象并将其发送到中间层，或是使中间层基于其提供的值来构造对象。  通常，在 n 层应用程序中检索和插入数据与 2 层应用程序中的过程并无显著差异。  有关详细信息，请参阅[查询数据库](../../../../../../docs/framework/data/adonet/sql/linq/querying-the-database.md)和[生成和提交数据更改](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md)。  
  
## 跟踪更新和删除的更改  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 支持基于时间戳（也称为 RowVersion）和基于原始值的开放式并发。  如果数据库表具有时间戳，则更新和删除几乎不需要在中间层或表示层上进行额外工作。  但是，如果必须使用原始值进行开放式并发检查，则表示层在其进行更新时负责跟踪这些值并将这些值发送回去。  这是因为在表示层上对实体所做的更改不会在中间层上进行跟踪。  实际上，实体的原始检索以及对其所进行的最终更新通常由 <xref:System.Data.Linq.DataContext> 的两个完全独立的实例执行。  
  
 表示层进行的更改越多，跟踪这些更改以及将这些更改打包发送回中间层的过程就越复杂。  传达更改的机制的实现完全由应用程序负责。  唯一的要求是必须为 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 提供进行开放式并发检查所必需的那些原始值。  
  
 有关详细信息，请参阅[N 层应用程序中的数据检索和 CUD 操作 \(LINQ to SQL\)](../../../../../../docs/framework/data/adonet/sql/linq/data-retrieval-and-cud-operations-in-n-tier-applications.md)。  
  
## 请参阅  
 [使用 LINQ to SQL 的 N 层应用程序和远程应用程序](../../../../../../docs/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql.md)   
 [NIB: LinqDataSource Web Server Control Overview](http://msdn.microsoft.com/zh-cn/104cfc3f-7385-47d3-8a51-830dfa791136)