---
title: "DataTable 编辑 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f08008a9-042e-4de9-94f3-4f0e502b1eb5
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# DataTable 编辑
当您在 <xref:System.Data.DataRow> 中更改列值时，所做更改会立即置于行的当前状态中。  然后，<xref:System.Data.DataRowState> 会设置为 **Modified**，并使用 **DataRow** 的 <xref:System.Data.DataRow.AcceptChanges%2A> 或 <xref:System.Data.DataRow.RejectChanges%2A> 方法来接受或拒绝所做更改。  **DataRow** 还提供了三种可用于在编辑行时将行的状态挂起的方法。  这三个方法是 <xref:System.Data.DataRow.BeginEdit%2A>、<xref:System.Data.DataRow.EndEdit%2A> 和 <xref:System.Data.DataRow.CancelEdit%2A>。  
  
 当您直接在 **DataRow** 中修改列值时，**DataRow** 会使用 **Current**、**Default** 和 **Original** 行版本来管理列值。  除了这些行版本之外，**BeginEdit**、**EndEdit** 和 **CancelEdit** 方法使用第四种行版本：**Proposed**。  有关行版本的更多信息，请参见[行状态与行版本](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md)。  
  
 在执行编辑操作（通过调用 **BeginEdit** 开始，并且通过使用 **EndEdit** 或 **CancelEdit** 或者通过调用 **AcceptChanges** 或 **RejectChanges** 结束）的过程中，**Proposed** 行版本会存在。  
  
 在编辑操作过程中，您可以通过计算 **DataTable** 的 **ColumnChanged** 事件中的 **ProposedValue** 来将验证逻辑应用于各列。  **ColumnChanged** 事件保存 **DataColumnChangeEventArgs**，可保持对正在更改的列和 **ProposedValue** 的引用。  计算了建议值后，可以对其进行修改或取消编辑。  编辑结束时，行从 **Proposed** 状态中移出。  
  
 您可以通过调用 **EndEdit** 来确认编辑，也可以通过调用 **CancelEdit** 来取消编辑。  请注意，尽管 **EndEdit** 确实已确认您所做的编辑，但在调用 **AcceptChanges** 之前，**DataSet** 并没有实际接受更改。  另外请注意，如果在使用 **EndEdit** 或 **CancelEdit** 结束编辑之前调用 **AcceptChanges**，编辑将会结束，并接受 **Current** 和 **Original** 行版本的 **Proposed** 行值。  同样，调用 **RejectChanges** 也会结束编辑，并放弃 **Current** 和 **Proposed** 行版本。  在调用 **AcceptChanges** 或 **RejectChanges** 之后调用 **EndEdit** 或 **CancelEdit** 不会起作用，因为编辑已经结束。  
  
 以下示例演示了如何将 **BeginEdit** 与 **EndEdit** 和 **CancelEdit** 一起使用。  本示例还会检查 **ColumnChanged** 事件中的 **ProposedValue**，并决定是否取消编辑。  
  
```vb  
Dim workTable As DataTable = New DataTable  
workTable.Columns.Add("LastName", Type.GetType("System.String"))  
  
AddHandler workTable.ColumnChanged, _  
  New DataColumnChangeEventHandler(AddressOf OnColumnChanged)  
  
Dim workRow As DataRow = workTable.NewRow()  
workRow(0) = "Smith"  
workTable.Rows.Add(workRow)  
  
workRow.BeginEdit()  
' Causes the ColumnChanged event to write a message and cancel the edit.  
workRow(0) = ""       
workRow.EndEdit()  
  
' Displays "Smith, New".  
Console.WriteLine("{0}, {1}", workRow(0), workRow.RowState)  
  
Private Shared Sub OnColumnChanged( _  
  sender As Object, args As DataColumnChangeEventArgs)  
  If args.Column.ColumnName = "LastName" Then  
    If args.ProposedValue.ToString() = "" Then  
      Console.WriteLine("Last Name cannot be blank.  Edit canceled.")  
      args.Row.CancelEdit()  
    End If  
  End If  
End Sub  
  
```  
  
```csharp  
DataTable workTable  = new DataTable();  
workTable.Columns.Add("LastName", typeof(String));  
  
workTable.ColumnChanged +=   
  new DataColumnChangeEventHandler(OnColumnChanged);  
  
DataRow workRow = workTable.NewRow();  
workRow[0] = "Smith";  
workTable.Rows.Add(workRow);  
  
workRow.BeginEdit();  
// Causes the ColumnChanged event to write a message and cancel the edit.  
workRow[0] = "";       
workRow.EndEdit();  
  
// Displays "Smith, New".  
Console.WriteLine("{0}, {1}", workRow[0], workRow.RowState);    
  
protected static void OnColumnChanged(  
  Object sender, DataColumnChangeEventArgs args)  
{  
  if (args.Column.ColumnName == "LastName")  
    if (args.ProposedValue.ToString() == "")  
    {  
      Console.WriteLine("Last Name cannot be blank. Edit canceled.");  
      args.Row.CancelEdit();  
    }  
}  
```  
  
## 请参阅  
 <xref:System.Data.DataRow>   
 <xref:System.Data.DataTable>   
 <xref:System.Data.DataRowVersion>   
 [在 DataTable 中处理数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)   
 [处理 DataTable 事件](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/handling-datatable-events.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)