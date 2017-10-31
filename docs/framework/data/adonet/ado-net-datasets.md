---
title: "ADO.NET 数据集 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 82b641bb-6001-4512-bf1a-2830acdd92ab
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# ADO.NET 数据集
<xref:System.Data.DataSet>对象是支持的核心断开连接，分布式数据方案[!INCLUDE[vstecado](../../../../includes/vstecado-md.md)]。 **数据集**是提供一致的关系编程模型，而不考虑数据源的数据的内存驻留表示。 它可以用于多种不同的数据源，用于 XML 数据，或用于管理应用程序本地的数据。 **数据集**表示一组完整的数据，包括相关的表、 约束和表之间的关系。 如下图所示**数据集**对象模型。  
  
 ![ADO.Net 图](../../../../docs/framework/data/adonet/media/ado-1-bpuedev11.png "ado_1_bpuedev11")  
DataSet 对象模型  
  
 方法和中的对象**数据集**与关系数据库模型保持一致。  
  
 **数据集**还可以保留并重新加载其内容为 XML，且其架构作为 XML 架构定义语言 (XSD) 架构。 有关详细信息，请参阅[数据集中使用 XML](../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)。  
  
## <a name="the-datatablecollection"></a>DataTableCollection  
 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] **数据集**包含所表示的零个或多个表的集合<xref:System.Data.DataTable>对象。 <xref:System.Data.DataTableCollection>包含所有**DataTable**中的对象**数据集**。  
  
 一个**DataTable**中定义<xref:System.Data>命名空间并表示内存驻留数据的单个表。 它包含的列所表示的集合<xref:System.Data.DataColumnCollection>，和约束由<xref:System.Data.ConstraintCollection>，这在一起定义表的架构。 一个**DataTable**还包含一个由行集合<xref:System.Data.DataRowCollection>，其中包含表中的数据。 除了其当前状态<xref:System.Data.DataRow>保留其当前和原始版本版本，以标识更改的行中存储的值。  
  
## <a name="the-dataview-class"></a>DataView 类  
 一个<xref:System.Data.DataView>使您能够创建中存储的数据的不同视图<xref:System.Data.DataTable>，通常在数据绑定应用程序中使用的功能。 使用<xref:System.Data.DataView>，您可以公开具有不同的排序顺序的表中的数据，并且可以按行状态或基于筛选器表达式来筛选数据。 有关详细信息，请参阅[Dataview](../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataviews.md)。  
  
## <a name="the-datarelationcollection"></a>DataRelationCollection  
 一个**数据集**包含中的关系及其<xref:System.Data.DataRelationCollection>对象。 一种关系，由表示<xref:System.Data.DataRelation>对象，其中一个中的行相关联**DataTable**另一个中的行与**DataTable**。 关系类似于可能存在于关系数据库中的主键列和外键列之间的联接路径。 一个**DataRelation**标识两个数据表中的匹配列**数据集**。  
  
 关系可以从一个表导航到另一个在**数据集**。 基本元素**DataRelation**是关系的名称、 其相关的表的名称和每个表中的相关的列。 关系可以通过指定一个字符串数组的每个表的多个列生成<xref:System.Data.DataColumn>对象作为键列。 当添加到关系<xref:System.Data.DataRelationCollection>，您可以选择添加**UniqueKeyConstraint**和**ForeignKeyConstraint**相关的列的值发生更改时强制执行完整性约束。  
  
 有关详细信息，请参阅[添加 Datarelation](../../../../docs/framework/data/adonet/dataset-datatable-dataview/adding-datarelations.md)。  
  
## <a name="xml"></a>XML  
 你可以填写**数据集**从 XML 流或文档。 可以使用 XML 流或文档要提供给**数据集**数据、 架构信息，或两者。 从 XML 流或文档中提供的信息可以与现有数据或架构信息已存在于组合**数据集**。 有关详细信息，请参阅[数据集中使用 XML](../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)。  
  
## <a name="extendedproperties"></a>ExtendedProperties  
 **数据集**， **DataTable**，和**DataColumn**都**ExtendedProperties**属性。 **ExtendedProperties**是**PropertyCollection**可用来放置自定义的信息，例如用于生成结果集的 SELECT 语句或生成数据的时间。 **ExtendedProperties**集合的架构信息一起持久化**数据集**。  
  
## <a name="linq-to-dataset"></a>LINQ to DataSet  
 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)]为数据集中存储的已断开连接的数据提供语言集成查询功能。 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)]使用标准[!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)]语法，并且提供编译时语法检查、 静态类型和 IntelliSense 支持，在您使用[!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)]IDE。  
  
 有关详细信息，请参阅[LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset.md)。  
  
## <a name="see-also"></a>另请参阅  
 [ADO.NET 概述](../../../../docs/framework/data/adonet/ado-net-overview.md)   
 [数据集、 数据表和数据视图](../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [检索和修改 ADO.NET 中的数据](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)