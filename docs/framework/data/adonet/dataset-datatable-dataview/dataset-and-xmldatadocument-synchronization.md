---
title: "数据集与 XmlDataDocument 同步 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0ce3793d-54b2-47e4-8cf7-b0591cc4dd21
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 数据集与 XmlDataDocument 同步
ADO.NET <xref:System.Data.DataSet> 为您提供了数据的关系表示形式。  若要实现分层数据访问，可以使用 .NET Framework 中的可用 XML 类。  以前，数据的这两种表示形式是单独使用的。  不过，.NET Framework 允许分别通过 **DataSet** 对象和 <xref:System.Xml.XmlDataDocument> 对象对数据的关系和分层表示形式进行实时、同步的访问。  
  
 当 **DataSet** 与 **XmlDataDocument** 同步时，这两个对象都使用同一组数据。  这意味着如果对 **DataSet** 作出更改，更改将在 **XmlDataDocument** 中得到反映，反之亦然。  **DataSet** 和 **XmlDataDocument** 之间的这种关系为编程提供了很大的灵活性，它允许单个应用程序使用一组数据来访问围绕 **DataSet** 生成的整组服务（例如 Web 窗体控件、Windows 窗体控件以及 Visual Studio .NET 设计器等）以及 XML 服务组（例如可扩展样式表语言 \[XSL\]、XSL 转换 \[XSLT\] 和 XML 路径语言 \[XPath\]）。  您不必选择使应用程序以哪一组服务为目标，这两组服务都可用。  
  
 有若干种方法可以使 **DataSet** 与 **XmlDataDocument** 同步。  你可以：  
  
-   使用架构（即关系结构）和数据填充 **DataSet**，然后使其与新 **XmlDataDocument** 同步。  这将提供现有关系数据的分层视图。  例如：  
  
    ```vb  
    Dim dataSet As DataSet = New DataSet  
  
    ' Add code here to populate the DataSet with schema and data.  
  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)  
    ```  
  
    ```csharp  
    DataSet dataSet = new DataSet();  
  
    // Add code here to populate the DataSet with schema and data.  
  
    XmlDataDocument xmlDoc = new XmlDataDocument(dataSet);  
    ```  
  
-   仅使用架构填充 **DataSet**（如强类型化的 **DataSet**），使其与 **XmlDataDocument** 同步，然后从 XML 文档中加载 **XmlDataDocument**。  这将提供现有分层数据的关系视图。  **DataSet** 架构中的表名称和列名称必须匹配要与其同步的 XML 元素的名称。  该匹配区分大小写。  
  
     请注意，**DataSet** 的架构只需匹配需要在关系视图中公开的 XML 元素。  这样，就可以具有非常大的 XML 文档，而该文档上可以有非常小的关系“窗口”。  即使 **DataSet** 仅公开 XML 文档的一小部分，**XmlDataDocument** 仍将保留整个 XML 文档。  （有关详细示例，请参见[使数据集与 XmlDataDocument 同步](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/synchronizing-a-dataset-with-an-xmldatadocument.md)。）  
  
     以下代码示例显示创建 **DataSet** 和填充其架构，然后使其与 **XmlDataDocument** 同步的步骤。  请注意，**DataSet** 架构只需要匹配 **XmlDataDocument** 中要使用 **DataSet** 公开的元素。  
  
    ```vb  
    Dim dataSet As DataSet = New DataSet  
  
    ' Add code here to populate the DataSet with schema, but not data.  
  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)  
    xmlDoc.Load("XMLDocument.xml")  
    ```  
  
    ```csharp  
    DataSet dataSet = new DataSet();  
  
    // Add code here to populate the DataSet with schema, but not data.  
  
    XmlDataDocument xmlDoc = new XmlDataDocument(dataSet);  
    xmlDoc.Load("XMLDocument.xml");  
    ```  
  
     如果 **XmlDataDocument** 已经与包含数据的 **DataSet** 同步，则不能加载该 **XmlDataDocument**。  否则会引发异常。  
  
-   创建一个新的 **XmlDataDocument** 并从 XML 文档中加载，然后使用 **XmlDataDocument** 的 **DataSet** 属性访问数据的关系视图。  若要使用 **DataSet** 查看 **XmlDataDocument** 中的数据，需要先设置 **DataSet** 的架构。  同样，**DataSet** 架构中的表名称和列名称必须匹配要与其同步的 XML 元素的名称。  该匹配区分大小写。  
  
     以下代码示例显示如何访问 **XmlDataDocument** 中数据的关系视图。  
  
    ```vb  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument  
    Dim dataSet As DataSet = xmlDoc.DataSet  
  
    ' Add code here to create the schema of the DataSet to view the data.  
  
    xmlDoc.Load("XMLDocument.xml")  
  
    ```  
  
    ```csharp  
    XmlDataDocument xmlDoc = new XmlDataDocument();  
    DataSet dataSet = xmlDoc.DataSet;  
  
    // Add code here to create the schema of the DataSet to view the data.  
  
    xmlDoc.Load("XMLDocument.xml");  
    ```  
  
 使 **XmlDataDocument** 与 **DataSet** 同步的另一个优点是避免了 XML 文档的失真。  如果 **DataSet** 是使用 **ReadXml** 从 XML 文档中填充的，那么当使用 **WriteXml** 以 XML 文档形式写回数据时，数据可能大大不同于初始的 XML 文档。  这是因为 **DataSet** 不维护 XML 文档中的格式设置（如空白）或分层信息（如元素顺序）。  **DataSet** 也不包含 XML 文档中因为不匹配 **Dataset** 架构而被忽略的元素。  通过使 **XmlDataDocument** 与 **DataSet** 同步，可以在 **XmlDataDocument** 中维护初始 XML 文档的格式设置和分层元素结构，而 **DataSet** 仅包含适用于 **DataSet** 的数据和架构信息。  
  
 当使 **DataSet** 与 **XmlDataDocument** 同步时，根据 <xref:System.Data.DataRelation> 对象是否嵌套，所得的结果可能会有所不同。  有关详细信息，请参阅[嵌套 DataRelation](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)。  
  
## 本节内容  
 [使数据集与 XmlDataDocument 同步](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/synchronizing-a-dataset-with-an-xmldatadocument.md)  
 显示如何使强类型化的 **DataSet** 使用最小的架构与 **XmlDataDocument** 同步的示例。  
  
 [对 DataSet 执行 XPath 查询](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/performing-an-xpath-query-on-a-dataset.md)  
 显示对 **DataSet** 的内容执行 XPath 查询的示例。  
  
 [将 XSLT 转换应用于数据集](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/applying-an-xslt-transform-to-a-dataset.md)  
 显示对 **DataSet** 的内容应用 XSLT 转换的示例。  
  
## 相关章节  
 [在 DataSet 中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)  
 描述 **DataSet** 如何作为数据源与 XML 进行交互（包括以 XML 数据的形式加载和保持 **DataSet** 的内容）。  
  
 [嵌套 DataRelation](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations.md)  
 讨论嵌套 **DataRelation** 对象在以 XML 数据形式表示 **DataSet** 内容时的重要性，并描述如何创建这些关系。  
  
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)  
 描述 **DataSet** 并说明如何使用它来管理应用程序数据和与包括关系数据库和 XML 在内的数据源进行交互。  
  
 [XmlDataDocument 类](frlrfSystemXmlXmlDataDocumentClassTopic)  
 包含有关 **XmlDataDocument** 类的参考信息。  
  
## 请参阅  
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)