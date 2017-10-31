---
title: "XML 处理选项 | Microsoft Docs"
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
ms.assetid: 33ced8ee-1745-4e71-8dee-ebe70ec067c7
caps.latest.revision: 5
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 5
---
# XML 处理选项
请参见下面的表以获得可用于处理 XML 数据的 Microsoft 技术的列表。  
  
## .NET Framework 选项  
  
|**选项**|**处理类型**|**描述**|  
|------------|--------------|------------|  
|[LINQ to XML](../../../../ocs/visual-basic/programming-guide/concepts/linq/linq-to-xml.md) <br /> \(<xref:System.Xml.Linq> 命名空间）|内存中|-   基于 .NET Framework 语言集成查询 \(LINQ\) 技术。<br />-   提供与用于对象、关系数据和 XML 数据的 SQL 相类似的查询体验。<br />-   提供直观的文档创建和转换功能。<br />-   如果您要编写新代码，请使用此选项。|  
|<xref:System.Xml.XmlReader?displayProperty=fullName>|基于流|-   提供用于访问 XML 数据的快速、非缓存、只进方法。<br />-   您可以使用 <xref:System.Xml.XmlReader.Create%2A?displayProperty=fullName> 方法创建对象，并使用 <xref:System.Xml.XmlReaderSettings> 类指定在该对象上启用的功能集。|  
|<xref:System.Xml.XmlWriter?displayProperty=fullName>|基于流|-   提供用于生成 XML 数据的快速、非缓存、只进方法。<br />-   您可以使用 <xref:System.Xml.XmlWriter.Create%2A?displayProperty=fullName> 方法创建对象，并使用 <xref:System.Xml.XmlWriterSettings> 类指定在该对象上启用的功能集。|  
|<xref:System.Xml.XmlDocument?displayProperty=fullName>|内存中|-   实现 [W3C 文档对象模型 \(DOM\) 级别 1 核心](http://www.w3.org/TR/REC-DOM-Level-1/level-one-core.html)（可能为英文网页）和 [DOM 级别 2 核心](http://www.w3.org/TR/DOM-Level-2-Core/)（可能为英文网页）建议。<br />-   您可以使用基于熟悉的 DOM 模型的方法和属性，创建、插入、删除和修改节点。<br />-   如果您要修改利用 W3C DOM 的现有代码，请使用此选项。|  
|<xref:System.Xml.XPath.XPathNavigator?displayProperty=fullName>|内存中|-   使用游标模型提供多个编辑选项和导航功能。<br />-   XML 文档可以包含在 <xref:System.Xml.XPath.XPathDocument> 或 <xref:System.Xml.XmlDocument> 对象中。<br />-   提供用于对 XML 进行只读处理的出色性能。<br />-   如果您要通过 XPath 查询或 XSLT 转换来修改现有代码，请使用此选项。|  
|<xref:System.Xml.Xsl.XslCompiledTransform>|内存中|-   提供用于使用 XSL 转换来转换 XML 数据的选项。<br />-   通过 [XSLT 编译器 \(xsltc.exe\)](../../../../docs/standard/data/xml/xslt-compiler-xsltc-exe.md)，您可以在应用程序中引用预编译转换。|  
  
## 基于 Win32 和 COM 的选项  
  
|**选项**|**描述**|  
|------------|------------|  
|[XmlLite](http://go.microsoft.com/fwlink/?LinkId=93723)|-   一个快速、安全、非缓存、只进 XML 分析器，它可帮助您生成高性能的 XML 应用程序。<br />-   可处理能够使用动态链接库 \(DLL\) 的任何语言；建议使用 C\+\+。|  
|[MSXML](http://go.microsoft.com/fwlink/?LinkId=93722)|-   基于 COM 的技术，用于处理 Windows 操作系统附带的 XML。<br />-   提供 DOM 的本机实现，支持 XPath 和 XSLT。<br />-   包含 SAX2 基于事件的分析器。|  
  
## 请参阅  
 [使用 DOM 模型处理 XML 数据](../../../../docs/standard/data/xml/process-xml-data-using-the-dom-model.md)   
 [使用 XPath 数据模型处理 XML 数据](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [XSLT 编译器 \(xsltc.exe\)](../../../../docs/standard/data/xml/xslt-compiler-xsltc-exe.md)