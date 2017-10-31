---
title: "向 DataSet 添加现有约束 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 307d2809-208b-4cf8-b6a9-5d16f15fc16c
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 向 DataSet 添加现有约束
**DataAdapter** 的 **Fill** 方法仅使用数据源中的表列和表行来填充 <xref:System.Data.DataSet>；虽然约束通常由数据源来设置，但在默认情况下，**Fill** 方法不会将此架构信息添加到 **DataSet** 中。  若要使用数据源中的现有主键约束信息填充 **DataSet**，则可以调用 **DataAdapter** 的 **FillSchema** 方法，或者在调用 **Fill** 之前将 **DataAdapter** 的 **MissingSchemaAction** 属性设置为 **AddWithKey**。  这将确保 **DataSet** 中的主键约束反映数据源中的主键约束。  外键约束信息不包含在内，必须显式创建，如[数据表约束](../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-constraints.md)中所示。  
  
 如果在使用数据填充 **DataSet** 之前向其中添加架构信息，可以确保将主键约束与 **DataSet** 中的 <xref:System.Data.DataTable> 对象包含在一起。  这样，当再次调用来填充 **DataSet** 时，将使用主键列信息将数据源中的新行与每个 **DataTable** 中的当前行相匹配，并使用数据源中的数据改写表中的当前数据。  如果没有架构信息，来自数据源的新行将追加到 **DataSet** 中，从而导致重复的行。  
  
> [!NOTE]
>  如果数据源中的某列被标识为自动递增列，则 **FillSchema** 方法或 **MissingSchemaAction** 为 **AddWithKey** 的 **Fill** 方法将创建一个 **AutoIncrement** 属性设置为 `true` 的 **DataColumn**。  不过，您将需要手动设置 **AutoIncrementStep** 和 **AutoIncrementSeed** 值。  有关自动递增列的更多信息，请参见[创建 AutoIncrement 列](../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-autoincrement-columns.md)。  
  
 当使用 **FillSchema** 或将 **MissingSchemaAction** 设置为 **AddWithKey** 时，将需要在数据源中进行额外的处理来确定主键列信息。  这一额外的处理可能会降低性能。  如果主键信息在设计时已知，为了实现最佳性能，建议显式指定一个或多个主键列。  有关显式设置表的主键信息的详情，请参见[定义主键](../../../../docs/framework/data/adonet/dataset-datatable-dataview/defining-primary-keys.md)。  
  
 以下代码示例显示如何使用 **FillSchema** 向 **DataSet** 添加架构信息。  
  
```vb  
Dim custDataSet As DataSet = New DataSet()  
  
custAdapter.FillSchema(custDataSet, SchemaType.Source, "Customers")  
custAdapter.Fill(custDataSet, "Customers")  
```  
  
```csharp  
DataSet custDataSet = new DataSet();  
  
custAdapter.FillSchema(custDataSet, SchemaType.Source, "Customers");  
custAdapter.Fill(custDataSet, "Customers");  
```  
  
 以下代码示例显示如何使用 **Fill** 方法的 **MissingSchemaAction.AddWithKey** 属性向 **DataSet** 添加架构信息。  
  
```vb  
Dim custDataSet As DataSet = New DataSet()  
  
custAdapter.MissingSchemaAction = MissingSchemaAction.AddWithKey  
custAdapter.Fill(custDataSet, "Customers")  
```  
  
```csharp  
DataSet custDataSet = new DataSet();  
  
custAdapter.MissingSchemaAction = MissingSchemaAction.AddWithKey;  
custAdapter.Fill(custDataSet, "Customers");  
```  
  
## 处理多个结果集  
 如果 **DataAdapter** 遇到从 **SelectCommand** 中返回的多个结果集，将在 **DataSet** 中创建多个表。  将向这些表提供基于零的递增的默认名称 **Table** *N*，从 **Table** 开始，而不是从“Table0”开始。  如果以参数形式向 **FillSchema** 方法传递表名称，则将向这些表提供基于零的递增的名称 **TableName** *N*，从 **TableName** 开始，而不是从“TableName0”开始。  
  
> [!NOTE]
>  如果对返回多个结果集的命令调用 **OleDbDataAdapter** 对象的 **FillSchema** 方法，则将只返回第一个结果集中的架构信息。  当使用 **OleDbDataAdapter** 为多个结果集返回架构信息时，建议在调用 **Fill** 方法时将 **MissingSchemaAction** 指定为 **AddWithKey** 并获取架构信息。  
  
## 请参阅  
 [DataAdapter 和 DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [DataSet、DataTable 和 DataView](../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [在 ADO.NET 中检索和修改数据](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)