---
title: "XslTransform 的 XmlDataDocument 输入 | Microsoft Docs"
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
ms.assetid: a0b536b6-cdb3-4a44-86c2-3b2ebc7bd4c9
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# XslTransform 的 XmlDataDocument 输入
> [!NOTE]
>  <xref:System.Xml.Xsl.XslTransform> 类在 [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)] 中已过期。 可以使用 <xref:System.Xml.Xsl.XslCompiledTransform> 类执行可扩展样式表语言转换 \(XSLT\) 转换。 有关更多信息，请参见[使用 XslCompiledTransform 类](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md)和[从 XslTransform 类迁移](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)。  
  
 Microsoft [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 实现 XML 文档对象模型 \(DOM\) 以提供对 XML 文档的数据访问，并且提供了用于在 XML 文档中读、写和浏览的附加类。<xref:System.Xml.XmlDataDocument> 命名空间中的 <xref:System.Xml> 通过与 <xref:System.Data.DataSet> 中的关系数据同步的能力，提供对数据的关系访问。 可通过 <xref:System.Data.DataSet> 的关系表示形式同时查看和处理结构化 XML，也可通过 <xref:System.Xml.XmlDataDocument> 的 DOM 表示形式处理半结构化 XML。 因此，<xref:System.Xml.XmlDataDocument> 将 XML 世界和关系世界联系起来。  
  
 如果数据存储在关系结构中并希望它作为 XSLT 转换的输入，则可以将关系数据加载到 <xref:System.Data.DataSet> 中并将其与 <xref:System.Xml.XmlDataDocument> 关联。<xref:System.Xml.XPath.XPathNavigator> 作为 <xref:System.Xml.Xsl.XslTransform> 的输入，在 <xref:System.Xml.XmlDataDocument> 上通过 <xref:System.Xml.XPath.IXPathNavigable> 接口实现。 通过获取关系数据，将其加载到 <xref:System.Data.DataSet> 中并使用 <xref:System.Xml.XmlDataDocument> 中的同步，现在可以对关系数据执行 XSLT 转换。  
  
 有关将转换应用于关系数据的更多信息，请参见[将 XSLT 转换应用于数据集](../../../../docs/framework/data/adonet/dataset-datatable-dataview/applying-an-xslt-transform-to-a-dataset.md)。  
  
## 请参阅  
 <xref:System.Xml.XmlDataDocument>   
 [数据集与 XmlDataDocument 同步](../../../../docs/framework/data/adonet/dataset-datatable-dataview/dataset-and-xmldatadocument-synchronization.md)   
 [XslTransform 类的 XSLT 转换](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)   
 [XslTransform 类实现 XSLT 处理器](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)   
 [转换中的 XPathNavigator](../../../../docs/standard/data/xml/xpathnavigator-in-transformations.md)   
 [转换中的 XPathNodeIterator](../../../../docs/standard/data/xml/xpathnodeiterator-in-transformations.md)   
 [XslTransform 的 XPathDocument 输入](../../../../docs/standard/data/xml/xpathdocument-input-to-xsltransform.md)   
 [XslTransform 的 XmlDocument 输入](../../../../docs/standard/data/xml/xmldocument-input-to-xsltransform.md)