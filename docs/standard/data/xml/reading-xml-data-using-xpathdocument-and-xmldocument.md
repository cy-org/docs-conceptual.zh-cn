---
title: "使用 XPathDocument 和 XmlDocument 读取 XML 数据 | Microsoft Docs"
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
ms.assetid: 5711b225-6aa2-4e4f-9898-19f2d518ad1a
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# 使用 XPathDocument 和 XmlDocument 读取 XML 数据
可以通过两种方式读取 <xref:System.Xml.XPath?displayProperty=fullName> 命名空间中的 XML 文档。  一种方式是使用只读 <xref:System.Xml.XPath.XPathDocument> 类读取 XML 文档，另一种方式是使用 <xref:System.Xml?displayProperty=fullName> 命名空间中可编辑的 <xref:System.Xml.XmlDocument> 类读取 XML 文档。  
  
## 使用 XPathDocument 类读取 XML 文档  
 <xref:System.Xml.XPath.XPathDocument> 类使用 XPath 数据模型提供 XML 文档在内存中的快速只读表示形式。  <xref:System.Xml.XPath.XPathDocument> 类的实例使用其六个构造函数之一创建。  通过这些构造函数，可以使用 <xref:System.IO.Stream>、<xref:System.IO.TextReader> 或 <xref:System.Xml.XmlReader> 对象以及 XML 文件的 `string` 路径来读取 XML 文档。  
  
 以下示例说明如何使用 <xref:System.Xml.XPath.XPathDocument> 类的 `string` 构造函数来读取 XML 文档。  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
```  
  
## 使用 XmlDocument 类读取 XML 文档  
 <xref:System.Xml.XmlDocument> 类是实现 W3C 文档对象模型 \(DOM\) 级别 1 核心和核心 DOM 级别 2 的 XML 文档在内存中的可编辑表示形式。  <xref:System.Xml.XmlDocument> 类的实例使用其三个构造函数之一创建。  可以通过调用没有参数的 <xref:System.Xml.XmlDocument> 类构造函数，创建新的空 <xref:System.Xml.XmlDocument> 对象。  在调用了构造函数之后，使用 <xref:System.Xml.XmlDocument.Load%2A> 方法以及 XML 文件的 `string` 路径将 XML 数据从 <xref:System.IO.Stream>、<xref:System.IO.TextReader> 或 <xref:System.Xml.XmlReader> 对象加载到新的 <xref:System.Xml.XmlDocument> 对象中。  
  
 以下示例说明如何使用没有参数的 <xref:System.Xml.XmlDocument> 类构造函数以及 <xref:System.Xml.XmlDocument.Load%2A> 方法来读取 XML 文档。  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("books.xml")  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("books.xml");  
```  
  
## 确定 XML 文档的编码  
 <xref:System.Xml.XmlReader> 对象可以用于读取 XML 文档并创建 <xref:System.Xml.XPath.XPathDocument> 和 <xref:System.Xml.XmlDocument> 对象，如前面各节所示。  但是，<xref:System.Xml.XmlReader> 对象可能会读取未编码的数据，因此，不会提供任何编码信息。  
  
 <xref:System.Xml.XmlTextReader> 类从 <xref:System.Xml.XmlReader> 类继承，使用其 <xref:System.Xml.XmlTextReader.Encoding%2A> 属性提供编码信息，并且可以用于创建 <xref:System.Xml.XPath.XPathDocument> 对象或 <xref:System.Xml.XmlDocument> 对象。  
  
 有关 <xref:System.Xml.XmlTextReader> 类提供的编码信息的更多信息，请参见 <xref:System.Xml.XmlTextReader> 类参考文档中的 <xref:System.Xml.XmlTextReader.Encoding%2A> 属性。  
  
## 创建 XPathNavigator 对象  
 在将 XML 文档读入 <xref:System.Xml.XPath.XPathDocument> 或 <xref:System.Xml.XmlDocument> 对象之后，可以创建一个 <xref:System.Xml.XPath.XPathNavigator> 对象，以选择、计算、浏览和（在有些情况下）编辑基础 XML 数据。  
  
 除了 <xref:System.Xml.XmlNode> 类之外，<xref:System.Xml.XPath.XPathDocument> 和 <xref:System.Xml.XmlDocument> 类也实现了 <xref:System.Xml.XPath?displayProperty=fullName> 命名空间的 <xref:System.Xml.XPath.IXPathNavigable> 接口。  因此，所有三个类均提供返回 <xref:System.Xml.XPath.XPathNavigator> 对象的 <xref:System.Xml.XPath.IXPathNavigable.CreateNavigator%2A> 方法。  
  
### 使用 XPathNavigator 类编辑 XML 文档  
 除了选择、计算和浏览 XML 数据之外，在有些情况下，<xref:System.Xml.XPath.XPathNavigator> 类还可以用于编辑 XML 文档，这取决于创建文档的对象。  
  
 <xref:System.Xml.XPath.XPathDocument> 类为只读类，而 <xref:System.Xml.XmlDocument> 类是可编辑的类，因此，从 <xref:System.Xml.XPath.XPathDocument> 对象创建的 <xref:System.Xml.XPath.XPathNavigator> 对象不能用于编辑 XML 文档，而从 <xref:System.Xml.XmlDocument> 对象创建的对象可以编辑。  <xref:System.Xml.XPath.XPathDocument> 类只能用于读取 XML 文档。  如果需要编辑 XML 文档，或要求访问 <xref:System.Xml.XmlDocument> 类提供的其他功能（例如事件处理），应使用 <xref:System.Xml.XmlDocument> 类。  
  
 <xref:System.Xml.XPath.XPathNavigator> 类的 <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> 属性指定 <xref:System.Xml.XPath.XPathNavigator> 对象是否可以编辑 XML 数据。  
  
 下表说明了每个类的 <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> 属性的值。  
  
|<xref:System.Xml.XPath.IXPathNavigable> 实现|<xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> 值|  
|--------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Xml.XPath.XPathDocument>|`false`|  
|<xref:System.Xml.XmlDocument>|`true`|  
  
## 请参阅  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [使用 XPath 数据模型处理 XML 数据](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [使用 XPathNavigator 访问 XML 数据](../../../../docs/standard/data/xml/accessing-xml-data-using-xpathnavigator.md)   
 [使用 XPathNavigator 编辑 XML 数据](../../../../docs/standard/data/xml/editing-xml-data-using-xpathnavigator.md)   
 [使用 XPathNavigator 验证架构](../../../../docs/standard/data/xml/schema-validation-using-xpathnavigator.md)