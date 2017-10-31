---
title: "推断限制 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 78517994-5d57-44f8-9d20-38812977de09
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 推断限制
根据每个文档中的 XML 元素，从 XML 推断 <xref:System.Data.DataSet> 架构的过程会产生不同的架构。  例如，考虑以下 XML 文档。  
  
 Document1：  
  
```  
<DocumentElement>  
  <Element1>Text1</Element1>  
  <Element1>Text2</Element1>  
</DocumentElement>  
```  
  
 Document2：  
  
```  
<DocumentElement>  
  <Element1>Text1</Element1>  
</DocumentElement>  
```  
  
 对于“Document1”，由于“Element1”是重复元素，推断过程将生成一个名为“DocumentElement”的 **DataSet** 和一个名为“Element1”的表。  
  
 **DataSet：**DocumentElement  
  
 **Table：**Element1  
  
|Element1\_Text|  
|--------------------|  
|Text1|  
|Text2|  
  
 但是，对于“Document2”，推断过程将生成一个名为“NewDataSet”的 **DataSet** 和一个名为“DocumentElement”的表。由于“Element1”不具有属性和子元素，它将被推断为列。  
  
 **DataSet：**NewDataSet  
  
 **Table：**DocumentElement  
  
|Element1|  
|--------------|  
|Text1|  
  
 这两个 XML 文档可能本应生成相同的架构，但根据每个文档中包含的不同元素，推断过程生成了极不相同的结果。  
  
 为了避免在从 XML 文档生成架构时可能出现的差异，建议在从 XML 中加载 **DataSet** 时使用 XML 架构定义语言 \(XSD\) 或 XML 数据缩减 \(XDR\) 显式地指定架构。  有关使用 XML 架构显式指定 **DataSet** 架构的更多信息，请参见[从 XML 架构 \(XSD\) 派生数据集关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)。  
  
## 请参阅  
 [从 XML 推断 DataSet 关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)   
 [从 XML 中加载 DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [从 XML 中加载 DataSet 架构信息](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)   
 [在 DataSet 中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)