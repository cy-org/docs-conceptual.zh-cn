---
title: "从 XML 中加载 DataSet 架构信息 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 43dfb23b-5cef-46f2-8d87-78f0fba1eb8c
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 从 XML 中加载 DataSet 架构信息
<xref:System.Data.DataSet> 的架构（它的表、列、关系和约束）可以通过编程来定义，使用 <xref:System.Data.Common.DataAdapter> 的 **Fill** 或 **FillSchema** 方法来创建，或从 XML 文档中加载。  若要从 XML 文档中加载 **DataSet** 架构信息，可以使用 **DataSet** 的 **ReadXmlSchema** 或 **InferXmlSchema** 方法。  **ReadXmlSchema** 用于从包含 XML 架构定义语言 \(XSD\) 架构的文档或包含内联 XML 架构的 XML 文档加载或推断 **DataSet** 架构信息。  **InferXmlSchema** 用于在从 XML 文档推断架构时忽略所指定的特定 XML 命名空间。  
  
> [!NOTE]
>  使用 Web 服务或 XML 序列化传输采用 XSD 构造（如嵌套关系）在内存中创建的 **DataSet** 时，可能不会保留 **DataSet** 中的表顺序。  因此，在这种情况下，**DataSet** 的接收人不应依赖表顺序。  但是，如果要传输的 **DataSet** 的架构是从 XSD 文件读取的，而不是在内存中创建的，则会始终保留表顺序。  
  
## ReadXmlSchema  
 若要从 XML 文档中加载 **DataSet** 的架构而不加载任何数据，可以使用 **DataSet** 的 **ReadXmlSchema** 方法。  **ReadXmlSchema** 创建使用 XML 架构定义语言 \(XSD\) 架构定义的 **DataSet** 架构。  
  
 **ReadXmlSchema** 方法接受单个参数，如文件名、流或包含要加载的 XML 文档的 **XmlReader**。  XML 文档可以仅包含架构，也可以包含与包含数据的 XML 元素内联的架构。  有关将内联架构作为 XML 架构编写的详细信息，请参见[从 XML 架构 \(XSD\) 派生数据集关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)。  
  
 如果传递给 **ReadXmlSchema** 的 XML 文档不包含内联架构信息，则 **ReadXmlSchema** 将根据 XML 文档中的元素推断该架构。  如果 **DataSet** 已包含架构，则会在表不存在的情况下通过添加新表来扩展当前架构。  不会将新列添加到现有表中。  如果所添加的列已存在于 **DataSet** 中但该列的类型与 XML 中的相应列不兼容，则将引发异常。  有关 **ReadXmlSchema** 如何从 XML 文档推断架构的详细信息，请参见[从 XML 推断 DataSet 关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)。  
  
 尽管 **ReadXmlSchema** 仅加载或推断 **DataSet** 的架构，但是 **DataSet** 的 **ReadXml** 方法则将加载或推断 XML 文档中包含的架构和数据。  有关详细信息，请参阅[从 XML 中加载 DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)。  
  
 以下代码示例显示如何从 XML 文档或流中加载 **DataSet** 架构。  第一个示例显示向 **ReadXmlSchema** 方法传递的 XML 架构文件名。  第二个示例显示一个 **System.IO.StreamReader**。  
  
```vb  
Dim dataSet As DataSet = New DataSet  
dataSet.ReadXmlSchema("schema.xsd")  
```  
  
```csharp  
DataSet dataSet = new DataSet();  
dataSet.ReadXmlSchema("schema.xsd");  
```  
  
```vb  
Dim xmlStream As System.IO.StreamReader = New System.IO.StreamReader ("schema.xsd");  
Dim dataSet As DataSet = New DataSet  
dataSet.ReadXmlSchema(xmlStream)  
xmlStream.Close()  
```  
  
```csharp  
System.IO.StreamReader xmlStream = new System.IO.StreamReader("schema.xsd");  
DataSet dataSet = new DataSet();  
dataSet.ReadXmlSchema(xmlStream);  
xmlStream.Close();  
```  
  
## InferXmlSchema  
 您也可以指示 **DataSet** 使用 **DataSet** 的 **InferXmlSchema** 方法来从 XML 文档推断其架构。  **InferXmlSchema** 的功能与 **XmlReadMode** 为 **InferSchema** 的 **ReadXml**（加载数据并推断架构）以及所读取的文档不包含任何内联架构时的 **ReadXmlSchema** 相同。  但是，**InferXmlSchema** 还提供了其他功能，使您能够指定在推断架构时所忽略的特定 XML 命名空间。  **InferXmlSchema** 采用两个必需的参数：XML 文档的位置，由文件名、流或 **XmlReader** 指定；以及要在该操作中忽略的 XML 命名空间的字符串数组。  
  
 例如，考虑以下 XML：  
  
```  
<NewDataSet xmlns:od="urn:schemas-microsoft-com:officedata">  
<Categories>  
  <CategoryID od:adotype="3">1</CategoryID>   
  <CategoryName od:maxLength="15" od:adotype="130">Beverages</CategoryName>   
  <Description od:adotype="203">Soft drinks and teas</Description>   
</Categories>  
<Products>  
  <ProductID od:adotype="20">1</ProductID>   
  <ReorderLevel od:adotype="3">10</ReorderLevel>   
  <Discontinued od:adotype="11">0</Discontinued>   
</Products>  
</NewDataSet>  
```  
  
 考虑到为上述 XML 文档中元素指定的属性，具有 **InferSchema** 的 **XmlReadMode** 的 **ReadXmlSchema** 方法和 **ReadXml** 方法将为该文档中的每个元素创建表：**Categories**、**CategoryID**、**CategoryName**、**Description**、**Products**、**ProductID**、**ReorderLevel** 和 **Discontinued**。  （有关详细信息，请参阅 [从 XML 推断 DataSet 关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)。）但是，更为合适的结构是仅创建 **Categories** 和 **Products** 表，然后在 **Categories** 表中创建 **CategoryID**、**CategoryName** 和 **Description** 列，并在 **Products** 表中创建 **ProductID**、**ReorderLevel** 和 **Discontinued** 列。  若要确保推断架构忽略在 XML 元素中指定的属性，请使用 **InferXmlSchema** 方法，并为要忽略的 **officedata** 指定 XML 命名空间（如下例所示）。  
  
```vb  
Dim dataSet As DataSet = New DataSet  
dataSet.InferXmlSchema("input_od.xml", New String() {"urn:schemas-microsoft-com:officedata"})  
```  
  
```csharp  
DataSet dataSet = new DataSet();  
dataSet.InferXmlSchema("input_od.xml", new string[] "urn:schemas-microsoft-com:officedata");  
```  
  
## 请参阅  
 [在 DataSet 中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [从 XML 架构 \(XSD\) 派生数据集关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)   
 [从 XML 推断 DataSet 关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)   
 [从 XML 中加载 DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)