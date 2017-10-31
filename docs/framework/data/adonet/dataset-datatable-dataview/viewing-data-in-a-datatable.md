---
title: "查看数据表中的数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1d26e0fb-f6e0-4afa-9a9c-b8d55b8f20dc
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 查看数据表中的数据
可以使用 **DataTable** 的 **Rows** 和 **Columns** 集合来访问 <xref:System.Data.DataTable> 中的内容。  也可以根据包括搜索条件、排序顺序和行状态在内的特定条件，使用 <xref:System.Data.DataTable.Select%2A> 方法返回 **DataTable** 中数据的子集。  此外，在使用主键值搜索特定行时，还可以使用 **DataRowCollection** 的 <xref:System.Data.DataRowCollection.Find%2A> 方法。  
  
 **DataTable** 对象的 **Select** 方法返回一组与指定条件匹配的 <xref:System.Data.DataRow> 对象。  **Select** 接受筛选表达式、排序表达式和 **DataViewRowState** 的可选参数。  筛选表达式根据 **DataColumn** 值（例如 `LastName = 'Smith'`）标识要返回的行。  排序表达式遵循用于为列排序的标准 SQL 约定，例如 `LastName ASC, FirstName ASC`。  有关编写表达式的规则，请参见 **DataColumn** 类的 <xref:System.Data.DataColumn.Expression%2A> 属性。  
  
> [!TIP]
>  如果将对 **DataTable** 的 **Select** 方法执行多次调用，可以先为 **DataTable** 创建 <xref:System.Data.DataView> 以提高性能。  创建 **DataView** 会为表中的行编制索引。  然后，**Select** 方法会使用该索引，这样将显著缩短生成查询结果的时间。  有关为 **DataTable** 创建 **DataView** 的信息，请参见[DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)。  
  
 **Select** 方法基于 <xref:System.Data.DataViewRowState> 确定要查看或处理的行的版本。  下表说明了可能的 **DataViewRowState** 枚举值。  
  
|DataViewRowState 值|描述|  
|------------------------|--------|  
|**CurrentRows**|当前行，包括未更改的行、已添加的行和已修改的行。|  
|**Deleted**|已删除的行。|  
|**ModifiedCurrent**|当前版本，它是原始数据的修改版本。  （请参见 **ModifiedOriginal**）。|  
|**ModifiedOriginal**|所有已修改行的原始版本。  使用 **ModifiedCurrent** 可以获得当前版本。|  
|**Added**|新行。|  
|**无**|无。|  
|**OriginalRows**|原始行，包括未更改的行和已删除的行。|  
|**Unchanged**|未更改的行。|  
  
 在下面的示例中，**DataSet** 对象已经过筛选，这样，您可以只使用其 **DataViewRowState** 设置为 **CurrentRows** 的行。  
  
```vb  
Dim column As DataColumn  
Dim row As DataRow  
  
Dim currentRows() As DataRow = _  
    workTable.Select(Nothing, Nothing, DataViewRowState.CurrentRows)  
  
If (currentRows.Length < 1 ) Then  
  Console.WriteLine("No Current Rows Found")  
Else  
  For Each column in workTable.Columns  
    Console.Write(vbTab & column.ColumnName)  
  Next  
  
  Console.WriteLine(vbTab & "RowState")  
  
  For Each row In currentRows  
    For Each column In workTable.Columns  
      Console.Write(vbTab & row(column).ToString())  
    Next  
  
    Dim rowState As String = _  
        System.Enum.GetName(row.RowState.GetType(), row.RowState)  
    Console.WriteLine(vbTab & rowState)  
  Next  
End If  
  
```  
  
```csharp  
DataRow[] currentRows = workTable.Select(  
    null, null, DataViewRowState.CurrentRows);  
  
if (currentRows.Length < 1 )  
  Console.WriteLine("No Current Rows Found");  
else  
{  
  foreach (DataColumn column in workTable.Columns)  
    Console.Write("\t{0}", column.ColumnName);  
  
  Console.WriteLine("\tRowState");  
  
  foreach (DataRow row in currentRows)  
  {  
    foreach (DataColumn column in workTable.Columns)  
      Console.Write("\t{0}", row[column]);  
  
    Console.WriteLine("\t" + row.RowState);  
  }  
}  
```  
  
 **Select** 方法可用于返回具有不同 **RowState** 值或字段值的行。  下面的示例返回一个引用所有已删除行的 **DataRow** 数组，并返回另一个引用所有按 **CustLName** 排序的行（其中 **CustID** 列大于 5）的 **DataRow** 数组。  有关如何在 **Deleted** 行中查看信息的信息，请参见[行状态与行版本](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md)。  
  
```vb  
' Retrieve all deleted rows.  
Dim deletedRows() As DataRow = workTable.Select(Nothing, Nothing, DataViewRowState.Deleted)  
  
' Retrieve rows where CustID > 5, and order by CustLName.  
Dim custRows() As DataRow = workTable.Select( _  
    "CustID > 5", "CustLName ASC")  
  
```  
  
```csharp  
// Retrieve all deleted rows.  
DataRow[] deletedRows = workTable.Select(  
    null, null, DataViewRowState.Deleted);  
  
// Retrieve rows where CustID > 5, and order by CustLName.  
DataRow[] custRows = workTable.Select("CustID > 5", "CustLName ASC");  
```  
  
## 请参阅  
 <xref:System.Data.DataRow>   
 <xref:System.Data.DataSet>   
 <xref:System.Data.DataTable>   
 <xref:System.Data.DataViewRowState>   
 [在 DataTable 中处理数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)   
 [行状态与行版本](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)