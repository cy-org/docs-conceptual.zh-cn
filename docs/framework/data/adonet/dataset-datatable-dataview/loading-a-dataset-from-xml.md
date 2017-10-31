---
title: "从 XML 中加载 DataSet | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 49c083b7-a5ed-41cf-aabc-5aaba96f00e6
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 从 XML 中加载 DataSet
ADO.NET <xref:System.Data.DataSet> 的内容可以从 XML 流或文档创建。  此外，利用 .NET Framework，您可以相当灵活地控制从 XML 中加载哪些信息以及如何创建 <xref:System.Data.DataSet> 的架构（即关系结构）。  
  
 若要使用 XML 中的数据填充 <xref:System.Data.DataSet>，请使用 <xref:System.Data.DataSet> 对象的 **ReadXml** 方法。  该 **ReadXml** 方法将从文件、流或 **XmlReader** 中进行读取，并将 XML 的源以及可选的 **XmlReadMode** 参数用作参数。  （有关 **XmlReader** 的更多信息，请参见[NIB: Reading XML Data with XmlTextReader](http://msdn.microsoft.com/zh-cn/762c069b-b50c-41b8-936e-39eacfb0d540)。）**ReadXml** 方法读取 XML 流或文档的内容并将数据加载到 <xref:System.Data.DataSet> 中。  根据所指定的 **XmlReadMode** 以及关系架构是否已存在，它还将创建 <xref:System.Data.DataSet> 的关系架构。  
  
 下表描述 **XmlReadMode** 参数的选项。  
  
|选项|描述|  
|--------|--------|  
|**Auto**|这是默认设置。  检查 XML 并按如下顺序选择最适合的选项：<br /><br /> -   如果 XML 为 DiffGram，则使用 **DiffGram**。<br />-   如果 <xref:System.Data.DataSet> 包含架构或 XML 包含内联架构，则使用 **ReadSchema**。<br />-   如果 <xref:System.Data.DataSet> 不包含架构且 XML 不包含内联架构，则使用 **InferSchema**。<br /><br /> 如果所读取的 XML 格式已知，为了获得最佳性能，建议设置显式 **XmlReadMode** 而不是接受默认选项 **Auto**。|  
|**ReadSchema**|读取内联架构并加载数据和架构。<br /><br /> 如果 <xref:System.Data.DataSet> 已包含架构，则新表将从内联架构添加到 <xref:System.Data.DataSet> 中的现有架构。  如果 <xref:System.Data.DataSet> 中已存在内联架构中的任何表，则将引发异常。  您将无法使用 **XmlReadMode.ReadSchema** 来修改现有表的架构。<br /><br /> 如果 <xref:System.Data.DataSet> 不包含架构，并且没有内联架构，则不会读取任何数据。<br /><br /> 内联架构可以使用 XML 架构定义语言 \(XSD\) 架构来定义。  有关将内联架构作为 XML 架构编写的详细信息，请参见[从 XML 架构 \(XSD\) 派生数据集关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)。|  
|**IgnoreSchema**|忽略任何内联架构并将数据加载到现有的 <xref:System.Data.DataSet> 架构中。  任何与现有架构不匹配的数据都将被丢弃。  如果 <xref:System.Data.DataSet> 中不存在任何架构，则不会加载任何数据。<br /><br /> 如果数据为 DiffGram，则 **IgnoreSchema** 与 **DiffGram** 具有相同的功能。|  
|**InferSchema**|忽略任何内联架构并按照 XML 数据的结构推断架构，然后加载数据。<br /><br /> 如果 <xref:System.Data.DataSet> 已经包含架构，则会通过向现有表中添加列来扩展当前架构。  如果不存在表，则不会添加其他表。  如果已存在具有不同命名空间的推断表或者任何推断表与现有列发生冲突，则会引发异常。<br /><br /> 有关 **ReadXmlSchema** 如何从 XML 文档推断架构的详细信息，请参见[从 XML 推断 DataSet 关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)。|  
|**DiffGram**|读取 DiffGram 并将数据添加到当前架构中。  **DiffGram** 会将新行和唯一标识符值匹配的现有行合并。  请参见本主题末尾的“合并 XML 中的数据”。  有关 DiffGrams 的更多信息，请参见 [DiffGram](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/diffgrams.md)。|  
|**Fragment**|持续读取多个 XML 片断，直至到达流的末尾。  与 <xref:System.Data.DataSet> 架构匹配的片断会追加到相应的表。  与 <xref:System.Data.DataSet> 架构不匹配的片断将被丢弃。|  
  
> [!NOTE]
>  如果将 **XmlReader** 传递到未完全放入 XML 文档的 **ReadXml** 中，**ReadXml** 将读取至下一个元素节点并将其当作根元素，这种读取仅持续到元素节点末尾。  这在指定 **XmlReadMode.Fragment** 时不适用。  
  
## DTD 实体  
 如果 XML 包含在文档类型定义 \(DTD\) 架构中定义的实体，那么当试图通过向 **ReadXml** 传递文件名、流或非验证 **XmlReader** 来加载 <xref:System.Data.DataSet> 时，将引发异常。  因此，您必须在将 **EntityHandling** 设置为 **EntityHandling.ExpandEntities** 的情况下创建一个 **XmlValidatingReader**，然后将该 **XmlValidatingReader** 传递到 **ReadXml**。  该 **XmlValidatingReader** 将在 <xref:System.Data.DataSet> 读取之前扩展实体。  
  
 以下代码示例显示如何从 XML 流中加载 <xref:System.Data.DataSet>。  第一个示例显示向 **ReadXml** 方法传递的文件名。  第二个示例显示一个字符串，包含使用 <xref:System.IO.StringReader> 加载的 XML。  
  
```vb  
Dim dataSet As DataSet = New DataSet  
dataSet.ReadXml("input.xml", XmlReadMode.ReadSchema)  
```  
  
```csharp  
DataSet dataSet = new DataSet();  
dataSet.ReadXml("input.xml", XmlReadMode.ReadSchema);  
```  
  
```vb  
Dim dataSet As DataSet = New DataSet  
Dim dataTable As DataTable = New DataTable("table1")  
dataTable.Columns.Add("col1", Type.GetType("System.String"))  
dataSet.Tables.Add(dataTable)  
  
Dim xmlData As String = "<XmlDS><table1><col1>Value1</col1></table1><table1><col1>Value2</col1></table1></XmlDS>"  
  
Dim xmlSR As System.IO.StringReader = New System.IO.StringReader(xmlData)  
  
dataSet.ReadXml(xmlSR, XmlReadMode.IgnoreSchema)  
```  
  
```csharp  
DataSet dataSet = new DataSet();  
DataTable dataTable = new DataTable("table1");  
dataTable.Columns.Add("col1", typeof(string));  
dataSet.Tables.Add(dataTable);  
  
string xmlData = "<XmlDS><table1><col1>Value1</col1></table1><table1><col1>Value2</col1></table1></XmlDS>";  
  
System.IO.StringReader xmlSR = new System.IO.StringReader(xmlData);  
  
dataSet.ReadXml(xmlSR, XmlReadMode.IgnoreSchema);  
```  
  
> [!NOTE]
>  如果调用 **ReadXml** 来加载非常大的文件，则性能可能会下降。  为确保最佳的 **ReadXml** 性能，对于大文件，请为 <xref:System.Data.DataSet> 中的每个表调用 <xref:System.Data.DataTable.BeginLoadData%2A> 方法，然后调用 **ReadXml**。  最后，为 <xref:System.Data.DataSet> 中的每个表调用 <xref:System.Data.DataTable.EndLoadData%2A>，如下面的示例所示。  
  
```vb  
Dim dataTable As DataTable  
  
For Each dataTable In dataSet.Tables  
   dataTable.BeginLoadData()  
Next  
  
dataSet.ReadXml("file.xml")  
  
For Each dataTable in dataSet.Tables  
   dataTable.EndLoadData()  
Next  
```  
  
```csharp  
foreach (DataTable dataTable in dataSet.Tables)  
   dataTable.BeginLoadData();  
  
dataSet.ReadXml("file.xml");   
  
foreach (DataTable dataTable in dataSet.Tables)  
   dataTable.EndLoadData();  
```  
  
> [!NOTE]
>  如果您的 <xref:System.Data.DataSet> 的 XML 架构包含 **targetNamespace**，则可能无法读取数据，而且在调用 **ReadXml** 以加载所含 XML 中包含的元素有非限定命名空间的 <xref:System.Data.DataSet> 时，可能会发生异常。  在这种情况下，若要读取未限定的元素，请在 XSD 架构中将 **elementFormDefault** 设置为等于“qualified”。  例如：  
  
```  
<xsd:schema id="customDataSet"   
  elementFormDefault="qualified"  
  targetNamespace="http://www.tempuri.org/customDataSet.xsd"   
  xmlns="http://www.tempuri.org/customDataSet.xsd"   
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
  xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
</xsd:schema>  
```  
  
## 合并 XML 中的数据  
 如果 <xref:System.Data.DataSet> 已经包含数据，则会向已存在于 <xref:System.Data.DataSet> 中的数据添加 XML 中的新数据。  **ReadXml** 不会从 XML 向 <xref:System.Data.DataSet> 中并入任何具有匹配主键的行信息。  若要使用 XML 中的新信息覆盖现有行信息，请使用 **ReadXml** 创建新的 <xref:System.Data.DataSet>，然后将新的 <xref:System.Data.DataSet> <xref:System.Data.DataSet.Merge%2A> 到现有 <xref:System.Data.DataSet> 中。  请注意，如果使用 **XmlReadMode** 为 **DiffGram** 的 **ReadXML** 来加载 DiffGram，则将合并具有相同唯一标识符的行。  
  
## 请参阅  
 <xref:System.Data.DataSet.Merge%2A?displayProperty=fullName>   
 [在 DataSet 中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [DiffGram](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/diffgrams.md)   
 [从 XML 架构 \(XSD\) 派生数据集关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)   
 [从 XML 推断 DataSet 关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)   
 [从 XML 中加载 DataSet 架构信息](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)   
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)