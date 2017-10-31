---
title: "修改 DataView | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 697a3991-b660-4a5a-8a54-1a2304ff158e
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 修改 DataView
可以使用 <xref:System.Data.DataView> 在基础表中添加、删除或修改数据行。  通过设置 **DataView** 的三个布尔值属性之一，可以控制使用 **DataView** 修改基础表数据的能力。  这三个属性是 <xref:System.Data.DataView.AllowNew%2A>、<xref:System.Data.DataView.AllowEdit%2A> 和 <xref:System.Data.DataView.AllowDelete%2A>。  默认情况下，它们设置为 **true**。  
  
 如果 **AllowNew** 为 **true**，则可以使用 **DataView** 的 <xref:System.Data.DataView.AddNew%2A> 方法来创建新的 <xref:System.Data.DataRowView>。  请注意，在调用 **DataRowView** 的 <xref:System.Data.DataRowView.EndEdit%2A> 方法之前，新行实际上不会添加到基础 <xref:System.Data.DataTable> 中。  如果调用 **DataRowView** 的 <xref:System.Data.DataRowView.CancelEdit%2A> 方法，则将丢弃新行。  另请注意，一次只能编辑一个 **DataRowView**。  如果在存在挂起行时调用 **DataRowView** 的 **AddNew** 或 **BeginEdit** 方法，则会对该挂起行隐式调用 **EndEdit**。  当调用 **EndEdit** 时，更改将应用于基础 **DataTable**，并且随后可以使用 **DataTable**、**DataSet** 或 **DataRow** 对象的 **AcceptChanges** 或 **RejectChanges** 方法来提交或拒绝更改。  如果 **AllowNew** 为 **false**，则当调用 **DataRowView** 的 **AddNew** 方法时，将引发异常。  
  
 如果 **AllowEdit** 为 **true**，可以通过 **DataRowView** 来修改 **DataRow** 的内容。  可以使用 **DataRowView.EndEdit** 确认对基础行的更改，或使用 **DataRowView.CancelEdit** 拒绝更改。  注意，一次只能编辑一行。  如果在存在挂起行时调用 **DataRowView** 的 **AddNew** 或 **BeginEdit** 方法，则会对该挂起行隐式调用 **EndEdit**。  当调用 **EndEdit** 时，建议更改将放置在基础 **DataRow** 的 **Current** 行版本中，随后可以使用 **DataTable**、**DataSet** 或 **DataRow** 对象的 **AcceptChanges** 或 **RejectChanges** 方法来提交或拒绝这些更改。  如果 **AllowEdit** 为 **false**，则当试图修改 **DataView** 中的值时，将引发异常。  
  
 当编辑现有 **DataRowView** 时，仍将引发基础 **DataTable** 的事件，并提供建议更改。  请注意，如果对基础 **DataRow** 调用 **EndEdit** 或 **CancelEdit**，那么无论是否对 **DataRowView** 调用 **EndEdit** 或 **CancelEdit**，都将应用或取消挂起的更改。  
  
 如果 **AllowDelete** 为 **true**，则可以使用 **DataView** 或 **DataRowView** 对象的 **Delete** 方法删除 **DataView** 中的行，这些行也将从基础 **DataTable** 中删除。  随后可以分别使用 **AcceptChanges** 或 **RejectChanges** 来提交或拒绝删除。  如果 **AllowDelete** 为 **false**，当调用 **DataView** 或 **DataRowView** 的 **Delete** 方法时，将引发异常。  
  
 以下代码示例禁用通过 **DataView** 删除行的功能，并使用 **DataView** 向基础表中添加新行。  
  
```vb  
Dim custTable As DataTable = custDS.Tables("Customers")  
Dim custView As DataView = custTable.DefaultView  
custView.Sort = "CompanyName"  
  
custView.AllowDelete = False  
  
Dim newDRV As DataRowView = custView.AddNew()  
newDRV("CustomerID") = "ABCDE"  
newDRV("CompanyName") = "ABC Products"  
newDRV.EndEdit()  
  
```  
  
```csharp  
DataTable custTable = custDS.Tables["Customers"];  
DataView custView = custTable.DefaultView;  
custView.Sort = "CompanyName";  
  
custView.AllowDelete = false;  
  
DataRowView newDRV = custView.AddNew();  
newDRV["CustomerID"] = "ABCDE";  
newDRV["CompanyName"] = "ABC Products";  
newDRV.EndEdit();  
```  
  
## 请参阅  
 <xref:System.Data.DataTable>   
 <xref:System.Data.DataView>   
 <xref:System.Data.DataRowView>   
 [DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)