---
title: "排序和筛选数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fdd9c753-39df-48cd-9822-2781afe76200
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 排序和筛选数据
<xref:System.Data.DataView> 为在 <xref:System.Data.DataTable> 中对数据排序和筛选提供了多种方法：  
  
-   可以使用 <xref:System.Data.DataView.Sort%2A> 属性指定单个或多个列排序顺序并包含 ASC（升序）和 DESC（降序）参数。  
  
-   可以使用 <xref:System.Data.DataView.ApplyDefaultSort%2A> 属性自动以升序创建基于表的一个或多个主键列的排序顺序。  只有当 **Sort** 属性为空引用或空字符串时以及表已定义主键时，<xref:System.Data.DataView.ApplyDefaultSort%2A> 才适用。  
  
-   可以使用 <xref:System.Data.DataView.RowFilter%2A> 属性根据行的列值来指定行的子集。  有关 **RowFilter** 属性的有效表达式的详细信息，请参见 <xref:System.Data.DataColumn> 类的 <xref:System.Data.DataColumn.Expression%2A> 属性的参考信息。  
  
     如果要返回对数据的特定查询的结果（而不是提供数据子集的动态视图），要实现最佳性能，请使用 **DataView** 的 <xref:System.Data.DataView.Find%2A> 或 <xref:System.Data.DataView.FindRows%2A> 方法，而不是设置 **RowFilter** 属性。  设置 **RowFilter** 属性会重新生成数据的索引，从而增加应用程序的系统开销并降低性能。  最好将 **RowFilter** 属性用于通过绑定控件显示筛选结果的数据绑定应用程序。  **Find** 和 **FindRows** 方法会利用当前的索引，而不需要重新生成索引。  有关 **Find** 和 **FindRows** 方法的更多信息，请参见[查找行](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/finding-rows.md)。  
  
-   可以使用 <xref:System.Data.DataView.RowStateFilter%2A> 属性指定要查看的行版本。  **DataView** 根据基础行的 **RowState** 来隐式地管理要公开的行版本。  例如，如果 **RowStateFilter** 设置为 **DataViewRowState.Deleted**，由于不存在 **Current** 行版本，**DataView** 将公开所有 **Deleted** 行的 **Original** 行版本。  可以使用 **DataRowView** 的 **RowVersion** 属性来确定要公开行的哪个行版本。  
  
     下表显示了 **DataViewRowState** 选项。  
  
    |DataViewRowState 选项|描述|  
    |-------------------------|--------|  
    |**CurrentRows**|所有 **Unchanged**、**Added** 和 **Modified** 行的 **Current** 行版本。  这是默认设置。|  
    |**Added**|所有 **Added** 行的 **Current** 行版本。|  
    |**Deleted**|所有 **Deleted** 行的 **Original** 行版本。|  
    |**ModifiedCurrent**|所有 **Modified** 行的 **Current** 行版本。|  
    |**ModifiedOriginal**|所有 **Modified** 行的 **Original** 行版本。|  
    |**无**|没有行。|  
    |**OriginalRows**|所有 **Unchanged**、**Modified** 和 **Deleted** 行的 **Original** 行版本。|  
    |**Unchanged**|所有 **Unchanged** 行的 **Current** 行版本。|  
  
 有关行状态和行版本的更多信息，请参见[行状态与行版本](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md)。  
  
 以下代码示例创建一个视图，该视图显示所有库存量小于或等于再订购量的产品，这些产品首先按供应商 ID 排序，然后按产品名称排序。  
  
```vb  
Dim prodView As DataView = New DataView(prodDS.Tables("Products"), _  
   "UnitsInStock <= ReorderLevel", _  
   "SupplierID, ProductName", _  
   DataViewRowState.CurrentRows)  
  
```  
  
```csharp  
DataView prodView = new DataView(prodDS.Tables["Products"],  
   "UnitsInStock <= ReorderLevel",  
   "SupplierID, ProductName",  
   DataViewRowState.CurrentRows);  
```  
  
## 请参阅  
 <xref:System.Data.DataViewRowState>   
 <xref:System.Data.DataColumn.Expression%2A?displayProperty=fullName>   
 <xref:System.Data.DataTable>   
 <xref:System.Data.DataView>   
 [DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)