---
title: "导航 DataRelation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5e673f4-9b44-45ae-aaea-c504d1cc5d3e
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 导航 DataRelation
<xref:System.Data.DataRelation> 的一项主要功能就是在 <xref:System.Data.DataSet> 中从一个 <xref:System.Data.DataTable> 浏览到另一个。  它使您能够在给定相关 **DataTable** 中的单个 **DataRow** 的情况下检索一个 **DataTable** 中的所有相关 <xref:System.Data.DataRow> 对象。  例如，当建立客户表和订单表之间的 **DataRelation** 后，可以使用 **GetChildRows** 检索特定客户行的所有订单行。  
  
 以下代码示例创建 **DataSet** 的 **Customers** 表和 **Orders** 表之间的 **DataRelation**，并返回每个客户的所有订单。  
  
 [!code-csharp[DataWorks Data.DataTableRelation#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableRelation/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableRelation#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableRelation/VB/source.vb#1)]  
  
 下一示例以上例为基础，将四个表关联在一起，并浏览这些关系。  如上例所示，**CustomerID** 使 **Customers** 表与 **Orders** 表相关联。  对于 **Customers** 表中的每个客户，将确定 **Orders** 表中的所有子行，以返回特定客户的订单数以及他们的 **OrderID** 值。  
  
 该扩展示例还将返回 **OrderDetails** 表和 **Products** 表中的值。  **Orders** 表使用 **OrderID** 与 **OrderDetails** 表相关联，以确定在每一客户订单中订购的产品及数量。  由于 **OrderDetails** 表只包含已订购产品的 **ProductID**，**OrderDetails** 将使用 **ProductID** 与 **Products** 相关联，以返回 **ProductName**。  在这一关系中，**Products** 表为父表，而 **Order Details** 表为子表。  因此，当循环访问 **OrderDetails** 表时，将调用 **GetParentRow** 来检索相关的 **ProductName** 值。  
  
 请注意，当为 **Customers** 表和 **Orders** 表创建 **DataRelation** 时，没有为 **createConstraints** 标志指定任何值（默认为 **true**）。  它假定 **Orders** 表中的所有行都具有一个存在于父 **Customers** 表中的 **CustomerID** 值。  如果 **CustomerID** 存在于 **Customers** 表之外的 **Orders** 表中，则 <xref:System.Data.ForeignKeyConstraint> 将引发异常。  
  
 如果子列可能包含父列不包含的值，添加 **DataRelation** 时请将 **createConstraints** 标志设置为 **false**。  在该示例中，对于 **Orders** 表和 **OrderDetails** 表之间的 **DataRelation**，**createConstraints** 标志将设置为 **false**。  这样，应用程序就可以返回 **OrderDetails** 表中的所有记录并只返回 **Orders** 表中记录的子集，而不会生成运行时异常。  该扩展示例生成以下格式的输出。  
  
```  
Customer ID: NORTS  
  Order ID: 10517  
        Order Date: 4/24/1997 12:00:00 AM  
           Product: Filo Mix  
          Quantity: 6  
           Product: Raclette Courdavault  
          Quantity: 4  
           Product: Outback Lager  
          Quantity: 6  
  Order ID: 11057  
        Order Date: 4/29/1998 12:00:00 AM  
           Product: Outback Lager  
          Quantity: 3  
```  
  
 以下代码示例是一个扩展示例，在该示例中将返回 **OrderDetails** 表和 **Products** 表中的值，并只返回 **Orders** 表中记录的子集。  
  
 [!code-csharp[DataWorks Data.DataTableNavigation#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableNavigation/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableNavigation#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableNavigation/VB/source.vb#1)]  
  
## 请参阅  
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)