---
title: "使用 XPathNavigator 提取 XML 数据 | Microsoft Docs"
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
ms.assetid: 095b0987-ee4b-4595-a160-da1c956ad576
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# 使用 XPathNavigator 提取 XML 数据
可以通过多种不同的方式在 Microsoft .NET Framework 中表示 XML 文档。  包括使用 <xref:System.String>，或通过使用 <xref:System.Xml.XmlReader>、<xref:System.Xml.XmlWriter>、<xref:System.Xml.XmlDocument> 或 <xref:System.Xml.XPath.XPathDocument> 类。  为了便于在这些不同的 XML 文档表示形式之间切换，<xref:System.Xml.XPath.XPathNavigator> 类提供了许多方法和属性，用于将 XML 作为 <xref:System.String>, <xref:System.Xml.XmlReader> 对象或 <xref:System.Xml.XmlWriter> 对象提取。  
  
## 将 XPathNavigator 转换为字符串  
 <xref:System.Xml.XPath.XPathNavigator> 类的 <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> 属性用于获取整个 XML 文档的标记或只获取单个节点及其子节点的标记。  
  
> [!NOTE]
>  <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> 属性只获取节点的子节点的标记。  
  
 以下代码示例显示如何将 <xref:System.Xml.XPath.XPathNavigator> 对象中包含的整个 XML 文档以及单个节点及其子节点保存为 <xref:System.String>。  
  
```vb  
Dim document As XPathDocument = New XPathDocument("input.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Save the entire input.xml document to a string.  
Dim xml As String = navigator.OuterXml  
  
' Now save the Root element and its child nodes to a string.  
navigator.MoveToChild(XPathNodeType.Element)  
Dim root As String = navigator.OuterXml  
```  
  
```csharp  
XPathDocument document = new XPathDocument("input.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Save the entire input.xml document to a string.  
string xml = navigator.OuterXml;  
  
// Now save the Root element and its child nodes to a string.  
navigator.MoveToChild(XPathNodeType.Element);  
string root = navigator.OuterXml;  
```  
  
## 将 XPathNavigator 转换为 XmlReader  
 <xref:System.Xml.XPath.XPathNavigator.ReadSubtree%2A> 方法用于将 XML 文档的全部内容或只是单个节点及其子节点流处理到 <xref:System.Xml.XmlReader> 对象。  
  
 为当前节点及其子节点创建 <xref:System.Xml.XmlReader> 对象时，<xref:System.Xml.XmlReader> 对象的 <xref:System.Xml.XmlReader.ReadState%2A> 属性设置为 <xref:System.Xml.ReadState>。  当首次调用 <xref:System.Xml.XmlReader> 对象的 <xref:System.Xml.XmlReader.Read%2A> 方法时，<xref:System.Xml.XmlReader> 移动到 <xref:System.Xml.XPath.XPathNavigator> 的当前节点上。  新的 <xref:System.Xml.XmlReader> 对象继续执行读取操作，直到到达 XML 树的结尾为止。  此时，<xref:System.Xml.XmlReader.Read%2A> 方法返回 `false`，<xref:System.Xml.XmlReader> 对象的 <xref:System.Xml.XmlReader.ReadState%2A> 属性设置为 <xref:System.Xml.ReadState>。  
  
 创建或移动 <xref:System.Xml.XmlReader> 对象时不会更改 <xref:System.Xml.XPath.XPathNavigator> 对象的位置。  <xref:System.Xml.XPath.XPathNavigator.ReadSubtree%2A> 方法只有在位于元素或根节点上时才有效。  
  
 以下示例显示如何获取包含 <xref:System.Xml.XPath.XPathDocument> 对象中的整个 XML 文档以及单个节点及其子节点的 <xref:System.Xml.XmlReader> 对象。  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Stream the entire XML document to the XmlReader.  
Dim xml As XmlReader = navigator.ReadSubtree()  
  
While xml.Read()  
    Console.WriteLine(xml.ReadInnerXml())  
End While  
  
xml.Close()  
  
' Stream the book element and its child nodes to the XmlReader.  
navigator.MoveToChild("bookstore", "")  
navigator.MoveToChild("book", "")  
  
Dim book As XmlReader = navigator.ReadSubtree()  
  
While book.Read()  
    Console.WriteLine(book.ReadInnerXml())  
End While  
  
book.Close()  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Stream the entire XML document to the XmlReader.  
XmlReader xml = navigator.ReadSubtree();  
  
while (xml.Read())  
{  
    Console.WriteLine(xml.ReadInnerXml());  
}  
  
xml.Close();  
  
// Stream the book element and its child nodes to the XmlReader.  
navigator.MoveToChild("bookstore", "");  
navigator.MoveToChild("book", "");  
  
XmlReader book = navigator.ReadSubtree();  
  
while (book.Read())  
{  
    Console.WriteLine(book.ReadInnerXml());  
}  
  
book.Close();  
```  
  
 该示例使用 `books.xml` 文件作为输入。  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
## 将 XPathNavigator 转换为 XmlWriter  
 <xref:System.Xml.XPath.XPathNavigator.WriteSubtree%2A> 方法用于将 XML 文档的全部内容或只是单个节点及其子节点流处理到 <xref:System.Xml.XmlWriter> 对象。  
  
 创建 <xref:System.Xml.XmlWriter> 对象时不会更改 <xref:System.Xml.XPath.XPathNavigator> 对象的位置。  
  
 以下示例显示如何获取包含 <xref:System.Xml.XPath.XPathDocument> 对象中的整个 XML 文档以及单个节点及其子节点的 <xref:System.Xml.XmlWriter> 对象。  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Stream the entire XML document to the XmlWriter.  
Dim xml As XmlWriter = XmlWriter.Create("newbooks.xml")  
navigator.WriteSubtree(xml)  
xml.Close()  
  
' Stream the book element and its child nodes to the XmlWriter.  
navigator.MoveToChild("bookstore", "")  
navigator.MoveToChild("book", "")  
  
Dim book As XmlWriter = XmlWriter.Create("book.xml")  
navigator.WriteSubtree(book)  
book.Close()  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Stream the entire XML document to the XmlWriter.  
XmlWriter xml = XmlWriter.Create("newbooks.xml");  
navigator.WriteSubtree(xml);  
xml.Close();  
  
// Stream the book element and its child nodes to the XmlWriter.  
navigator.MoveToChild("bookstore", "");  
navigator.MoveToChild("book", "");  
  
XmlWriter book = XmlWriter.Create("book.xml");  
navigator.WriteSubtree(book);  
book.Close();  
```  
  
 该示例使用本主题前面所示的 `books.xml` 文件作为输入。  
  
## 请参阅  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [使用 XPath 数据模型处理 XML 数据](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [使用 XPathNavigator 的节点集定位](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md)   
 [使用 XPathNavigator 的属性和命名空间节点定位](../../../../docs/standard/data/xml/attribute-and-namespace-node-navigation-using-xpathnavigator.md)   
 [使用 XPathNavigator 访问强类型 XML 数据](../../../../docs/standard/data/xml/accessing-strongly-typed-xml-data-using-xpathnavigator.md)