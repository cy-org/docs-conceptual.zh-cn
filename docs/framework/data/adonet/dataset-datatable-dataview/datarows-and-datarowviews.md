---
title: "DataRow 和 DataRowView | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8f5eec26-b809-4aca-8778-7e202356d856
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# DataRow 和 DataRowView
<xref:System.Data.DataView> 公开 <xref:System.Data.DataRowView> 对象的可枚举集合。  **DataRowView** 对象将值公开为对象数组，这些数组按基础表中列的名称或序号引用来编制索引。  可以使用 **DataRowView** 的 <xref:System.Data.DataRowView.Row%2A> 属性访问由 **DataRowView** 公开的 <xref:System.Data.DataRow>。  
  
 当使用 **DataRowView** 查看值时，**DataView** 的 <xref:System.Data.DataView.RowStateFilter%2A> 属性将确定公开基础 **DataRow** 的哪一个行版本。  有关使用 **DataRow** 访问不同行版本的信息，请参见[行状态与行版本](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md)。  
  
 以下代码示例显示一个表中的所有当前值和原始值。  
  
```vb  
Dim catView As DataView = New DataView(catDS.Tables("Categories"))  
Console.WriteLine("Current Values:")  
WriteView(catView)  
Console.WriteLine("Original Values:")  
catView.RowStateFilter = DataViewRowState.ModifiedOriginal  
WriteView(catView)      
  
Public Shared Sub WriteView(thisDataView As DataView)  
  Dim rowView As DataRowView  
  Dim i As Integer  
  
  For Each rowView In thisDataView  
    For i = 0 To thisDataView.Table.Columns.Count - 1  
      Console.Write(rowView(i) & vbTab)  
    Next  
    Console.WriteLine()  
  Next  
End Sub  
  
```  
  
```csharp  
DataView catView = new DataView(catDS.Tables["Categories"]);  
Console.WriteLine("Current Values:");  
WriteView(catView);  
Console.WriteLine("Original Values:");  
catView.RowStateFilter = DataViewRowState.ModifiedOriginal;  
WriteView(catView);  
  
public static void WriteView(DataView thisDataView)  
{  
  foreach (DataRowView rowView in thisDataView)  
  {  
    for (int i = 0; i < thisDataView.Table.Columns.Count; i++)  
      Console.Write(rowView[i] + "\t");  
    Console.WriteLine();  
  }  
}  
```  
  
## 请参阅  
 <xref:System.Data.DataRowVersion>   
 <xref:System.Data.DataViewRowState>   
 <xref:System.Data.DataView>   
 <xref:System.Data.DataRowView>   
 [DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)