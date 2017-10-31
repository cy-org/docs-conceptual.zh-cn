---
title: "用 XSD 形式编写数据集架构信息 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4e530831-695e-49ff-8f0b-e5b0c526b8eb
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 用 XSD 形式编写数据集架构信息
您可以用 XML 架构定义语言 \(XSD\) 架构的形式来编写 <xref:System.Data.DataSet> 的架构，以便在 XML 文档中传输包含或不包含相关数据的架构。  XML 架构可以写入文件、流、<xref:System.Xml.XmlWriter> 或字符串，它对于生成强类型化的 **DataSet** 非常有用。  有关强类型化的 **DataSet** 对象的更多信息，请参见[类型化数据集](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/typed-datasets.md)。  
  
 您可以使用 <xref:System.Data.DataColumn> 对象的 **ColumnMapping** 属性来指定如何在 XML 架构中表示表列。  有关更多信息，请参见[以 XML 数据形式编写数据集内容](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-contents-as-xml-data.md) 中的“将列映射到 XML 元素、属性和文本”。  
  
 若要以 XML 架构形式将 **DataSet** 的架构写入文件、流或 **XmlWriter**，请使用 **DataSet** 的 **WriteXmlSchema** 方法。  **WriteXmlSchema** 接受一个参数，用于指定所生成的 XML 架构的目标。  以下代码示例演示如何通过传递包含文件名的字符串和 <xref:System.IO.StreamWriter> 对象将 **DataSet** 的 XML 架构写入文件。  
  
```vb  
dataSet.WriteXmlSchema("Customers.xsd")  
```  
  
```csharp  
dataSet.WriteXmlSchema("Customers.xsd");  
```  
  
```vb  
Dim writer As System.IO.StreamWriter = New System.IO.StreamWriter("Customers.xsd")  
dataSet.WriteXmlSchema(writer)  
writer.Close()  
```  
  
```csharp  
System.IO.StreamWriter writer = new System.IO.StreamWriter("Customers.xsd");  
dataSet.WriteXmlSchema(writer);  
writer.Close();  
```  
  
 若要获取 **DataSet** 的架构并以 XML 架构字符串的形式来编写该架构，请使用以下示例所示的 **GetXmlSchema** 方法。  
  
```vb  
Dim schemaString As String = dataSet.GetXmlSchema()  
```  
  
```csharp  
string schemaString = dataSet.GetXmlSchema();  
```  
  
## 请参阅  
 [在 DataSet 中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [以 XML 数据形式编写数据集内容](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-contents-as-xml-data.md)   
 [类型化数据集](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/typed-datasets.md)   
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)