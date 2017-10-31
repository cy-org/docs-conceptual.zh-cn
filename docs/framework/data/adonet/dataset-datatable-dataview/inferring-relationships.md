---
title: "推断关系 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8fa86a9d-6545-4a9d-b1f5-58d9742179c7
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 推断关系
如果被推断为表的元素具有一个同样被推断为表的子元素，则将在这两个表之间创建 <xref:System.Data.DataRelation>。  一个名为 **ParentTableName\_Id** 的新列将添加到为父元素创建的表以及为子元素创建的表中。  此标识列的 **ColumnMapping** 属性将设置为 **MappingType.Hidden**。  该列将成为父表的自动递增主键，并将用于两个表之间的 **DataRelation**。  所添加的标识列的数据类型将为 **System.Int32**，与所有其他被推断的列的数据类型不同，后者的数据类型为 **System.String**。  **DeleteRule** \= **Cascade** 的 <xref:System.Data.ForeignKeyConstraint> 也将使用父表和子表中的新列创建。  
  
 例如，考虑以下 XML：  
  
```  
<DocumentElement>  
  <Element1>  
    <ChildElement1 attr1="value1" attr2="value2"/>  
    <ChildElement2>Text2</ChildElement2>  
  </Element1>  
</DocumentElement>  
```  
  
 推理过程将生成两个表：**Element1** 和 **ChildElement1**。  
  
 **Element1** 表具有两个列：**Element1\_Id** 和 **ChildElement2**。  **Element1\_Id** 列的 **ColumnMapping** 属性将设置为 **MappingType.Hidden**。  **ChildElement2** 列的 **ColumnMapping** 属性将设置为 **MappingType.Element**。  **Element1\_Id** 列将设置为 **Element1** 表的主键。  
  
 **ChildElement1** 表具有三个列：**attr1**、**attr2** 和 **Element1\_Id**。  **attr1** 和 **attr2** 列的 **ColumnMapping** 属性将设置为 **MappingType.Attribute**。  **Element1\_Id** 列的 **ColumnMapping** 属性将设置为 **MappingType.Hidden**。  
  
 **DataRelation** 和 **ForeignKeyConstraint** 将使用两个表中的 **Element1\_Id** 列来创建。  
  
 **DataSet：**DocumentElement  
  
 **Table：**Element1  
  
|Element1\_Id|ChildElement2|  
|------------------|-------------------|  
|0|Text2|  
  
 **Table：**ChildElement1  
  
|attr1|attr2|Element1\_Id|  
|-----------|-----------|------------------|  
|value1|value2|0|  
  
 **DataRelation：**Element1\_ChildElement1  
  
 **ParentTable：**Element1  
  
 **ParentColumn：**Element1\_Id  
  
 **ChildTable：**ChildElement1  
  
 **ChildColumn：**Element1\_Id  
  
 **Nested：**True  
  
 **ForeignKeyConstraint：**Element1\_ChildElement1  
  
 **Column：**Element1\_Id  
  
 **ParentTable：**Element1  
  
 **ChildTable：**ChildElement1  
  
 **DeleteRule：**Cascade  
  
 **AcceptRejectRule：**None  
  
## 请参阅  
 [从 XML 推断 DataSet 关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)   
 [从 XML 中加载 DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [从 XML 中加载 DataSet 架构信息](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)   
 [嵌套 DataRelation](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)   
 [在 DataSet 中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)