---
title: "关系数据和 ADO.NET 的 XML 集成 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: f6ebb1a1-f2ca-49b9-92c9-0150940cf6e6
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# 关系数据和 ADO.NET 的 XML 集成
**XmlDataDocument** 类是 **XmlDocument** 的派生类，包含 XML 数据。  **XmlDataDocument** 的优势是在关系数据和分层数据之间架起了桥梁。  它是一个可绑定到 **DataSet** 的 **XmlDocument**，这两个类可以同步对其中所包含的数据的更改。  绑定到 **DataSet** 的 **XmlDocument** 允许 XML 与关系数据集成，您不必将数据表示为 XML 格式或关系格式。  您可以用这两种格式表示数据，而不是限于一种数据表示形式。  
  
 让数据可以以两种视图呈现的好处是：  
  
-   XML 文档的结构化部分可以映射到一个数据集，并可以有效地存储、索引和搜索。  
  
-   转换、验证和导航可以通过以关系形式存储的 XML 数据上的游标模型有效地进行。  有时，对关系结构进行操作比在 XML 存储在一个 **XmlDocument** 模型中时更为有效。  
  
-   **DataSet** 可以存储 XML 的一部分。  也就是说，您可以用 **XPath** 或 **XslTransform** 只将有关的元素和属性存储到 **DataSet**。  在这里，可以对较小的、经过筛选的数据子集进行更改，而这些更改可以传播到 **XmlDataDocument** 中更大的数据中。  
  
 您也可以对从 SQL Server 加载到 **DataSet** 中的数据进行转换。  另一种选择是将 .NET Framework 类样式管理的 WinForm 和 WebForm 控件绑定到从 XML 输入流填充的 **DataSet**。  
  
 除支持 **XslTransform** 外，**XmlDataDocument** 还将关系数据向 **XPath** 查询和验证公开。  一般地，所有 XML 服务都可以对关系数据使用，而关系功能（如控件绑定、代码生成等）可以对 XML 的结构化映射使用，不会使 XML 失真。  
  
 因为 **XmlDataDocument** 从 **XmlDocument** 继承，所以提供了 W3C DOM 的实现。  **XmlDataDocument** 与 **DataSet** 关联并将一个数据子集存储到其中的这一事实，并未限制或改变其用作 **XmlDocument** 的这一性质。  编写用来使用 **XmlDocument** 的代码不加更改即可对 **XmlDataDocument** 使用。  **DataSet** 通过定义表、列、关系和约束提供了相同数据的关系视图，它是一个独立的、内存中的用户数据存储区。  
  
 下面的插图显示了 XML 数据与 **DataSet** 和 **XmlDataDocument** 的不同关联。  
  
 ![XML 数据集](../../../../docs/standard/data/xml/media/xmlintegrationwithrelationaldataandadodotnet.gif "xmlIntegrationWithRelationalDataAndADOdotNet")  
  
 插图显示了 XML 数据可以直接加载到 **DataSet** 中，从而可以以关系型的方式对 XML 进行直接处理。  或者，XML 可以加载到 DOM 的派生类 **XmlDataDocument** 中，然后就可以加载 **DataSet** 并进行同步。  因为 **DataSet** 和 **XmlDataDocument** 是通过单个数据集同步的，所以对一个存储区中的数据所做的更改会反映到另一个存储区中。  
  
 **XmlDataDocument** 继承了 **XmlDocument** 的所有编辑和浏览功能。  有时使用 **XmlDataDocument** 及其继承的功能时，与 **DataSet** 同步比将 XML 直接加载到 **DataSet** 中更为合适。  下表显示了在选择加载 **DataSet** 要使用的方法时考虑的事项。  
  
|何时将 XML 直接加载到数据集中|何时将 XmlDataDocument 与 DataSet 同步|  
|-----------------------|--------------------------------------|  
|用 SQL 在 **DataSet** 中查询数据比用 XPath 容易。|需要对 **DataSet** 中的数据执行 XPath 查询。|  
|保留源 XML 中的元素顺序并不重要。|保留源 XML 中的元素顺序很重要。|  
|源 XML 中元素间的空白和格式设置不需要保留。|保留源 XML 中的空白和格式设置很重要。|  
  
 如果直接将 XML 加载并写入 **DataSet** 以及直接从中加载和写出 XML 可满足您的需要，请参见[从 XML 中加载 DataSet](../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md) 和[以 XML 数据形式编写 DataSet](../../../../docs/framework/data/adonet/dataset-datatable-dataview/writing-dataset-contents-as-xml-data.md)。  
  
 如果从 **XmlDataDocument** 加载 **DataSet** 可满足您的需要，请参见[将 Dataset 与 XML 文档同步](../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataset-and-xmldatadocument-synchronization.md)。  
  
## 请参阅  
 [在 DataSet 中使用 XML](../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)