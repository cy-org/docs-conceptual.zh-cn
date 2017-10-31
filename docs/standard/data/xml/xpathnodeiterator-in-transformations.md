---
title: "转换中的 XPathNodeIterator | Microsoft Docs"
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
ms.assetid: 2bc6ddc6-674a-4f75-b264-abc35e4e5857
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# 转换中的 XPathNodeIterator
<xref:System.Xml.XPath.XPathNodeIterator> 提供的方法可以循环访问执行 XML 路径语言 \(XPath\) 查询所创建的节点集或者使用 node\-set 方法转换成节点集的结果树片段。  <xref:System.Xml.XPath.XPathNodeIterator> 使您能够循环访问该节点集内的节点。  检索到节点集后，<xref:System.Xml.XPath.XPathNodeIterator> 类提供对选定节点集的只读、只进游标。  该节点集以文档顺序创建，因此调用此方法会移到文档顺序中的下一个节点。  <xref:System.Xml.XPath.XPathNodeIterator> 不生成节点集内所有节点的节点树，  而是提供数据的单节点窗口，当您在树中浏览时，会公开所指向的基础节点。  <xref:System.Xml.XPath.XPathNodeIterator> 类中可用的方法和属性使您能够获取当前节点中的信息。  有关可用方法和属性的列表，请参见 [XPathNodeIterator 成员](frlrfsystemxmlxpathxpathnodeiteratormemberstopic)。  
  
 由于 <xref:System.Xml.XPath.XPathNodeIterator> 在 XPath 查询创建的节点集中移动，并且只向前移动，因此，移动方法是使用 <xref:System.Xml.XPath.XPathNodeIterator.MoveNext%2A> 方法。  此方法的返回类型是 `Boolean`，如果移到下一选定节点，则返回 `true`，如果再也没有其他选定节点，则返回 `false`。  如果返回 `true`，下表显示了可用的属性：  
  
-   <xref:System.Xml.XPath.XPathNodeIterator.Current%2A>  
  
-   <xref:System.Xml.XPath.XPathNodeIterator.CurrentPosition%2A>  
  
-   <xref:System.Xml.XPath.XPathNodeIterator.Count%2A>  
  
 第一次查看一个节点集时，必须调用 <xref:System.Xml.XPath.XPathNodeIterator.MoveNext%2A> 以将 <xref:System.Xml.XPath.XPathNodeIterator> 定位在选定节点集的第一个节点上。  这样可以编写 while 循环。  
  
 以下代码示例显示如何将 <xref:System.Xml.XPath.XPathNodeIterator> 作为 <xref:System.Xml.Xsl.XsltArgumentList> 中的参数传递给 <xref:System.Xml.Xsl.XslTransform>。  代码输入是 **books.xml**，样式表是 **text.xsl**。  文件 **test.xml** 是 <xref:System.Xml.XPath.XPathDocument>。  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Xml  
Imports System.Xml.Xsl  
Imports System.Xml.XPath  
Imports System.Text  
  
Public Class sample  
  
   Public Shared Sub Main()  
      Dim Doc As New XPathDocument("books.xml")  
      Dim nav As XPathNavigator = Doc.CreateNavigator()  
      Dim Iterator As XPathNodeIterator = nav.Select("/bookstore/book")  
  
      Dim arg As New XsltArgumentList()  
      arg.AddParam("param1", "", Iterator)  
  
      Dim xslt As New XslTransform()  
      xslt.Load("test.xsl")  
  
      Dim xd As New XPathDocument("test.xml")  
  
      Dim strmTemp = New FileStream("out.xml", FileMode.Create, FileAccess.ReadWrite)  
      xslt.Transform(xd, arg, strmTemp, Nothing)  
   End Sub 'Main  
End Class 'sample  
  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Xml;  
using System.Xml.Xsl;  
using System.Xml.XPath;  
using System.Text;  
  
public class sample  
{  
    public static void Main()  
    {  
        XPathDocument Doc = new XPathDocument("books.xml");  
        XPathNavigator nav = Doc.CreateNavigator();  
        XPathNodeIterator Iterator = nav.Select("/bookstore/book");  
  
        XsltArgumentList arg = new XsltArgumentList();  
        arg.AddParam("param1", "", Iterator);  
  
        XslTransform xslt = new XslTransform();  
        xslt.Load("test.xsl");  
  
        XPathDocument xd = new XPathDocument("test.xml");  
  
        Stream strmTemp = new FileStream("out.xml", FileMode.Create, FileAccess.ReadWrite);  
        xslt.Transform(xd, arg, strmTemp, null);  
    }  
}  
```  
  
## books.xml  
  
```  
<?xml version='1.0'?>  
<!-- This file represents a fragment of a book store inventory database. -->  
<bookstore specialty="novel">  
    <book style="autobiography">  
    <title>Seven Years in Trenton</title>  
        <author>  
            <first-name>Jay</first-name>  
            <last-name>Adams</last-name>  
            <award>Trenton Literary Review Honorable Mention</award>  
            <country>USA</country>  
        </author>  
        <price>12</price>  
    </book>  
    <book style="textbook">  
        <title>History of Trenton</title>  
        <author>  
            <first-name>Kim</first-name>  
            <last-name>Akers</last-name>  
            <publication>  
                Selected Short Stories of  
                <first-name>Scott</first-name>  
                <last-name>Bishop</last-name>  
                <country>US</country>  
            </publication>  
        </author>  
        <price>55</price>  
    </book>  
</bookstore>  
```  
  
## test.xsl  
  
```  
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
xmlns:msxsl="urn:schemas-microsoft-com:xslt" exclude-result-prefixes="msxsl">  
  
<xsl:output method="xml" indent="yes"/>  
<xsl:param name="param1"/>  
  
<xsl:template match="/">  
    <out>  
        <xsl:for-each select="$param1/title">  
            <title><xsl:value-of select="."/></title>  
        </xsl:for-each>  
    </out>  
</xsl:template>  
  
</xsl:stylesheet>  
```  
  
## test.xml  
  
```  
<Title attr="Test">this is a test</Title>  
```  
  
## 输出 \(out.xml\)  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<out>  
  <title>Seven Years in Trenton</title>  
  <title>History of Trenton</title>  
</out>  
```  
  
## 请参阅  
 [XslTransform 类实现 XSLT 处理器](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)