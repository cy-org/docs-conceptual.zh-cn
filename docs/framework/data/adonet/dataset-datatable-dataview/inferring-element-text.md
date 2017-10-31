---
title: "推断元素文本 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 789799e5-716f-459f-a168-76c5cf22178b
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 推断元素文本
如果元素包含文本但不包含被推断为表的子元素（如具有属性或重复元素的元素），一个名为 **TableName\_Text** 的新列将添加到为该元素推断的表中。  该元素中包含的文本将添加到此表中的一行，并存储在新列中。  新列的 **ColumnMapping** 属性将设置为 **MappingType.SimpleContent**。  
  
 例如，考虑以下 XML。  
  
```  
<DocumentElement>  
  <Element1 attr1="value1">Text1</Element1>  
</DocumentElement>  
```  
  
 推断过程将生成一个名为 **Element1** 的表，该表包含两列：**attr1** 和 **Element1\_Text**。  **attr1** 列的 **ColumnMapping** 属性将设置为 **MappingType.Attribute**。  **Element1\_Text** 列的 **ColumnMapping** 属性将设置为 **MappingType.SimpleContent**。  
  
 **DataSet：**DocumentElement  
  
 **Table：**Element1  
  
|attr1|Element1\_Text|  
|-----------|--------------------|  
|value1|Text1|  
  
 如果某元素包含文本，并且还具有包含文本的子元素，则不会将列添加到表中来存储该元素所包含的文本。  该元素中包含的文本将被忽略，但子元素中的文本将包含在表的一行中。  例如，考虑以下 XML。  
  
```  
<Element1>  
  Text1  
  <ChildElement1>Text2</ChildElement1>  
  Text3  
</Element1>  
```  
  
 推理过程将生成一个名为 **Element1** 的表，它包含一个名为 **ChildElement1** 的列。  **ChildElement1** 元素的文本将包含在表的一行中。  其他文本则将被忽略。  **ChildElement1** 列的 **ColumnMapping** 属性将设置为 **MappingType.Element**。  
  
 **DataSet：**DocumentElement  
  
 **Table：**Element1  
  
|ChildElement1|  
|-------------------|  
|Text2|  
  
## 请参阅  
 [从 XML 推断 DataSet 关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)   
 [从 XML 中加载 DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [从 XML 中加载 DataSet 架构信息](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)   
 [在 DataSet 中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)