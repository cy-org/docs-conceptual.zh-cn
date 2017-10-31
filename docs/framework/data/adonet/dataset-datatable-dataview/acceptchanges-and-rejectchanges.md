---
title: "AcceptChanges 和 RejectChanges | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e2d1a6fe-31f9-4b83-9728-06c406a3394e
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# AcceptChanges 和 RejectChanges
在验证了对 <xref:System.Data.DataTable> 中的数据所做更改的准确性之后，可使用 <xref:System.Data.DataRow>、<xref:System.Data.DataTable> 或 <xref:System.Data.DataSet> 的 <xref:System.Data.DataRow.AcceptChanges%2A> 方法来接受更改，此方法会将 **Current** 行值设置为 **Original** 值，并会将 **RowState** 属性设置为 **Unchanged**。  接受或拒绝更改会清除所有 **RowError** 信息，并将 **HasErrors** 属性设置为 **false**。  接受或拒绝更改还可以影响在数据源中更新数据。  有关详细信息，请参阅[使用 DataAdapter 更新数据源](../../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md)。  
  
 如果 **DataTable** 上存在外键约束，使用 **AcceptChanges** 和 **RejectChanges** 接受或拒绝的更改就会根据 **ForeignKeyConstraint.AcceptRejectRule** 传播到 **DataRow** 的子行。  有关详细信息，请参阅[数据表约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-constraints.md)。  
  
 以下示例检查有错误的行，如果可以会解决错误，拒绝无法解决错误的行。  请注意，对于已解决的错误，**RowError** 值会重置为空字符串，导致将 **HasErrors** 属性设置为 **false**。  当解决或拒绝了所有有错误的行后，就会调用 **AcceptChanges** 来接受对整个 **DataTable** 的所有更改。  
  
```vb  
If workTable.HasErrors Then  
  Dim errRow As DataRow  
  
  For Each errRow in workTable.GetErrors()  
  
    If errRow.RowError = "Total cannot exceed 1000." Then  
      errRow("Total") = 1000  
      errRow.RowError = ""    ' Clear the error.  
    Else  
      errRow.RejectChanges()  
    End If  
  Next  
End If  
  
workTable.AcceptChanges()  
  
```  
  
```csharp  
if (workTable.HasErrors)  
{  
  
  foreach (DataRow errRow in workTable.GetErrors())  
  {  
    if (errRow.RowError == "Total cannot exceed 1000.")  
    {  
      errRow["Total"] = 1000;  
      errRow.RowError = "";    // Clear the error.  
    }  
    else  
      errRow.RejectChanges();  
  }  
}  
  
workTable.AcceptChanges();  
```  
  
## 请参阅  
 <xref:System.Data.DataRow>   
 <xref:System.Data.DataSet>   
 <xref:System.Data.DataTable>   
 [在 DataTable 中处理数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)