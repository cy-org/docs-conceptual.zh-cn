---
title: "复制 DataSet 内容 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cb846617-2b1a-44ff-bd7f-5835f5ea37fa
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# 复制 DataSet 内容
为了在不影响原始数据的情况下使用数据，或者使用 **DataSet** 中数据的子集，可以创建 <xref:System.Data.DataSet> 的副本。  当复制 **DataSet** 时，可以：  
  
-   创建 **DataSet** 的原样副本，其中包含架构、数据、行状态信息和行版本。  
  
-   创建包含现有 **DataSet** 的架构但仅包含已修改行的 **DataSet**。  可以返回已修改的所有行或者指定特定的 **DataRowState**。  有关行状态的更多信息，请参见[行状态与行版本](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-states-and-row-versions.md)。  
  
-   仅复制 **DataSet** 的架构（即关系结构），而不复制任何行。  可以使用 <xref:System.Data.DataTable.ImportRow%2A> 将行导入现有 <xref:System.Data.DataTable>。  
  
 若要创建包含架构和数据的 **DataSet** 的原样副本，请使用 **DataSet** 的 <xref:System.Data.DataSet.Copy%2A> 方法。  以下代码示例显示如何创建 **DataSet** 的原样副本。  
  
```vb  
Dim copyDataSet As DataSet = customerDataSet.Copy()  
  
```  
  
```csharp  
DataSet copyDataSet = customerDataSet.Copy();  
```  
  
 若要创建包含架构并仅包含表示 **Added**、**Modified** 或 **Deleted** 行的数据的 **DataSet** 副本，请使用 **DataSet** 的 <xref:System.Data.DataSet.GetChanges%2A> 方法。  当调用 **GetChanges** 时，也可以通过传递 **DataRowState** 值，使用 **GetChanges** 仅返回具有指定行状态的行。  以下代码示例显示如何在调用 **GetChanges** 时传递 **DataRowState**。  
  
```vb  
' Copy all changes.  
Dim changeDataSet As DataSet = customerDataSet.GetChanges()  
' Copy only new rows.  
Dim addedDataSetAs DataSet = _  
    customerDataSet.GetChanges(DataRowState.Added)  
  
```  
  
```csharp  
// Copy all changes.  
DataSet changeDataSet = customerDataSet.GetChanges();  
// Copy only new rows.  
DataSet addedDataSet= customerDataSet.GetChanges(DataRowState.Added);  
```  
  
 若要创建仅包含架构的 **DataSet** 副本，请使用 **DataSet** 的 <xref:System.Data.DataSet.Clone%2A> 方法。  您也可以使用 **DataTable** 的 **ImportRow** 方法将现有行添加到克隆的 **DataSet** 中。  **ImportRow** 将数据、行状态和行版本信息添加到指定表中。  只有当列名称匹配且数据类型兼容时，才会添加列值。  
  
 以下代码示例创建 **DataSet** 的复本，然后为 **CountryRegion** 列的值为“Germany”的客户将原始 **DataSet** 中的行添加到 **DataSet** 复本中的 **Customers** 表。  
  
```vb  
  
Dim customerDataSet As New DataSet  
        customerDataSet.Tables.Add(New DataTable("Customers"))  
        customerDataSet.Tables("Customers").Columns.Add("Name", GetType(String))  
        customerDataSet.Tables("Customers").Columns.Add("CountryRegion", GetType(String))  
        customerDataSet.Tables("Customers").Rows.Add("Juan", "Spain")  
        customerDataSet.Tables("Customers").Rows.Add("Johann", "Germany")  
        customerDataSet.Tables("Customers").Rows.Add("John", "UK")  
  
Dim germanyCustomers As DataSet = customerDataSet.Clone()  
  
Dim copyRows() As DataRow = _  
  customerDataSet.Tables("Customers").Select("CountryRegion = 'Germany'")  
  
Dim customerTable As DataTable = germanyCustomers.Tables("Customers")  
Dim copyRow As DataRow  
  
For Each copyRow In copyRows  
  customerTable.ImportRow(copyRow)  
Next  
  
```  
  
```csharp  
DataSet customerDataSet = new DataSet();  
customerDataSet.Tables.Add(new DataTable("Customers"));  
customerDataSet.Tables["Customers"].Columns.Add("Name", typeof(string));  
customerDataSet.Tables["Customers"].Columns.Add("CountryRegion", typeof(string));  
customerDataSet.Tables["Customers"].Rows.Add("Juan", "Spain");  
customerDataSet.Tables["Customers"].Rows.Add("Johann", "Germany");  
customerDataSet.Tables["Customers"].Rows.Add("John", "UK");  
  
DataSet germanyCustomers = customerDataSet.Clone();  
  
DataRow[] copyRows =   
  customerDataSet.Tables["Customers"].Select("CountryRegion = 'Germany'");  
  
DataTable customerTable = germanyCustomers.Tables["Customers"];  
  
foreach (DataRow copyRow in copyRows)  
  customerTable.ImportRow(copyRow);  
```  
  
## 请参阅  
 <xref:System.Data.DataSet>   
 <xref:System.Data.DataTable>   
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)