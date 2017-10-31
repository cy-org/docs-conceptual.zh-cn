---
title: "写入数据集内容作为 XML 数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fd15f8a5-3b4c-46d0-a561-4559ab2a4705
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# 写入数据集内容作为 XML 数据
可以在 ADO.NET 中编写的 XML 表示形式<xref:System.Data.DataSet>、 使用或不包含其架构。 如果架构信息以内联形式包含在 XML 表示形式中，则使用 XML 架构定义语言 (XSD) 来编写。 架构包含的表定义<xref:System.Data.DataSet>以及关系和约束定义。  
  
 当<xref:System.Data.DataSet>作为 XML 数据中的行写入<xref:System.Data.DataSet>以其当前版本编写。 但是，<xref:System.Data.DataSet>，以便将包括当前和原始值的行也可以以 diffgram 形式写入。  
  
 XML 表示形式<xref:System.Data.DataSet>可以写入文件、 流、 **XmlWriter**，或字符串。 这些选项如何传输的 XML 表示形式提供极大的灵活性<xref:System.Data.DataSet>。 若要获取的 XML 表示形式<xref:System.Data.DataSet>作为一个字符串，使用**GetXml**方法，如下面的示例所示。  
  
```vb  
Dim xmlDS As String = custDS.GetXml()  
```  
  
```csharp  
string xmlDS = custDS.GetXml();  
```  
  
 **GetXml**返回的 XML 表示形式<xref:System.Data.DataSet>不包含架构信息。 若要从架构信息写入<xref:System.Data.DataSet>（作为 XML 架构） 化为一个字符串，使用**GetXmlSchema**。  
  
 若要编写<xref:System.Data.DataSet>到文件中，流，或**XmlWriter**，使用**WriteXml**方法。 第一个参数传递给**WriteXml**目标的 XML 输出。 例如，传递包含文件名，string **System.IO.TextWriter**对象，依次类推。 可以传递另一个可选参数**XmlWriteMode**来指定如何编写 XML 输出。  
  
 下表显示的选项**XmlWriteMode**。  
  
|XmlWriteMode 选项|说明|  
|-------------------------|-----------------|  
|**IgnoreSchema**|当前的内容写入<xref:System.Data.DataSet>作为 XML 数据，不包含 XML 架构。 这是默认设置。|  
|**WriteSchema**|当前的内容写入<xref:System.Data.DataSet>以与关系结构作为内联 XML 架构的 XML 数据形式。|  
|**DiffGram**|编写整个<xref:System.Data.DataSet>以 diffgram 形式，包括原始值和当前值。 有关详细信息，请参阅[Diffgram](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/diffgrams.md)。|  
  
 在编写的 XML 表示形式时<xref:System.Data.DataSet>，其中包含**DataRelation**对象时，您很可能希望生成的 XML 将每个关系嵌套在它们相关的父元素的子行。 若要实现此目的，将设置**嵌套**属性**DataRelation**到**true**时添加**DataRelation**到<xref:System.Data.DataSet>。 有关详细信息，请参阅[嵌套 Datarelation](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)。  
  
 以下是两个示例说明了如何以 XML 表示形式写入<xref:System.Data.DataSet>到文件。 第一个示例将生成的 XML 的文件名传递到字符串形式**WriteXml**。 第二个示例传递**System.IO.StreamWriter**对象。  
  
```vb  
custDS.WriteXml("Customers.xml", XmlWriteMode.WriteSchema)  
  
```  
  
```csharp  
custDS.WriteXml("Customers.xml", XmlWriteMode.WriteSchema);  
  
```  
  
```vb  
Dim xmlSW As System.IO.StreamWriter = New System.IO.StreamWriter("Customers.xml")  
custDS.WriteXml(xmlSW, XmlWriteMode.WriteSchema)  
xmlSW.Close()  
  
```  
  
```csharp  
System.IO.StreamWriter xmlSW = new System.IO.StreamWriter("Customers.xml");  
custDS.WriteXml(xmlSW, XmlWriteMode.WriteSchema);  
xmlSW.Close();  
```  
  
## <a name="mapping-columns-to-xml-elements-attributes-and-text"></a>将列映射到 XML 元素、属性和文本  
 您可以指定以 XML 方式表示表的列使用**ColumnMapping**属性**DataColumn**对象。 下表显示了不同**MappingType**值**ColumnMapping**的表列，以及生成的 XML 属性。  
  
|MappingType 值|描述|  
|-----------------------|-----------------|  
|**元素**|这是默认设置。 列以元素名称为 ColumnName 的 XML 元素形式编写，列的内容以元素文本形式编写。 例如: <br /><br /> `<ColumnName>Column Contents</ColumnName>`|  
|**属性**|对于属性名称为 ColumnName 的当前行，列以 XML 元素的 XML 属性形式编写，列的内容以属性值形式编写。 例如: <br /><br /> `<RowElement ColumnName="Column Contents" />`|  
|**SimpleContent**|列的内容以 XML 元素中当前行文本的形式编写。 例如: <br /><br /> `<RowElement>Column Contents</RowElement>`<br /><br /> 请注意， **SimpleContent**无法为一个表，该表的列设置**元素**列或嵌套的关系。|  
|**隐藏**|不在 XML 输出中编写该列。|  
  
## <a name="see-also"></a>另请参阅  
 [在数据集中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [Diffgram](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/diffgrams.md)   
 [嵌套 Datarelation](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)   
 [写入数据集架构信息作为 XSD](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-schema-information-as-xsd.md)   
 [数据集、 数据表和数据视图](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)