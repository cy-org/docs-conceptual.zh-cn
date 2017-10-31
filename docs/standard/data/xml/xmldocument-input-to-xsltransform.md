---
title: "XslTransform 的 XmlDocument 输入 | Microsoft Docs"
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
ms.assetid: 97115892-410a-4657-ab47-1e14dfba73f8
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# XslTransform 的 XmlDocument 输入
<xref:System.Xml.XmlDocument> 类提供对 XML 文档的编辑功能。 如果 XML 在发送到 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法之前需要编辑或修改，请将 XML 加载到 <xref:System.Xml.XmlDocument> 中进行编辑，然后发送到 <xref:System.Xml.Xsl.XslTransform>。  
  
> [!NOTE]
>  <xref:System.Xml.Xsl.XslTransform> 类在 [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)] 中已过期。 可以使用 <xref:System.Xml.Xsl.XslCompiledTransform> 类执行可扩展样式表语言转换 \(XSLT\) 转换。 有关更多信息，请参见[使用 XslCompiledTransform 类](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md)和[从 XslTransform 类迁移](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)。  
  
 <xref:System.Xml.XmlDocument> 实现了 <xref:System.Xml.XPath.IXPathNavigable> 接口，所以，文档在编辑后可以传递给 <xref:System.Xml.Xsl.XslTransform.Transform%2A> 方法。  
  
 因为 <xref:System.Xml.XmlDocument> 的编辑功能，对于可扩展样式表语言转换 \(XSLT\) 转换，使用 <xref:System.Xml.XmlDocument> 类作为转换的输入比使用 <xref:System.Xml.XPath.XPathDocument> 速度要慢，因为 <xref:System.Xml.XPath.XPathDocument> 是内部存储，已针对 XML 路径语言 \(XPath\) 查询进行优化。  
  
## 示例  
 下面的代码示例显示如何将 <xref:System.Xml.XmlDocument> 提供给 <xref:System.Xml.Xsl.XslTransform>，同时将输出发送到 <xref:System.Xml.XmlReader>。  
  
```vb  
Dim doc as XmlDocument = new XmlDocument()  
doc.Load("books.xml")  
Dim trans As XslTransform = new XslTransform()  
trans.Load("book.xsl")  
Dim rdr As XmlReader = trans.Transform(doc, Nothing, Nothing)  
while (rdr.Read())  
end while  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
doc.Load("books.xml");  
XslTransform trans = new XslTransform();  
trans.Load("book.xsl");  
XmlReader rdr = trans.Transform(doc, null, null);  
while (rdr.Read()) {}  
```  
  
## 请参阅  
 <xref:System.Xml.XmlDocument>   
 [XslTransform 类的 XSLT 转换](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)   
 [XslTransform 类实现 XSLT 处理器](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)   
 [转换中的 XPathNavigator](../../../../docs/standard/data/xml/xpathnavigator-in-transformations.md)   
 [转换中的 XPathNodeIterator](../../../../docs/standard/data/xml/xpathnodeiterator-in-transformations.md)   
 [XslTransform 的 XPathDocument 输入](../../../../docs/standard/data/xml/xpathdocument-input-to-xsltransform.md)   
 [XslTransform 的 XmlDataDocument 输入](../../../../docs/standard/data/xml/xmldatadocument-input-to-xsltransform.md)