---
title: "将 XML 架构 (XSD) 约束映射到 DataSet 约束 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3d0d1a4b-9104-434f-ac04-6c01ab5716b5
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 将 XML 架构 (XSD) 约束映射到 DataSet 约束
XML 架构定义语言 \(XSD\) 允许对它所定义的元素和属性指定约束。  在将 XML 架构映射到 <xref:System.Data.DataSet> 中的关系架构时，XML 架构约束将映射到 **DataSet** 中表和列上的相应关系约束。  
  
 本节讨论以下 XML 架构约束的映射：  
  
-   使用 **unique** 元素指定的唯一约束。  
  
-   使用 **key** 元素指定的键约束。  
  
-   使用 **keyref** 元素指定的 keyref 约束。  
  
 使用对元素或属性的约束，可以对任何文档实例中元素的值指定特定的限制。  例如，对架构中 **Customer** 元素的 **CustomerID** 子元素的某一键约束指示 **CustomerID** 子元素的值必须在任何文档实例中都是唯一的，并且不允许空值。  
  
 为了在文档中建立关系，也可以在文档中的元素和属性之间指定约束。  key 和 keyref 约束用于在架构中指定文档中的约束，从而生成文档元素和属性之间的关系。  
  
 映射进程将这些架构约束转换为在 **DataSet** 中创建的表上的相应约束。  
  
## 本节内容  
 [将唯一 XML 架构 \(XSD\) 约束映射为数据集约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/map-unique-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 描述用于在 **DataSet** 中创建唯一约束的 XML 架构元素。  
  
 [将键 XML 架构 \(XSD\) 约束映射为数据集约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/map-key-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 描述用于在 **DataSet** 中创建键约束（不允许空值的唯一约束）的 XML 架构元素。  
  
 [将 keyref XML 架构 \(XSD\) 约束映射为数据集约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/map-keyref-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 描述用于在 **DataSet** 中创建 keyref（外键）约束的 XML 架构元素。  
  
## 相关章节  
 [从 XML 架构 \(XSD\) 派生数据集关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 描述从 XSD 架构创建的 **DataSet** 的关系结构（即架构）。  
  
 [从 XML 架构 \(XSD\) 生成 DataSet 关系](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)  
 描述用于在 **DataSet** 中各表列间创建关系的 XML 架构元素。  
  
## 请参阅  
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)