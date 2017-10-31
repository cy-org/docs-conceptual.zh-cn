---
title: "创建 DataView | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b1cc02d1-23b1-4439-a998-0da1899f3442
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 创建 DataView
创建 <xref:System.Data.DataView> 的方法有两种。  可以使用 **DataView** 构造函数，也可以创建对 <xref:System.Data.DataTable> 的 <xref:System.Data.DataTable.DefaultView%2A> 属性的引用。  **DataView** 构造函数可以为空，也可以采用 **DataTable** 作为单个参数，也可以同时采用 **DataTable** 与筛选条件、排序条件和行状态筛选器。  有关可以用于 **DataView** 的其他参数的更多信息，请参见[排序和筛选数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/sorting-and-filtering-data.md)。  
  
 由于在创建 **DataView** 时以及在修改任何 **Sort**、**RowFilter** 或 **RowStateFilter** 属性时都会生成 **DataView** 的索引，所以当创建 **DataView** 时，通过以构造函数参数的形式提供任何初始排序顺序或筛选条件，可以实现最佳性能。  如果在不指定排序或筛选条件的情况下创建 **DataView**，然后设置 **Sort**、**RowFilter** 或 **RowStateFilter** 属性，这会使索引至少生成二次：一次是在创建 **DataView** 时，另一次是在修改任何排序或筛选属性时。  
  
 请注意，如果使用不采用任何参数的构造函数来创建 **DataView**，那么在设置 **Table** 属性之前，将无法使用 **DataView**。  
  
 以下代码示例演示如何使用 **DataView** 构造函数来创建 **DataView**。  **RowFilter**、**Sort** 列和 **DataViewRowState** 将与 **DataTable** 一起提供。  
  
```vb  
Dim custDV As DataView = New DataView(custDS.Tables("Customers"), _  
    "Country = 'USA'", _  
    "ContactName", _  
    DataViewRowState.CurrentRows)  
  
```  
  
```csharp  
DataView custDV = new DataView(custDS.Tables["Customers"],   
    "Country = 'USA'",   
    "ContactName",   
    DataViewRowState.CurrentRows);  
```  
  
 以下代码演示如何使用该表的 **DefaultView** 属性获取对 **DataTable** 的默认 **DataView** 的引用。  
  
```vb  
Dim custDV As DataView = custDS.Tables("Customers").DefaultView  
  
```  
  
```csharp  
DataView custDV = custDS.Tables["Customers"].DefaultView;  
```  
  
## 请参阅  
 <xref:System.Data.DataTable>   
 <xref:System.Data.DataView>   
 [DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)   
 [排序和筛选数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/sorting-and-filtering-data.md)   
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)