---
title: "DataAdapter DataTable 和 DataColumn 映射 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d023260a-a66a-4c39-b8f4-090cd130e730
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# DataAdapter DataTable 和 DataColumn 映射
**DataAdapter** 在其 **TableMappings** 属性中包含零个或更多个 <xref:System.Data.Common.DataTableMapping> 对象的集合。  **DataTableMapping** 提供对数据源的查询所返回的数据与 <xref:System.Data.DataTable> 之间的主映射。  **DataTableMapping** 名称可以代替 **DataTable** 名称传递到 **DataAdapter** 的 **Fill** 方法。  以下示例为 **Authors** 表创建名为 **AuthorsMapping** 的 **DataTableMapping**。  
  
```vb  
workAdapter.TableMappings.Add("AuthorsMapping", "Authors")  
```  
  
```csharp  
workAdapter.TableMappings.Add("AuthorsMapping", "Authors");  
```  
  
 **DataTableMapping** 使您能够使用 **DataTable** 中与数据库中的列名不同的列名。  当该表被更新时，**DataAdapter** 将使用此映射来匹配列。  
  
 如果在调用 **DataAdapter** 的 **Fill** 或 **Update** 方法时未指定 **TableName** 或 **DataTableMapping** 名称，**DataAdapter** 将查找名为“Table”的 **DataTableMapping**。  如果该 **DataTableMapping** 不存在，**DataTable** 的 **TableName** 将为“Table”。  可以通过创建名为“Table”的 **DataTableMapping** 来指定默认的 **DataTableMapping**。  
  
 以下代码示例创建一个 **DataTableMapping**（从 <xref:System.Data.Common> 命名空间）并通过将其命名为“Table”来使其成为指定 **DataAdapter** 的默认映射。  然后，该示例将查询结果中第一个表（**Northwind** 数据库的 **Customers** 表）中的列映射到 <xref:System.Data.DataSet> 的 **Northwind Customers** 表中的一组更为用户友好的名称。  对于未映射的列，将使用数据源中的列名称。  
  
```vb  
Dim mapping As DataTableMapping = _  
  adapter.TableMappings.Add("Table", "NorthwindCustomers")  
mapping.ColumnMappings.Add("CompanyName", "Company")  
mapping.ColumnMappings.Add("ContactName", "Contact")  
mapping.ColumnMappings.Add("PostalCode", "ZIPCode")  
  
adapter.Fill(custDS)  
  
```  
  
```csharp  
DataTableMapping mapping =   
  adapter.TableMappings.Add("Table", "NorthwindCustomers");  
mapping.ColumnMappings.Add("CompanyName", "Company");  
mapping.ColumnMappings.Add("ContactName", "Contact");  
mapping.ColumnMappings.Add("PostalCode", "ZIPCode");  
  
adapter.Fill(custDS);  
```  
  
 在更为先进的情况下，您可以决定需要使用相同的 **DataAdapter** 来支持为不同的表加载不同的映射。  若要完成此任务，只需添加附加的 **DataTableMapping** 对象。  
  
 当 **Fill** 方法以 **DataSet** 实例和 **DataTableMapping** 名称的形式进行传递时，如果存在具有该名称的映射，则使用该映射；否则将使用具有该名称的 **DataTable**。  
  
 以下示例创建一个名称为 **Customers** 而 **DataTable** 名称为 **BizTalkSchema** 的 **DataTableMapping**。  然后，该示例将 SELECT 语句所返回的行映射到 **BizTalkSchema** **DataTable**。  
  
```vb  
Dim mapping As ITableMapping = _  
  adapter.TableMappings.Add("Customers", "BizTalkSchema")  
mapping.ColumnMappings.Add("CustomerID", "ClientID")  
mapping.ColumnMappings.Add("CompanyName", "ClientName")  
mapping.ColumnMappings.Add("ContactName", "Contact")  
mapping.ColumnMappings.Add("PostalCode", "ZIP")  
  
adapter.Fill(custDS, "Customers")  
  
```  
  
```csharp  
ITableMapping mapping =   
  adapter.TableMappings.Add("Customers", "BizTalkSchema");  
mapping.ColumnMappings.Add("CustomerID", "ClientID");  
mapping.ColumnMappings.Add("CompanyName", "ClientName");  
mapping.ColumnMappings.Add("ContactName", "Contact");  
mapping.ColumnMappings.Add("PostalCode", "ZIP");  
  
adapter.Fill(custDS, "Customers");  
```  
  
> [!NOTE]
>  如果没有为列映射提供源列名称或者没有为表映射提供源表名称，则将自动生成默认名称。  如果没有为列映射提供源列，则将给列映射提供递增的默认名称 **SourceColumn** *N*，这些名称从 **SourceColumn1** 开始。  如果没有为表映射提供源表名称，则将给该表映射提供递增的默认名称 **SourceTable** *N*，这些名称从 **SourceTable1** 开始。  
  
> [!NOTE]
>  我们建议您避免采用列映射的 **SourceColumn** *N* 的命名约定，或表映射的 **SourceTable** *N* 的命名约定，因为您提供的名称可能会与 **ColumnMappingCollection** 中的现有默认列映射名称或 **DataTableMappingCollection** 中的现有默认表映射名称冲突。  如果提供的名称已经存在，将引发异常。  
  
## 处理多个结果集  
 如果 **SelectCommand** 返回多个表，**Fill** 将自动使用递增值为 **DataSet** 中的表生成表名称，这些表名称从指定表名称开始，并以 **TableName** *N* 格式（从 **TableName1** 开始）继续。  可以使用表映射将自动生成的表名称映射到要为 **DataSet** 中的表指定的名称。  例如，对于返回两个表（**Customers** 和 **Orders**）的 **SelectCommand**，可对 **Fill** 发出以下调用。  
  
```  
adapter.Fill(customersDataSet, "Customers")  
```  
  
 在 **DataSet** 中创建了两个表：**Customers** 和 **Customers1**。  可以使用表映射来确保第二个表名为 **Orders** 而不是 **Customers1**。  若要完成此任务，请将 **Customers1** 的源表映射到 **DataSet** 表 **Orders**，如以下示例所示。  
  
```  
adapter.TableMappings.Add("Customers1", "Orders")  
adapter.Fill(customersDataSet, "Customers")  
```  
  
## 请参阅  
 [DataAdapter 和 DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [在 ADO.NET 中检索和修改数据](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)