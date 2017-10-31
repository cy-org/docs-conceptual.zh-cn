---
title: "XslTransform 类的 XSLT 转换 | Microsoft Docs"
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
ms.assetid: 500335af-f9b5-413b-968a-e6d9a824478c
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# XslTransform 类的 XSLT 转换
> [!NOTE]
>  <xref:System.Xml.Xsl.XslTransform> 类在 [!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)] 中已过期。  可以使用 <xref:System.Xml.Xsl.XslCompiledTransform> 类执行可扩展样式表语言转换 \(XSLT\) 转换。  请参阅[使用 XslCompiledTransform 类](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md)和[从 XslTransform 类迁移](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)了解详细信息。  
  
 XSLT 的目标是将源 XML 文档的内容转换为格式或结构不同的另一个文档（例如，将 XML 转换为在网站上使用的 HTML，或将其转换为只包含应用程序所需字段的文档）。  此转换过程由万维网联合会 \(W3C\) XSLT 1.0 版建议（位于 www.w3.org\/TR\/xslt）指定。  在 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 中，<xref:System.Xml.Xsl.XslTransform> 命名空间中的 <xref:System.Xml.Xsl> 类是实现此规范功能的 XSLT 处理器。  有几个 W3C XSLT 1.0 建议未实现的功能，[XslTransform 的输出](../../../../docs/standard/data/xml/outputs-from-an-xsltransform.md)中列出了这些功能。  下图显示 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 的转换结构。  
  
## 概述  
 ![XSLT 转换体系结构](../../../../docs/standard/data/xml/media/xslttransformationswithxsltransformclass.gif "xsltTransformationsWithXslTransformClass")  
转换结构  
  
 XSLT 建议使用 XML 路径语言 \(XPath\) 选择 XML 文档的各部分，其中 XPath 是用于浏览文档树节点的查询语言。  如图所示，[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 实现的 XPath 用来选择存储在几个类中的 XML 部分，如 <xref:System.Xml.XmlDocument>、<xref:System.Xml.XmlDataDocument> 和 <xref:System.Xml.XPath.XPathDocument> 类。  <xref:System.Xml.XPath.XPathDocument> 是一个优化的 XSLT 数据存储区，当与 <xref:System.Xml.Xsl.XslTransform> 一起使用时，可以提供性能良好的 XSLT 转换。  
  
 下表列出了在使用 <xref:System.Xml.Xsl.XslTransform> 和 XPath 时常用的类及其功能。  
  
|类或接口|函数|  
|----------|--------|  
|<xref:System.Xml.XPath.XPathNavigator>|它是提供用于在存储区上浏览的游标样式模型以及 XPath 查询支持的 API。  它不提供对基础存储区的编辑。  要进行编辑，请使用 <xref:System.Xml.XmlDocument> 类。|  
|<xref:System.Xml.XPath.IXPathNavigable>|它是为存储区提供 `CreateNavigator` 的 <xref:System.Xml.XPath.XPathNavigator> 方法的接口。|  
|<xref:System.Xml.XmlDocument>|它启用对此文档的编辑。  它实现 <xref:System.Xml.XPath.IXPathNavigable>，从而允许随后需要 XSLT 转换的文档编辑方案。  有关更多信息，请参见 [XslTransform 的 XmlDocument 输入](../../../../docs/standard/data/xml/xmldocument-input-to-xsltransform.md)。|  
|<xref:System.Xml.XmlDataDocument>|它从 <xref:System.Xml.XmlDocument> 派生。  它根据 <xref:System.Data.DataSet> 的指定映射，使用 <xref:System.Data.DataSet> 优化 XML 文档中的结构化数据存储，从而将关系世界与 XML 世界联系起来。  它实现 <xref:System.Xml.XPath.IXPathNavigable>，从而允许可以对从数据库中检索到的关系数据执行 XSLT 转换的方案。  有关更多信息，请参见[关系数据和 ADO.NET 的 XML 集成](../../../../docs/standard/data/xml/xml-integration-with-relational-data-and-adonet.md)。|  
|<xref:System.Xml.XPath.XPathDocument>|此类针对 <xref:System.Xml.Xsl.XslTransform> 处理和 XPath 查询进行了优化，并提供只读的高性能缓存。  它实现 <xref:System.Xml.XPath.IXPathNavigable>，是用于 XSLT 转换的首选存储区。|  
|<xref:System.Xml.XPath.XPathNodeIterator>|它提供在 XPath 节点集上的浏览。  <xref:System.Xml.XPath.XPathNavigator> 的所有 XPath 选择方法都返回 <xref:System.Xml.XPath.XPathNodeIterator>。  可以在同一存储区上创建多个 <xref:System.Xml.XPath.XPathNodeIterator> 对象，每个对象表示一个选定的节点集。|  
  
## MSXML XSLT 扩展  
 `msxsl:script` 和 `msxsl:node-set` 函数是 <xref:System.Xml.Xsl.XslTransform> 类唯一支持的 Microsoft XML 核心服务 \(MSXML\) XSLT 扩展。  
  
## 示例  
 下面的代码示例加载一个 XSL 样式表，将一个称为 mydata.xml 的文件读入 <xref:System.Xml.XPath.XPathDocument> 中，并对一个称为 myStyleSheet.xsl 的虚构文件上的数据执行转换，将格式化的输出发送到控制台。  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.XPath  
Imports System.Xml.Xsl  
  
Public Class Sample  
    Private filename As [String] = "mydata.xml"  
    Private stylesheet As [String] = "myStyleSheet.xsl"  
  
    Public Shared Sub Main()  
        Dim xslt As New XslTransform()  
        xslt.Load(stylesheet)  
        Dim xpathdocument As New XPathDocument(filename)  
        Dim writer As New XmlTextWriter(Console.Out)  
        writer.Formatting = Formatting.Indented  
  
        xslt.Transform(xpathdocument, Nothing, writer, Nothing)  
    End Sub 'Main  
End Class 'Sample  
  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.XPath;  
using System.Xml.Xsl;  
  
public class Sample   
{  
    private const String filename = "mydata.xml";  
    private const String stylesheet = "myStyleSheet.xsl";  
  
    public static void Main()   
    {  
    XslTransform xslt = new XslTransform();  
    xslt.Load(stylesheet);  
    XPathDocument xpathdocument = new  
    XPathDocument(filename);  
    XmlTextWriter writer = new XmlTextWriter(Console.Out);  
    writer.Formatting=Formatting.Indented;  
  
    xslt.Transform(xpathdocument, null, writer, null);      
    }  
}  
```  
  
## 请参阅  
 <xref:System.Xml.Xsl.XslTransform>   
 [XslTransform 类实现 XSLT 处理器](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)   
 [XslTransform 类中任意行为的实现](../../../../docs/standard/data/xml/implementation-of-discretionary-behaviors-in-the-xsltransform-class.md)   
 [转换中的 XPathNavigator](../../../../docs/standard/data/xml/xpathnavigator-in-transformations.md)   
 [转换中的 XPathNodeIterator](../../../../docs/standard/data/xml/xpathnodeiterator-in-transformations.md)   
 [XslTransform 的 XPathDocument 输入](../../../../docs/standard/data/xml/xpathdocument-input-to-xsltransform.md)   
 [XslTransform 的 XmlDataDocument 输入](../../../../docs/standard/data/xml/xmldatadocument-input-to-xsltransform.md)   
 [XslTransform 的 XmlDocument 输入](../../../../docs/standard/data/xml/xmldocument-input-to-xsltransform.md)