---
title: "使用 XPathNavigator 计算 XPath 表达式 | Microsoft Docs"
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
ms.assetid: 2913ccf3-f932-4363-8028-9e2d22ce6093
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# 使用 XPathNavigator 计算 XPath 表达式
<xref:System.Xml.XPath.XPathNavigator> 类提供了 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 方法来计算 XPath 表达式。  <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 方法使用 XPath 表达式，计算表达式，然后基于 XPath 表达式的结果返回 Boolean、Number、String 或 Node Set 的 W3C XPath 类型。  
  
## Evaluate 方法  
 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 方法使用 XPath 表达式，计算表达式，然后返回 Boolean \(<xref:System.Boolean>\)、Number \(<xref:System.Double>\)、String \(<xref:System.String>\) 或 Node Set \(<xref:System.Xml.XPath.XPathNodeIterator>\) 的类型化结果。  例如，<xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 方法可以在数学方法中使用。  以下示例代码计算 `books.xml` 文件中的所有图书的总价格。  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
Dim query As XPathExpression = navigator.Compile("sum(//price/text())")  
Dim total As Double = CType(navigator.Evaluate(query), Double)  
Console.WriteLine(total)  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
XPathExpression query = navigator.Compile("sum(//price/text())");  
Double total = (Double)navigator.Evaluate(query);  
Console.WriteLine(total);  
```  
  
 该示例使用 `books.xml` 文件作为输入。  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
### position 和 last 函数  
 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 方法是重载方法。  一个 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 方法使用 <xref:System.Xml.XPath.XPathNodeIterator> 对象作为参数。  此特定的 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 方法与只使用 <xref:System.Xml.XPath.XPathExpression> 对象作为参数的 <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> 方法相同，只是允许使用节点集参数指定要执行计算的当前上下文。  XPath `position()` 和 `last()` 函数需要此上下文，因为这两个函数相对于当前上下文节点。  除非在定位步骤中作为谓词使用，`position()` 和 `last()` 函数要求引用节点集以便进行计算，否则，`position` 和 `last` 函数将返回 `0`。  
  
## 请参阅  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [使用 XPath 数据模型处理 XML 数据](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [使用 XPathNavigator 选择 XML 数据](../../../../docs/standard/data/xml/select-xml-data-using-xpathnavigator.md)   
 [使用 XPathNavigator 匹配节点](../../../../docs/standard/data/xml/matching-nodes-using-xpathnavigator.md)   
 [XPath 查询识别的节点类型](../../../../docs/standard/data/xml/node-types-recognized-with-xpath-queries.md)   
 [XPath 查询和命名空间](../../../../docs/standard/data/xml/xpath-queries-and-namespaces.md)   
 [已编译的 XPath 表达式](../../../../docs/standard/data/xml/compiled-xpath-expressions.md)