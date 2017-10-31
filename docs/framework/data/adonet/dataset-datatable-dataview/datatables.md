---
title: "DataTable | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52ff0e32-3e5a-41de-9a3b-7b04ea52b83e
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# DataTable
<xref:System.Data.DataSet> 由表、关系和约束的集合组成。  在 ADO.NET 中，<xref:System.Data.DataTable> 对象用于表示 **DataSet** 中的表。  **DataTable** 表示一个内存内关系数据的表；数据对于所处的基于 .NET 的应用程序来说是本地数据，但可从数据源（例如，使用 **DataAdapter** 的 Microsoft SQL Server）中导入。有关更多信息，请参见[从 DataAdapter 填充数据集](../../../../../docs/framework/data/adonet/populating-a-dataset-from-a-dataadapter.md)。  
  
 **DataTable** 类是 .NET Framework 类库中 **System.Data** 命名空间的成员。  您可以独立创建和使用 **DataTable**，也可以作为 **DataSet** 的成员创建和使用，而且 **DataTable** 对象也可以与其他 .NET Framework 对象（包括 <xref:System.Data.DataView>）一起使用。  您可以通过 **DataSet** 对象的 **Tables** 属性来访问 **DataSet** 中表的集合。  
  
 表的架构或结构由列和约束表示。  使用 <xref:System.Data.DataColumn> 对象以及 <xref:System.Data.ForeignKeyConstraint> 和 <xref:System.Data.UniqueConstraint> 对象定义 **DataTable** 的架构。  表中的列可以映射到数据源中的列、包含从表达式计算所得的值、自动递增它们的值，或包含主键值。  
  
 除架构以外，**DataTable** 还必须具有行，在其中包含数据并对数据排序。  <xref:System.Data.DataRow> 类表示表中包含的实际数据。  **DataRow** 及其属性和方法用于检索、计算和处理表中的数据。  在访问和更改行中的数据时，**DataRow** 对象会维护其当前状态和原始状态。  
  
 您可以使用表中的一个或多个相关的列来创建表与表之间的父子关系。  **DataTable** 对象之间的关系可使用 <xref:System.Data.DataRelation> 来创建。  然后，**DataRelation** 对象可用于返回某特定行的相关子行或父行。  有关详细信息，请参阅[添加 DataRelation](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/adding-datarelations.md)。  
  
## 本节内容  
 [创建 DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/creating-a-datatable.md)  
 说明如何创建 **DataTable** 并将其添加到 **DataSet**。  
  
 [DataTable 架构定义](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatable-schema-definition.md)  
 提供有关创建和使用 **DataColumn** 对象和约束的信息。  
  
 [在 DataTable 中处理数据](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/manipulating-data-in-a-datatable.md)  
 说明如何添加、修改和删除表中的数据。  说明如何使用 **DataTable** 事件来检查对表中数据的更改。  
  
 [处理 DataTable 事件](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/handling-datatable-events.md)  
 提供可用于 **DataTable** 的事件的相关信息，包括修改列值和添加或删除行时的事件。  
  
## 相关章节  
 [ADO.NET](../../../../../docs/framework/data/adonet/index.md)  
 描述 ADO.NET 结构和组件，并说明如何用来访问现有的数据源和管理应用程序数据。  
  
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)  
 提供有关 ADO.NET **DataSet** 的信息，包括如何创建表与表之间的关系。  
  
 [Constraint 类](frlrfSystemDataConstraintClassTopic)  
 提供有关 **Constraint** 对象的参考信息。  
  
 [DataColumn 类](frlrfSystemDataDataColumnClassTopic)  
 提供有关 **DataColumn** 对象的参考信息。  
  
 [DataSet 类](frlrfSystemDataDataSetClassTopic)  
 提供有关 **DataSet** 对象的参考信息。  
  
 [DataTable 类](frlrfSystemDataDataTableClassTopic)  
 提供有关 **DataTable** 对象的参考信息。  
  
 [类库概述](../../../../../docs/standard/class-library-overview.md)  
 提供 .NET Framework 类库（包括 **System** 命名空间及其第二级命名空间 **System.Data**）的概述。  
  
## 请参阅  
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)