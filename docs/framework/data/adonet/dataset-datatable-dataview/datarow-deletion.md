---
title: "DataRow 删除 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c34f531d-4b9b-4071-b2d7-342c402aa586
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# DataRow 删除
可以使用两个方法从 <xref:System.Data.DataTable> 对象删除 <xref:System.Data.DataRow> 对象：<xref:System.Data.DataRowCollection> 对象的 **Remove** 方法，以及 **DataRow** 对象的 <xref:System.Data.DataRow.Delete%2A> 方法。  <xref:System.Data.DataRowCollection.Remove%2A> 方法从 **DataRowCollection** 删除了 **DataRow**，而 <xref:System.Data.DataRow.Delete%2A> 方法仅标记要删除的行。  当应用程序调用 **AcceptChanges** 方法时，才会发生实际的删除。  通过使用 <xref:System.Data.DataRow.Delete%2A>，您可以在实际删除行之前，先以编程方式来检查哪些行已标记为删除。  如果将行标记为删除，则该行的 <xref:System.Data.DataRow.RowState%2A> 属性会设置为 <xref:System.Data.DataRow.Delete%2A>。  
  
 在 foreach 循环中，不会调用 <xref:System.Data.DataRow.Delete%2A> 和 <xref:System.Data.DataRowCollection.Remove%2A>，而是循环访问 <xref:System.Data.DataRowCollection> 对象。  <xref:System.Data.DataRow.Delete%2A> 和 <xref:System.Data.DataRowCollection.Remove%2A> 不会修改该集合的状态。  
  
 在将 <xref:System.Data.DataSet> 或 **DataTable** 与 **DataAdapter** 和关系型数据源一起使用时，用 **DataRow** 的 **Delete** 方法移除行。  **Delete** 方法只是在 **DataSet** 或 **DataTable** 中将行标记为 **Deleted**，而不会移除它。  而 **DataAdapter** 在遇到标记为 **Deleted** 的行时，会执行其 **DeleteCommand** 方法以在数据源中删除该行。  然后，就可以用 **AcceptChanges** 方法永久移除该行。  如果使用 **Remove** 删除该行，则该行将从表中完全移除，但 **DataAdapter** 不会在数据源中删除该行。  
  
 **DataRowCollection** 的 **Remove** 方法采用 **DataRow** 作为参数，并将其从集合中移除，如下例所示。  
  
```vb  
workTable.Rows.Remove(workRow)  
  
```  
  
```csharp  
workTable.Rows.Remove(workRow);  
```  
  
 作为对比，以下示例演示了如何调用 **DataRow** 上的 **Delete** 方法来将其 **RowState** 改为 **Deleted**。  
  
```vb  
workRow.Delete  
  
```  
  
```csharp  
workRow.Delete();  
```  
  
 如果将行标记为删除，并且调用 **DataTable** 对象的 **AcceptChanges** 方法，该行就会从 **DataTable** 中移除。  相比之下，如果调用 **RejectChanges**，行的 **RowState** 就会恢复到被标记为 **Deleted** 之前的状态。  
  
> [!NOTE]
>  如果 **DataRow** 的 **RowState** 为 **Added**，则意味着已将其添加到表中，然后会将其标记为 **Deleted**，并从表中移除。  
  
## 请参阅  
 <xref:System.Data.DataRow>   
 <xref:System.Data.DataRowCollection>   
 <xref:System.Data.DataTable>   
 [在 DataTable 中处理数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)