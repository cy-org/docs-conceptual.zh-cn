---
title: "XML 文档和数据"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: e695047f-3c0f-4045-8708-5baea91cc380
caps.latest.revision: 9
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 88d993122bf1498b08d2e523a71f7f1bed505c9a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/05/2017

---
# <a name="xml-documents-and-data"></a>XML 文档和数据
.NET Framework 提供了一组全面而集成的类，可用来方便地生成可以识别 XML 的应用程序。 通过以下命名空间中的类，可以分析和编写 XML，编辑内存中的 XML 数据，进行数据验证以及 XSLT 转换。  
  
-   <xref:System.Xml>  
  
-   <xref:System.Xml.XPath>  
  
-   <xref:System.Xml.Xsl>  
  
-   <xref:System.Xml.Schema>  
  
-   <xref:System.Xml.Linq>  
  
 有关完整列表，请参阅 [System.Xml 命名空间](http://msdn.microsoft.com/library/gg145036.aspx)网页。  
  
 这些命名空间中的类支持万维网联合会 (W3C) 建议。 例如:   
  
-   <xref:System.Xml.XmlDocument?displayProperty=fullName> 类可实现 [W3C 文档对象模型 (DOM) 级别 1 核心](http://www.w3.org/TR/REC-DOM-Level-1/)和 [DOM 级别 2 核心](http://www.w3.org/TR/DOM-Level-2-Core/)建议。  
  
-   <xref:System.Xml.XmlReader?displayProperty=fullName> 和 <xref:System.Xml.XmlWriter?displayProperty=fullName> 类支持 [W3C XML 1.0](http://www.w3.org/TR/2006/REC-xml-20060816/) 和 [XML 中的命名空间](http://www.w3.org/TR/REC-xml-names/)建议。  
  
-   <xref:System.Xml.Schema.XmlSchemaSet?displayProperty=fullName> 类中的架构支持 [W3C XML 架构第 1 部分：结构](http://www.w3.org/TR/xmlschema-1/)和 [XML 架构第 2 部分：数据类型](http://www.w3.org/TR/xmlschema-2/)建议。  
  
-   <xref:System.Xml.Xsl?displayProperty=fullName> 命名空间中的类支持符合 [W3C XSLT 1.0](http://www.w3.org/TR/xslt) 建议的 XSLT 转换。  
  
 .NET Framework 中的 XML 类具有以下优点：  
  
-   **高效率。** 通过 [LINQ to XML](http://msdn.microsoft.com/library/f0fe21e9-ee43-4a55-b91a-0800e5782c13)，可更方便地用 XML 编程，并可得到与 SQL 类似的查询体验。  
  
-   **扩展性。** .NET Framework 中的 XML 类可使用抽象基类和虚拟方法进行扩展。 例如，您可以创建 <xref:System.Xml.XmlUrlResolver> 类的一个派生类，用以将缓存流存储到本地磁盘。  
  
-   **可插入的体系结构。** .NET Framework 提供了一种体系结构，其中的组件可以相互利用，数据可以在各组件之间传送。 例如，可以使用 <xref:System.Xml.XPath.XPathDocument> 类来转换数据存储（例如，<xref:System.Xml.XmlDocument> 或 <xref:System.Xml.Xsl.XslCompiledTransform> 对象），然后可将输出传送到另一个存储或作为 Web 服务的流返回。  
  
-   **性能。** 为获得更佳应用程序性能，.NET Framework 中设计的某些 XML 类支持基于流的模型并具有以下特性：  
  
    -   只进、拉出模型分析使用最小缓存 (<xref:System.Xml.XmlReader>)。  
  
    -   只进验证 (<xref:System.Xml.XmlReader>)。  
  
    -   游标式导航，可使创建的节点减少到单个虚拟节点，同时提供对文档的随机访问 (<xref:System.Xml.XPath.XPathNavigator>)。  
  
     为了在需要进行 XSLT 处理时都获得更佳性能，您可以使用 <xref:System.Xml.XPath.XPathDocument> 类，这是一个用于 XPath 查询的经过优化的只读存储，旨在高效地与 <xref:System.Xml.Xsl.XslCompiledTransform> 类结合使用。  
  
-   **与 ADO.NET 集成。** XML 类和 [ADO.NET](../../../../docs/framework/data/adonet/index.md) 紧密集成，将关系数据和 XML 组合在一起。 <xref:System.Data.DataSet> 类是从数据库中检索到的数据在内存中的缓存。 <xref:System.Data.DataSet> 类能够使用 <xref:System.Xml.XmlReader> 和 <xref:System.Xml.XmlWriter> 类读取和写入 XML，以 XML 架构 (XSD) 形式保持其内部关系架构结构，并可以推断 XML 文档的架构结构。  
  
## <a name="in-this-section"></a>本节内容  
 [XML 处理选项](../../../../docs/standard/data/xml/xml-processing-options.md)  
 讨论用于处理 XML 数据的选项。  
  
 [内存中 XML 数据处理](../../../../docs/standard/data/xml/processing-xml-data-in-memory.md)  
 讨论用于处理内存中 XML 数据的三种模型。 [LINQ to XML](http://msdn.microsoft.com/library/f0fe21e9-ee43-4a55-b91a-0800e5782c13)、<xref:System.Xml.XmlDocument> 类（基于 W3C 文档对象模型）和 <xref:System.Xml.XPath.XPathDocument> 类（基于 XPath 数据模型）。  
  
 [XSLT 转换](../../../../docs/standard/data/xml/xslt-transformations.md)  
 描述如何使用 XSLT 处理器。  
  
 [XML 架构对象模型 (SOM)](../../../../docs/standard/data/xml/xml-schema-object-model-som.md)  
 描述用于通过提供 <xref:System.Xml.Schema.XmlSchema> 类加载和编辑架构来生成和处理 XML 架构 (XSD) 的类。  
  
 [关系数据和 ADO.NET 的 XML 集成](../../../../docs/standard/data/xml/xml-integration-with-relational-data-and-adonet.md)  
 描述 .NET Framework 如何通过 <xref:System.Data.DataSet> 对象和 <xref:System.Xml.XmlDataDocument> 对象启用对数据的关系和分层表示形式的实时同步访问。  
  
 [管理 XML 文档中的命名空间](../../../../docs/standard/data/xml/managing-namespaces-in-an-xml-document.md)  
 描述 <xref:System.Xml.XmlNamespaceManager> 类如何用于存储和维护命名空间信息。  
  
 [System.Xml 类中的类型支持](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)  
 描述如何将 XML 数据类型映射到 CLR 类型，如何转换 XML 类型，并描述 <xref:System.Xml> 类中的其它类型支持功能。  
  
## <a name="related-sections"></a>相关章节  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)  
 提供如何使用 ADO.NET 访问数据的信息。  
  
 [安全性](../../../../docs/standard/security/index.md)  
 提供对 .NET Framework 安全系统的概述。  
  
 [XML 开发人员中心](http://go.microsoft.com/fwlink/?linkid=42458)  
 为 XML 开发人员提供其他技术信息、下载、新闻组和其他资源。

