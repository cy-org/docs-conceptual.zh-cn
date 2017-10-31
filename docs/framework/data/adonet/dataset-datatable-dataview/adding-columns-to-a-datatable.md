---
title: "向数据表中添加列 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e85c4a0e-4f3f-458c-b58b-0ddbc06bf974
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 向数据表中添加列
<xref:System.Data.DataTable> 包含了由表的 **Columns** 属性引用的 <xref:System.Data.DataColumn> 对象的集合。  这个列的集合与任何约束一起定义表的架构（即结构）。  
  
 通过使用 **DataColumn** 构造函数，或者通过调用表的 **Columns** 属性的 **Add** 方法（它是一个 <xref:System.Data.DataColumnCollection>），可在表内创建 **DataColumn** 对象。  **Add** 方法将接受可选的 **ColumnName**、**DataType** 和 **Expression** 参数，并将创建新的 **DataColumn** 作为集合的成员。  它还会接受现有的 **DataColumn** 对象并会将其添加到集合中，并会根据请求返回对所添加的 **DataColumn** 的引用。  由于 **DataTable** 对象不特定于任何数据源，所以在指定 **DataColumn** 的数据类型时会使用 .NET Framework 类型。  
  
 以下示例向 **DataTable** 中添加了四列。  
  
```vb  
Dim workTable As DataTable = New DataTable("Customers")  
  
Dim workCol As DataColumn = workTable.Columns.Add( _  
    "CustID", Type.GetType("System.Int32"))  
workCol.AllowDBNull = false  
workCol.Unique = true  
  
workTable.Columns.Add("CustLName", Type.GetType("System.String"))  
workTable.Columns.Add("CustFName", Type.GetType("System.String"))  
workTable.Columns.Add("Purchases", Type.GetType("System.Double"))  
  
```  
  
```csharp  
DataTable workTable = new DataTable("Customers");  
  
DataColumn workCol = workTable.Columns.Add("CustID", typeof(Int32));  
workCol.AllowDBNull = false;  
workCol.Unique = true;  
  
workTable.Columns.Add("CustLName", typeof(String));  
workTable.Columns.Add("CustFName", typeof(String));  
workTable.Columns.Add("Purchases", typeof(Double));  
```  
  
 请注意，示例中用于 **CustID** 列的属性设置为不允许 **DBNull** 值并将值约束为唯一。  但是，如果您将 **CustID** 列定义为表的主键列，**AllowDBNull** 属性就会自动设置为 **false**，并且 **Unique** 属性会自动设置为 **true**。  有关详细信息，请参阅[定义主键](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/defining-primary-keys.md)。  
  
> [!CAUTION]
>  如果没有为一个列提供列名，则在将该列添加到 **DataColumnCollection** 时，该列会得到从“Column1”开始递增的默认名称 Column*N*。  建议在提供列名时避免使用“Column*N*”命名约定，因为那样提供的名称可能与 **DataColumnCollection** 中现有的默认列名冲突。  如果提供的名称已经存在，将引发异常。  
  
 如果将 <xref:System.Xml.XLinq.XElement> 用作 <xref:System.Data.DataTable> 中的 <xref:System.Data.DataColumn> 的 <xref:System.Data.DataColumn.DataType%2A>，则在读入数据时，XML 序列化将不起作用。  例如，如果通过使用 `DataTable.WriteXml` 方法来写出 <xref:System.Xml.XmlDocument>，则在序列化为 XML 时，<xref:System.Xml.XLinq.XElement> 中会出现一个额外的父节点。  若要解决此问题，请使用 <xref:System.Data.SqlTypes.SqlXml> 类型来代替 <xref:System.Xml.XLinq.XElement>。  `ReadXml` 和 `WriteXml` 对 <xref:System.Data.SqlTypes.SqlXml> 均能正确使用。  
  
## 请参阅  
 <xref:System.Data.DataColumn>   
 <xref:System.Data.DataColumnCollection>   
 <xref:System.Data.DataTable>   
 [DataTable 架构定义](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-schema-definition.md)   
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)