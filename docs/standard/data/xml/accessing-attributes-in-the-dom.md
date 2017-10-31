---
title: "访问 DOM 中的属性 | Microsoft Docs"
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
ms.assetid: ce2df341-a1a4-4e97-8e1b-cd45b8e3e71e
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# 访问 DOM 中的属性
属性是元素的属性，不是元素的子级。  这一区别很重要，因为用来浏览 XML 文档对象模型 \(DOM\) 的同级、父级和子节点的方法不同。  例如，**PreviousSibling** 和 **NextSibling** 方法不用来从元素浏览到属性或在属性间浏览。  属性是元素的属性，归元素所有，具有一个 **OwnerElement** 属性而非 **parentNode** 属性，并且具有不同的浏览方法。  
  
 当当前节点是元素时，请使用 **HasAttribute** 方法查看是否存在任何与此元素关联的属性。  如果已知元素具有属性，有多种方法可以访问这些属性。  要从元素中检索单个属性，可使用 **XmlElement** 的 **GetAttribute** 和 **GetAttributeNode** 方法，也可以将所有属性收集到一个集合中。  如果需要循环访问集合，获取集合就很有用。  如果您需要一个元素中的所有属性，可使用该元素的 **Attributes** 属性将所有属性检索到一个集合中。  
  
## 将所有属性检索到一个集合中  
 如果您需要将一个元素节点的所有属性放入到一个集合中，可调用 **XmlElement.Attributes** 属性。  这将获取包含元素的所有属性的 **XmlAttributeCollection**。  **XmlAttributeCollection** 类从 **XmlNamedNode** 映射继承。  因此，该集合可用的方法和属性，除了 **XmlAttributeCollection** 类特定的方法和属性（如 **ItemOf** 属性或 **Append** 方法）外，还包括命名的节点映射上可用的方法和属性。  该属性集合中的每一项表示一个 **XmlAttribute** 节点。  若要确定元素的属性数，请获取 **XmlAttributeCollection** 并使用 **Count** 属性查看该集合中的 **XmlAttribute** 节点数。  
  
 下面的代码示例显示如何检索一个属性集合，以及如何用 **Count** 方法作为循环索引，循环访问此集合。  然后，此代码显示如何从集合中检索单个属性并显示其值。  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
  
Public Class Sample  
  
    Public Shared Sub Main()  
  
        Dim doc As XmlDocument = New XmlDocument()  
        doc.LoadXml("<book genre='novel' ISBN='1-861001-57-5' misc='sale item'>" & _  
               "<title>The Handmaid's Tale</title>" & _  
               "<price>14.95</price>" & _  
               "</book>")  
  
        ' Move to an element.   
        Dim myElement As XmlElement = doc.DocumentElement  
  
        ' Create an attribute collection from the element.  
        Dim attrColl As XmlAttributeCollection = myElement.Attributes  
  
        ' Show the collection by iterating over it.  
        Console.WriteLine("Display all the attributes in the collection...")  
        Dim i As Integer  
        For i = 0 To attrColl.Count - 1  
            Console.Write("{0} = ", attrColl.ItemOf(i).Name)  
            Console.Write("{0}", attrColl.ItemOf(i).Value)  
            Console.WriteLine()  
        Next  
  
        ' Retrieve a single attribute from the collection; specifically, the  
        ' attribute with the name "misc".  
        Dim attr As XmlAttribute = attrColl("misc")  
  
        ' Retrieve the value from that attribute.  
        Dim miscValue As String = attr.InnerXml  
  
        Console.WriteLine("Display the attribute information.")  
        Console.WriteLine(miscValue)  
  
    End Sub  
End Class  
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
        doc.LoadXml("<book genre='novel' ISBN='1-861001-57-5' misc='sale item'>" +  
                      "<title>The Handmaid's Tale</title>" +  
                      "<price>14.95</price>" +  
                      "</book>");  
  
        // Move to an element.  
        XmlElement myElement = doc.DocumentElement;  
  
        // Create an attribute collection from the element.  
        XmlAttributeCollection attrColl = myElement.Attributes;  
  
        // Show the collection by iterating over it.  
        Console.WriteLine("Display all the attributes in the collection...");  
        for (int i = 0; i < attrColl.Count; i++)  
        {  
            Console.Write("{0} = ", attrColl[i].Name);  
            Console.Write("{0}", attrColl[i].Value);  
            Console.WriteLine();  
        }  
  
        // Retrieve a single attribute from the collection; specifically, the  
        // attribute with the name "misc".  
        XmlAttribute attr = attrColl["misc"];  
  
        // Retrieve the value from that attribute.  
        String miscValue = attr.InnerXml;  
  
        Console.WriteLine("Display the attribute information.");  
        Console.WriteLine(miscValue);  
  
    }  
}  
```  
  
 此示例显示以下输出内容：  
  
 **输出**  
  
 显示集合中的所有属性。  
  
```  
genre = novel  
ISBN = 1-861001-57-5  
misc = sale item  
Display the attribute information.  
sale item  
```  
  
 可按名称或索引号检索属性集合中的信息。  上例显示了如何按名称检索数据。  下例将显示如何按索引编号检索数据。  
  
 因为 **XmlAttributeCollection** 是一个集合并可以按名称或索引循环访问，本示例显示如何从该集合中选择第一个属性（使用从零开始的索引并以下面的 **baseuri.xml** 文件作为输入）。  
  
### 输入  
  
```  
<!-- XML fragment -->  
<book genre="novel">  
  <title>Pride And Prejudice</title>  
</book>  
```  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.IO  
Imports System.Xml  
  
Public Class Sample  
  
    Public Shared Sub Main()  
        ' Create the XmlDocument.  
        Dim doc As New XmlDocument()  
        doc.Load("http://localhost/baseuri.xml")  
  
        ' Display information on the attribute node. The value  
        ' returned for BaseURI is 'http://localhost/baseuri.xml'.  
        Dim attr As XmlAttribute = doc.DocumentElement.Attributes(0)  
        Console.WriteLine("Name of the attribute:  {0}", attr.Name)  
        Console.WriteLine("Base URI of the attribute:  {0}", attr.BaseURI)  
        Console.WriteLine("The value of the attribtue:  {0}", attr.InnerText)  
    End Sub 'Main   
End Class 'Sample  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
  
public class Sample  
{  
  public static void Main()  
  {  
    // Create the XmlDocument.  
    XmlDocument doc = new XmlDocument();  
  
    doc.Load("http://localhost/baseuri.xml");  
  
    // Display information on the attribute node. The value  
    // returned for BaseURI is 'http://localhost/baseuri.xml'.  
    XmlAttribute attr = doc.DocumentElement.Attributes[0];  
    Console.WriteLine("Name of the attribute:  {0}", attr.Name);  
    Console.WriteLine("Base URI of the attribute:  {0}", attr.BaseURI);  
    Console.WriteLine("The value of the attribtue:  {0}", attr.InnerText);  
  }  
}  
```  
  
## 检索单个属性节点  
 若要从元素中检索单个属性节点，请使用 <xref:System.Xml.XmlElement.GetAttributeNode%2A?displayProperty=fullName> 方法。  它返回一个类型为 **XmlAttribute** 的对象。  有了 **XmlAttribute** 对象后，[XmlAttribute 成员](frlrfsystemxmlxmlattributeclasstopic)类中所有可用的方法和属性都可以用于该对象，例如查找 **OwnerElement**。  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
  
Public Class Sample  
  
    Public Shared Sub Main()  
  
        Dim doc As XmlDocument = New XmlDocument()  
        doc.LoadXml("<book genre='novel' ISBN='1-861001-57-5' misc='sale item'>" & _  
               "<title>The Handmaid's Tale</title>" & _  
               "<price>14.95</price>" & _  
               "</book>")  
  
        ' Move to an element.  
        Dim root As XmlElement  
        root = doc.DocumentElement  
  
        ' Get an attribute.  
        Dim attr As XmlAttribute  
        attr = root.GetAttributeNode("ISBN")  
  
        ' Display the value of the attribute.  
        Dim attrValue As String  
        attrValue = attr.InnerXml  
        Console.WriteLine(attrValue)  
  
    End Sub  
End Class  
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
     doc.LoadXml("<book genre='novel' ISBN='1-861003-78' misc='sale item'>" +  
                   "<title>The Handmaid's Tale</title>" +  
                   "<price>14.95</price>" +  
                   "</book>");   
  
    // Move to an element.  
     XmlElement root = doc.DocumentElement;  
  
    // Get an attribute.  
     XmlAttribute attr = root.GetAttributeNode("ISBN");  
  
    // Display the value of the attribute.  
     String attrValue = attr.InnerXml;  
     Console.WriteLine(attrValue);  
  
    }  
}  
```  
  
 您也可以如前例所示，从属性集合中检索单个属性节点。  下面的代码示例显示如何编写一行代码来按索引号从 XML 文档树的根节点（也称为 **DocumentElement** 属性）检索单个属性。  
  
```  
XmlAttribute attr = doc.DocumentElement.Attributes[0];  
```  
  
## 请参阅  
 [XML 文档对象模型 \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)