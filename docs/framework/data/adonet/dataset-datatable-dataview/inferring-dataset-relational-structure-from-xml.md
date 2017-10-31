---
title: "从 XML 推断 DataSet 关系结构 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cd2f41c6-6785-420e-aa43-3ceb0bdccdce
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 从 XML 推断 DataSet 关系结构
<xref:System.Data.DataSet> 的关系结构（即架构）由表、列、约束和关系组成。  当从 XML 中加载 <xref:System.Data.DataSet> 时，可以预定义架构，也可以从所加载的 XML 显式（或通过推断）创建架构。  有关从 XML 加载 <xref:System.Data.DataSet> 的架构和内容的更多信息，请参见[从 XML 中加载 DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)和[从 XML 中加载 DataSet 架构信息](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)。  
  
 如果正在从 XML 创建 <xref:System.Data.DataSet> 的架构，首选方法是使用 XML 架构定义语言 \(XSD\)（在[从 XML 架构 \(XSD\) 派生数据集关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)中描述）或 XML 数据缩减 \(XDR\) 来显式指定架构。  如果 XML 中没有可用的 XML 架构或 XDR 架构，则可以从 XML 元素和属性的结构推断 <xref:System.Data.DataSet> 的架构。  
  
 本节通过显示 XML 元素和属性及其结构以及生成的推断 <xref:System.Data.DataSet> 架构来描述推断 <xref:System.Data.DataSet> 架构的规则。  
  
 并非所有出现在 XML 文档中的属性都应包含在推断过程中。  由命名空间限定的属性可以包含对 XML 文档重要但对 <xref:System.Data.DataSet> 架构不重要的元数据。  使用 <xref:System.Data.DataSet.InferXmlSchema%2A>，您可以指定要在推断过程中忽略的命名空间。  有关详细信息，请参阅[从 XML 中加载 DataSet 架构信息](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)。  
  
## 本节内容  
 [DataSet 架构推断过程概述](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/summary-of-the-dataset-schema-inference-process.md)  
 提供从 XML 推断 <xref:System.Data.DataSet> 架构的规则的简要概述。  
  
 [推断表](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-tables.md)  
 描述被推断为 <xref:System.Data.DataSet> 中的表的 XML 元素。  
  
 [推断列](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-columns.md)  
 描述被推断为表列的 XML 元素和属性。  
  
 [推断关系](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-relationships.md)  
 描述为嵌套的推断表创建的 <xref:System.Data.DataRelation> 和 <xref:System.Data.ForeignKeyConstraint> 对象。  
  
 [推断元素文本](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-element-text.md)  
 描述为 XML 元素中的文本创建的列，并解释何时会忽略 XML 元素中的文本。  
  
 [推断限制](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inference-limitations.md)  
 讨论架构推断的限制。  
  
## 相关章节  
 [在 DataSet 中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)  
 描述 <xref:System.Data.DataSet> 对象如何与 XML 数据进行交互。  
  
 [从 XML 架构 \(XSD\) 派生数据集关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 描述从 XML 架构定义语言 \(XSD\) 架构创建的 <xref:System.Data.DataSet> 的关系结构（即架构）。  
  
 [ADO.NET 概述](../../../../../docs/framework/data/adonet/ado-net-overview.md)  
 描述 ADO.NET 结构和组件，并说明如何用来访问现有的数据源和管理应用程序数据。  
  
## 请参阅  
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)