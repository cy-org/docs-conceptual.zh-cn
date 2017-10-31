---
title: "推断列 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0e022699-c922-454c-93e2-957dd7e7247a
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 推断列
ADO.NET 从 XML 文档中确定了哪些元素要作为 <xref:System.Data.DataSet> 的表进行推断后，即开始推断这些表的列。  ADO.NET 2.0 引入了一个新的架构推断引擎，可推断每个 **simpleType** 元素的强类型化的数据类型。  在以前的版本中，推断的 **simpleType** 元素的数据类型总是 **xsd:string**。  
  
## 迁移和向后兼容性  
 **ReadXml** 方法接受 **InferSchema** 类型的参数。  使用此参数可以指定与以前的版本兼容的推断行为。  **InferSchema** 枚举的可用值显示在下表中。  
  
 <xref:System.Data.XmlReadMode>  
 通过始终将简单类型作为 <xref:System.String> 进行推断，提供向后兼容性。  
  
 <xref:System.Data.XmlReadMode>  
 推断强类型化的数据类型。  如果与 <xref:System.Data.DataTable> 一起使用，会发生异常。  
  
 <xref:System.Data.XmlReadMode>  
 忽略任何内联架构并将数据读入现有的 <xref:System.Data.DataSet> 架构。  
  
## 特性  
 正如[推断表](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-tables.md)中的定义，具有属性的元素将被推断为表。  然后，该元素的属性将被推断为该表的列。  这些列的 **ColumnMapping** 属性将设置为 **MappingType.Attribute**，以确保列名称将在架构写回 XML 时被写为属性。  这些属性的值存储在表的行中。  例如，考虑以下 XML：  
  
```  
<DocumentElement>  
  <Element1 attr1="value1" attr2="value2"/>  
</DocumentElement>  
```  
  
 推断过程将生成一个名为 **Element1** 的表，它包含两个列：**attr1** 和 **attr2**。  这两个列的 **ColumnMapping** 属性都将设置为 **MappingType.Attribute**。  
  
 **DataSet：**DocumentElement  
  
 **Table：**Element1  
  
|attr1|attr2|  
|-----------|-----------|  
|value1|value2|  
  
## 不具有属性或子元素的元素  
 如果元素不具有子元素或属性，它将被推断为列。  列的 **ColumnMapping** 属性将设置为 **MappingType.Element**。  子元素的文本存储在表的行中。  例如，考虑以下 XML：  
  
```  
<DocumentElement>  
  <Element1>  
    <ChildElement1>Text1</ChildElement1>  
    <ChildElement2>Text2</ChildElement2>  
  </Element1>  
</DocumentElement>  
```  
  
 推断过程将生成一个名为 **Element1** 的表，它包含两个列：**ChildElement1** 和 **ChildElement2**。  这两个列的 **ColumnMapping** 属性将设置为 **MappingType.Element**。  
  
 **DataSet：**DocumentElement  
  
 **Table：**Element1  
  
|ChildElement1|ChildElement2|  
|-------------------|-------------------|  
|Text1|Text2|  
  
## 请参阅  
 [从 XML 推断 DataSet 关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)   
 [从 XML 中加载 DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [从 XML 中加载 DataSet 架构信息](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)   
 [在 DataSet 中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)