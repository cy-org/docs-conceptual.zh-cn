---
title: "推断表 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 74a288d4-b8e9-4f1a-b2cd-10df92c1ed1f
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 推断表
当从 XML 文档推断 <xref:System.Data.DataSet> 的架构时，ADO.NET 首先会确定哪些 XML 元素表示表。  以下 XML 结构为 **DataSet** 架构生成表：  
  
-   具有属性的元素  
  
-   具有子元素的元素  
  
-   重复元素  
  
## 具有属性的元素  
 在其中指定了属性的元素将生成推断表。  例如，考虑以下 XML：  
  
```  
<DocumentElement>  
  <Element1 attr1="value1"/>  
  <Element1 attr1="value2">Text1</Element1>  
</DocumentElement>  
```  
  
 推断过程将生成名为“Element1”的表。  
  
 **DataSet：**DocumentElement  
  
 **Table：**Element1  
  
|attr1|Element1\_Text|  
|-----------|--------------------|  
|value1||  
|value2|Text1|  
  
## 具有子元素的元素  
 具有子元素的元素将生成推断表。  例如，考虑以下 XML：  
  
```  
<DocumentElement>  
  <Element1>  
    <ChildElement1>Text1</ChildElement1>  
  </Element1>  
</DocumentElement>  
```  
  
 推断过程将生成名为“Element1”的表。  
  
 **DataSet：**DocumentElement  
  
 **Table：**Element1  
  
|ChildElement1|  
|-------------------|  
|Text1|  
  
 如果文档元素（即根元素）具有将被推断为列的属性或子元素，将生成推断表。  如果文档元素不具有将被推断为列的属性和子元素，则该元素将被推断为 **DataSet**。  例如，考虑以下 XML：  
  
```  
<DocumentElement>  
  <Element1>Text1</Element1>  
  <Element2>Text2</Element2>  
</DocumentElement>  
```  
  
 推断过程将生成名为“DocumentElement”的表。  
  
 **DataSet：**NewDataSet  
  
 **Table：**DocumentElement  
  
|Element1|Element2|  
|--------------|--------------|  
|Text1|Text2|  
  
 或者，考虑以下 XML：  
  
```  
<DocumentElement>  
  <Element1 attr1="value1" attr2="value2"/>  
</DocumentElement>  
```  
  
 推断过程将生成一个名为“DocumentElement”的 **DataSet**，包含一个名为“Element1”的表。  
  
 **DataSet：**DocumentElement  
  
 **Table：**Element1  
  
|attr1|attr2|  
|-----------|-----------|  
|value1|value2|  
  
## 重复元素  
 重复的元素将生成单个推断表。  例如，考虑以下 XML：  
  
```  
<DocumentElement>  
  <Element1>Text1</Element1>  
  <Element1>Text2</Element1>  
</DocumentElement>  
```  
  
 推断过程将生成名为“Element1”的表。  
  
 **DataSet：**DocumentElement  
  
 **Table：**Element1  
  
|Element1\_Text|  
|--------------------|  
|Text1|  
|Text2|  
  
## 请参阅  
 [从 XML 推断 DataSet 关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)   
 [从 XML 中加载 DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [从 XML 中加载 DataSet 架构信息](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)   
 [在 DataSet 中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)