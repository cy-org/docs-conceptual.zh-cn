---
title: "为 DOM 中的元素创建新属性 | Microsoft Docs"
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
ms.assetid: dd6dc920-b011-418a-b3db-f1580a7d9251
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# 为 DOM 中的元素创建新属性
创建新属性不同于创建其他节点类型，因为属性不是节点，而是元素节点的属性并包含在与元素关联的 **XmlAttributeCollection** 中。  有多种方法可创建属性并将其附加到元素：  
  
-   获取元素节点并使用 **SetAttribute** 将属性添加到该元素的属性集合。  
  
-   使用 **CreateAttribute** 方法创建 **XmlAttribute** 节点，获取元素节点，然后使用 **SetAttributeNode** 将节点添加到该元素的属性集合。  
  
 下面的示例显示如何使用 **SetAttribute** 方法将属性添加到元素。  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
  
public class Sample  
  
  public shared sub Main()  
  
  Dim doc as XmlDocument = new XmlDocument()  
  doc.LoadXml("<book xmlns:bk='urn:samples' bk:ISBN='1-861001-57-5'>" & _  
              "<title>Pride And Prejudice</title>" & _  
              "</book>")  
  Dim root as XmlElement = doc.DocumentElement  
  
  'Add a new attribute.  
  root.SetAttribute("genre", "urn:samples", "novel")  
  
  Console.WriteLine("Display the modified XML...")  
  Console.WriteLine(doc.InnerXml)  
  
  end sub  
end class  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
  
public class Sample  
{  
  public static void Main()  
  {  
    XmlDocument doc = new XmlDocument();  
    doc.LoadXml("<book xmlns:bk='urn:samples' bk:ISBN='1-861001-57-5'>" +  
                "<title>Pride And Prejudice</title>" +  
                "</book>");  
    XmlElement root = doc.DocumentElement;  
  
    // Add a new attribute.  
    root.SetAttribute("genre", "urn:samples", "novel");  
  
    Console.WriteLine("Display the modified XML...");  
    Console.WriteLine(doc.InnerXml);  
  }  
```  
  
 下面的示例显示一个用 **CreateAttribute** 方法创建的新属性。  然后显示使用 **SetAttributeNode** 方法添加到 **book** 元素的属性集合的属性。  
  
 已知下列 XML：  
  
```  
<book genre='novel' ISBN='1-861001-57-5'>  
<title>Pride And Prejudice</title>  
</book>  
```  
  
 创建一个新属性并为其提供值：  
  
```vb  
Dim attr As XmlAttribute = doc.CreateAttribute("publisher")  
   attr.Value = "WorldWide Publishing"  
```  
  
```csharp  
XmlAttribute attr = doc.CreateAttribute("publisher");  
attr.Value = "WorldWide Publishing";  
```  
  
 将其附加到此元素：  
  
```vb  
doc.DocumentElement.SetAttributeNode(attr)  
```  
  
```csharp  
doc.DocumentElement.SetAttributeNode(attr);  
```  
  
 **输出**  
  
```  
<book genre="novel" ISBN="1-861001-57-5" publisher="WorldWide Publishing">  
<title>Pride And Prejudice</title>  
</book>  
```  
  
 完整代码示例位于 [XmlDocument.CreateAttribute 方法](frlrfSystemXmlXmlDocumentClassCreateAttributeTopic)。  
  
 还可以创建一个 **XmlAttribute** 节点并使用 **InsertBefore** 或 **InsertAfter** 方法将其放在集合中的适当位置。  如果该属性集合中已存在一个同名属性，则从该集合中移除现有的 **XmlAttribute** 节点并插入新的 **XmlAttribute** 节点。  这与 **SetAttribute** 方法执行的方式相同。  这些方法（作为参数）将现有节点作为执行 **InsertBefore** 和 **InsertAfter** 的参考点。  如果不提供指示插入新节点位置的参考节点，则 **InsertAfter** 方法的默认设置是在集合的开头插入新节点。  如果未提供任何参考节点，则 **InsertBefore** 的默认位置是集合的末尾。  
  
 如果创建了属性的 **XmlNamedNodeMap**，则可以使用 [SetNamedItem 方法](frlrfSystemXmlXmlNamedNodeMapClassSetNamedItemTopic)按名称添加属性。  有关更多信息，请参见 [NamedNodeMap 和 NodeList 中的节点集合](../../../../docs/standard/data/xml/node-collections-in-namednodemaps-and-nodelists.md)。  
  
## 默认属性  
 如果创建一个声明为具有默认属性的元素，则 XML 文档对象模型 \(DOM\) 创建一个带默认值的新默认属性并将其附加到该元素。  此时还创建默认属性的子节点。  
  
## 属性子节点  
 属性节点的值成为它的子节点。  有效子节点只有两种类型：**XmlText** 节点和 **XmlEntityReference** 节点。  从 **FirstChild** 和 **LastChild** 等方法将这些节点按子节点来处理这一点上说，它们是子节点。  当试图移除属性或属性子节点时，属性这种具有子节点的特性很重要。  有关更多信息，请参见[移除 DOM 中元素节点的属性](../../../../docs/standard/data/xml/removing-attributes-from-an-element-node-in-the-dom.md)。  
  
## 请参阅  
 [XML 文档对象模型 \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)