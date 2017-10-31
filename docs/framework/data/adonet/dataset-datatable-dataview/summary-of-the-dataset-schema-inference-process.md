---
title: "DataSet 架构推断过程概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fd0891c8-d068-4e30-a76f-7c375f078bf7
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# DataSet 架构推断过程概述
推断过程首先从 XML 文档中确定将哪些元素推断为表。  从剩余的 XML 中，推断过程确定这些表的列。  对于嵌套表，推断过程会生成嵌套的 <xref:System.Data.DataRelation> 和 <xref:System.Data.ForeignKeyConstraint> 对象。  
  
 下面是推断规则的简要概述：  
  
-   具有属性的元素会被推断为表。  
  
-   具有子元素的元素会被推断为表。  
  
-   重复的元素会被推断为单个表。  
  
-   如果文档元素（即根元素）不具有属性和将被推断为列的子元素，则将被推断为 <xref:System.Data.DataSet>。  否则，文档元素会被推断为表。  
  
-   属性会被推断为列。  
  
-   不具有属性或子元素且不重复的元素会被推断为列。  
  
-   如果元素被推断为表，而这些表嵌套在同样被推断为表的其他元素中，则将在两个表之间创建嵌套的 **DataRelation**。  两个表中都将添加一个名为 **TableName\_Id** 的新主键列，该列由 **DataRelation** 来使用。  两个表之间的 **ForeignKeyConstraint** 使用 **TableName\_Id** 列来创建。  
  
-   对于被推断为表的元素和包含文本但不包含子元素的元素，将为每个元素的文本创建一个名为 **TableName\_Text** 的新列。  如果元素被推断为表并包含文本和子元素，则将忽略文本。  
  
## 请参阅  
 [从 XML 推断 DataSet 关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)   
 [从 XML 中加载 DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [从 XML 中加载 DataSet 架构信息](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)   
 [在 DataSet 中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)