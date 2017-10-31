---
title: "创建 DataTable | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eecf9d78-60e3-4fdc-8de0-e56c13a89414
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 创建 DataTable
<xref:System.Data.DataTable> 表示一个内存内关系数据的表，可以独立创建和使用，也可以由其他 .NET Framework 对象使用，最常见的情况是作为 <xref:System.Data.DataSet> 的成员使用。  
  
 可以使用相应的 **DataTable** 构造函数创建 **DataTable** 对象。  可以通过使用 **Add** 方法将其添加到 **DataTable** 对象的 **Tables** 集合中，将其添加到 **DataSet** 中。  
  
 也可以通过以下方法创建 **DataTable** 对象：使用 **DataAdapter** 对象的 **Fill** 方法或 **FillSchema** 方法在 **DataSet** 中创建，或者使用 **DataSet** 的 **ReadXml**、**ReadXmlSchema** 或 **InferXmlSchema** 方法从预定义的或推断的 XML 架构中创建。  请注意，将一个 **DataTable** 作为成员添加到一个 **DataSet** 的 **Tables** 集合中后，不能再将其添加到任何其他 **DataSet** 的表集合中。  
  
 初次创建 **DataTable** 时，是没有架构（即结构）的。  要定义表的架构，必须创建 <xref:System.Data.DataColumn> 对象并将其添加到表的 **Columns** 集合中。  您也可以为表定义主键列，并且可以创建 **Constraint** 对象并将其添加到表的 **Constraints** 集合中。  在为 **DataTable** 定义了架构之后，可通过将 **DataRow** 对象添加到表的 **Rows** 集合中来将数据行添加到表中。  
  
 创建 **DataTable** 时，不需要为 <xref:System.Data.DataTable.TableName%2A> 属性提供值，您可以在其他时间指定该属性，或者将其保留为空。  但是，在将一个没有 **TableName** 值的表添加到 **DataSet** 中时，该表会得到一个从“Table”（表示 Table0）开始递增的默认名称 Table*N*。  
  
> [!NOTE]
>  建议在提供 **TableName** 值时避免使用“Table*N*”命名约定，因为那样提供的名称可能与 **DataSet** 中现有的默认表名冲突。  如果提供的名称已经存在，将引发异常。  
  
 以下示例创建 **DataTable** 对象的实例，并为其指定名称“Customers”。  
  
```vb  
Dim workTable as DataTable = New DataTable("Customers")  
  
```  
  
```csharp  
DataTable workTable = new DataTable("Customers");  
```  
  
 以下示例创建 **DataTable** 实例，方法是：将其添加到 **DataSet** 的 **Tables** 集合中。  
  
```vb  
Dim customers As DataSet = New DataSet  
Dim customersTable As DataTable = _  
   customers.Tables.Add("CustomersTable")  
  
```  
  
```csharp  
DataSet customers = new DataSet();  
DataTable customersTable = customers.Tables.Add("CustomersTable");  
```  
  
## 请参阅  
 <xref:System.Data.DataTable>   
 <xref:System.Data.DataTableCollection>   
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)   
 [从 DataAdapter 填充数据集](../../../../../docs/framework/data/adonet/populating-a-dataset-from-a-dataadapter.md)   
 [从 XML 中加载 DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [从 XML 中加载 DataSet 架构信息](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)