---
title: "添加 DataRelation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a4a564fb-c1c4-4135-b6c2-b030e51195e4
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 添加 DataRelation
在包含多个 <xref:System.Data.DataTable> 对象的 <xref:System.Data.DataSet> 中，可以使用 <xref:System.Data.DataRelation> 对象来使一个表与另一个表相关，在多个表之间导航，以及从相关表中返回子行或父行。  
  
 创建 **DataRelation** 所需的参数是所创建的 **DataRelation** 的名称以及对用作关系中父列和子列的那些列的一个或多个 <xref:System.Data.DataColumn> 引用的数组。  当创建 **DataRelation** 后，可以使用它在多个表之间导航和检索值。  
  
 默认情况下，向 <xref:System.Data.DataSet> 中添加 **DataRelation** 会将一个 <xref:System.Data.UniqueConstraint> 添加到父表中并将一个 <xref:System.Data.ForeignKeyConstraint> 添加到子表中。  有关这些默认约束的更多信息，请参见[数据表约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-constraints.md)。  
  
 以下代码示例使用 <xref:System.Data.DataSet> 中的两个 <xref:System.Data.DataTable> 对象来创建一个 **DataRelation**。  每个 <xref:System.Data.DataTable> 包含一个名为 **CustID** 的列，它用作两个 <xref:System.Data.DataTable> 对象之间的链接。  该示例将单个 **DataRelation** 添加到 <xref:System.Data.DataSet> 的 **Relations** 集合中。  该示例中的第一个参数指定所创建的 **DataRelation** 的名称。  第二个参数设置父 **DataColumn**，第三个参数设置子 **DataColumn**。  
  
```vb  
customerOrders.Relations.Add("CustOrders", _  
  customerOrders.Tables("Customers").Columns("CustID"), _  
  customerOrders.Tables("Orders").Columns("CustID"))  
```  
  
```csharp  
customerOrders.Relations.Add("CustOrders",  
  customerOrders.Tables["Customers"].Columns["CustID"],  
  customerOrders.Tables["Orders"].Columns["CustID"]);  
```  
  
 **DataRelation** 也具有 **Nested** 属性，如果该属性设置为 **true**，则来自子表的行会在使用 <xref:System.Data.DataSet.WriteXml%2A> 以 XML 元素形式编写时嵌套在来自父表的关联行中。  有关详细信息，请参阅[在 DataSet 中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)。  
  
## 请参阅  
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)