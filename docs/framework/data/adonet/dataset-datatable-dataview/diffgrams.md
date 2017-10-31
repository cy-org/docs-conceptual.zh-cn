---
title: "DiffGram | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 037f3991-7bbc-424b-b52e-8b03585d3e34
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# DiffGram
DiffGram 是用于标识数据元素的当前和原始版本的 XML 格式。  <xref:System.Data.DataSet> 使用 DiffGram 格式来加载和保持其内容，并将其内容序列化，以便通过网络连接来进行传输。  当 <xref:System.Data.DataSet> 以 DiffGram 形式来编写时，它会为 DiffGram 填充所有必要的信息，以便精确地重新创建 <xref:System.Data.DataSet> 的内容（但不包括其架构），其中包括 **Original** 和 **Current** 行版本、行错误信息以及行顺序的列值。  
  
 当从 XML Web services 发送和检索 <xref:System.Data.DataSet> 时，将隐式地使用 DiffGram 格式。  此外，当使用 **ReadXml** 方法从 XML 加载 <xref:System.Data.DataSet> 的内容时，或当使用 **WriteXml** 方法以 XML 编写 <xref:System.Data.DataSet> 的内容时，可以指定内容作为 DiffGram 读取或写入。  有关详细信息，请参阅[从 XML 中加载 DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)和[以 XML 数据形式编写数据集内容](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-contents-as-xml-data.md)。  
  
 虽然 DiffGram 格式主要由 .NET Framework 用作 <xref:System.Data.DataSet> 内容的序列化格式，但也可以使用 DiffGram 来修改 Microsoft SQL Server 数据库中表的数据。  
  
 通过将所有表的内容写入到 **\<diffgram\>** 元素中可生成 Diffgram。  
  
### 生成 Diffgram  
  
1.  生成根表（即没有任何父级的表）的列表。  
  
2.  对于列表中每个表及其子代，在 Diffgram 的第一部分中写出所有行的当前版本。  
  
3.  对于 <xref:System.Data.DataSet> 中的每个表，在 Diffgram 的 **\<before\>** 部分中写出所有行的原始版本（如果有）。  
  
4.  对于有错误的行，在 Diffgram 的 **\<errors\>** 部分中写入错误内容。  
  
 将按照从 XML 文件的开头到结尾的顺序处理 Diffgram。  
  
### 处理 Diffgram  
  
1.  处理包含行当前版本的 Diffgram 的第一部分。  
  
2.  处理包含已修改行和已删除行的原始行版本的第二部分或 **\<before\>** 部分。  
  
    > [!NOTE]
    >  如果某行标记为已删除，则删除操作还可删除该行的子代，具体取决于当前 <xref:System.Data.DataSet> 的 `Cascade` 属性。  
  
3.  处理 **\<errors\>** 部分。  为本部分中各项的指定行和列设置错误信息。  
  
> [!NOTE]
>  如果将 <xref:System.Data.XmlWriteMode> 设置为 Diffgram，则目标 <xref:System.Data.DataSet> 和原始 <xref:System.Data.DataSet> 的内容可能会不同。  
  
## DiffGram 格式  
 DiffGram 格式可分为三部分：当前数据、原始（或“before”）数据和错误部分，如下面的示例中所示。  
  
```  
<?xml version="1.0"?>  
<diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"  
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1"  
         xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
  
   <DataInstance>  
   </DataInstance>  
  
  <diffgr:before>  
  </diffgr:before>  
  
  <diffgr:errors>  
  </diffgr:errors>  
</diffgr:diffgram>  
```  
  
 DiffGram 格式由以下数据块组成：  
  
 **\<**  ***DataInstance***  **\>**  
 ***DataInstance***  表示此元素的名称，用于在该文档中提供解释。  ***DataInstance*** 元素表示 <xref:System.Data.DataSet> 或 <xref:System.Data.DataTable> 的行。  不过，该元素所包含的并不是 *DataInstance*，而是 <xref:System.Data.DataSet> 或 <xref:System.Data.DataTable> 的名称。  此 DiffGram 格式块包含当前数据（无论是否经过修改）。  已修改的元素或行用 **diffgr:hasChanges** 批注来标识。  
  
 **\<diffgr:before\>**  
 此 DiffGram 格式块包含行的原始版本。  使用 **diffgr:id** 批注将该块中的元素与 ***DataInstance*** 块中的元素进行匹配。  
  
 **\<diffgr:errors\>**  
 此 DiffGram 格式块包含 ***DataInstance*** 块中特定行的错误信息。  使用 **diffgr:id** 批注将该块中的元素与 ***DataInstance*** 块中的元素进行匹配。  
  
## DiffGram 批注  
 DiffGram 使用一些批注来使来自不同 DiffGram 块的元素相关，这些块表示 <xref:System.Data.DataSet> 中的不同行版本或错误信息。  
  
 下表描述在 DiffGram 命名空间 **urn:schemas\-microsoft\-com:xml\-diffgram\-v1** 中定义的 DiffGram 批注。  
  
|批注|描述|  
|--------|--------|  
|**id**|用于将 **\<diffgr:before\>** 和 **\<diffgr:errors\>** 块中的元素与 **\<** ***DataInstance*** **\>** 块中的元素配对。  带有 **diffgr:id** 批注的值的格式为 *\[TableName\]\[RowIdentifier\]*。  例如：`<Customers diffgr:id="Customers1">`。|  
|**parentId**|标识 **\<** ***DataInstance*** **\>** 块中的哪个元素是当前元素的父元素。  带有 **diffgr:parentId** 批注的值的格式为 *\[TableName\]\[RowIdentifier\]*。  例如：`<Orders diffgr:parentId="Customers1">`。|  
|**hasChanges**|将 **\<** ***DataInstance*** **\>** 块中的行标识为已修改。  **hasChanges** 批注可以具有以下两个值之一：<br /><br /> **inserted**<br /> 标识 **Added** 行。<br /><br /> **modified**<br /> 标识包含 **\<diffgr:before\>** 块中 **Original** 行版本的 **Modified** 行。  请注意，**Deleted** 行将包含 **\<diffgr:before\>** 块中的 **Original** 行版本，但 **\<** ***DataInstance*** **\>** 块中将不存在批注元素。|  
|**hasErrors**|用 **RowError** 标识 **\<** ***DataInstance*** **\>** 块中的行。  错误元素放置在 **\<diffgr:errors\>** 块中。|  
|**错误**|包含 **\<diffgr:errors\>** 块中特定元素的 **RowError** 的文本。|  
  
 当以 DiffGram 格式读写 <xref:System.Data.DataSet> 的内容时，还包含附加的批注。  下表描述在 **urn:schemas\-microsoft\-com:xml\-msdata** 命名空间中定义的三个附加批注。  
  
|批注|描述|  
|--------|--------|  
|**RowOrder**|保留原始数据的行顺序并标识特定 <xref:System.Data.DataTable> 中行的索引。|  
|**Hidden**|将列标识为 **ColumnMapping** 属性设置为 **MappingType.Hidden**。  该属性以 **msdata:hidden** *\[ColumnName\]*\="*value*" 格式编写。  例如：`<Customers diffgr:id="Customers1" msdata:hiddenContactTitle="Owner">`。<br /><br /> 请注意，只有当隐藏列包含数据时才以 DiffGram 属性的形式来编写隐藏列。  否则将忽略隐藏列。|  
  
## DiffGram 示例  
 下面是 DiffGram 格式的示例。  该示例显示对表行的更新在提交更改之前的结果。  CustomerID 为“ALFKI”的行已被修改，但尚未更新。  因此，**\<** ***DataInstance*** **\>** 块中有一个 **diffgr:id** 为“Customers1”的 **Current** 行，**\<diffgr:before\>** 块中有一个 **diffgr:id** 为“Customers1”的 **Original** 行。  CustomerID 为“ANATR”的行包含一个 **RowError**，因此它带有 `diffgr:hasErrors="true"` 批注并且在 **\<diffgr:errors\>** 块中有一个相关的元素。  
  
```  
<diffgr:diffgram xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
  <CustomerDataSet>  
    <Customers diffgr:id="Customers1" msdata:rowOrder="0" diffgr:hasChanges="modified">  
      <CustomerID>ALFKI</CustomerID>  
      <CompanyName>New Company</CompanyName>  
    </Customers>  
    <Customers diffgr:id="Customers2" msdata:rowOrder="1" diffgram:hasErrors="true">  
      <CustomerID>ANATR</CustomerID>  
      <CompanyName>Ana Trujillo Emparedados y Helados</CompanyName>  
    </Customers>  
    <Customers diffgr:id="Customers3" msdata:rowOrder="2">  
      <CustomerID>ANTON</CustomerID>  
      <CompanyName>Antonio Moreno Taquera</CompanyName>  
    </Customers>  
    <Customers diffgr:id="Customers4" msdata:rowOrder="3">  
      <CustomerID>AROUT</CustomerID>  
      <CompanyName>Around the Horn</CompanyName>  
    </Customers>  
  </CustomerDataSet>  
  <diffgr:before>  
    <Customers diffgr:id="Customers1" msdata:rowOrder="0">  
      <CustomerID>ALFKI</CustomerID>  
      <CompanyName>Alfreds Futterkiste</CompanyName>  
    </Customers>  
  </diffgr:before>  
  <diffgr:errors>  
    <Customers diffgr:id="Customers2" diffgr:Error="An optimistic concurrency violation has occurred for this row."/>  
  </diffgr:errors>  
</diffgr:diffgram>  
```  
  
## 请参阅  
 [在 DataSet 中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)   
 [从 XML 中加载 DataSet](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)   
 [以 XML 数据形式编写数据集内容](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-contents-as-xml-data.md)   
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)