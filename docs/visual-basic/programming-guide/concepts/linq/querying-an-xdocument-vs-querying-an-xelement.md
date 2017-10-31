---
title: "查询 XDocument 与查询 XElement (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 2d111f84-0ded-4cde-8d93-5440557a726d
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 29044cd118bfd8ecc12bddca722ee3656d455e0f
ms.lasthandoff: 03/13/2017


---
# <a name="querying-an-xdocument-vs-querying-an-xelement-visual-basic"></a>查询 XDocument 与查询 XElement (Visual Basic)
通过<xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName>，您将注意到，您需要编写查询稍有不同于通过<xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName>。</xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName>负载时，</xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName>将文档加载时  
  
## <a name="comparison-of-xdocumentload-and-xelementload"></a>XDocument.Load 与 XElement.Load 的比较  
 当您将 XML 文档加载到<xref:System.Xml.Linq.XElement>通过<xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName>、<xref:System.Xml.Linq.XElement>根目录下的 XML 树包含所加载文档的根元素。</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName> </xref:System.Xml.Linq.XElement> 但是，当您加载同一个 XML 文档<xref:System.Xml.Linq.XDocument><xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName>树的根<xref:System.Xml.Linq.XDocument>节点，然后加载文档的根元素是一个允许的子<xref:System.Xml.Linq.XElement>节点的<xref:System.Xml.Linq.XDocument>。</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument> ，</xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName>通过</xref:System.Xml.Linq.XDocument> [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 轴相对于根节点进行操作。  
  
 第一个示例加载使用<xref:System.Xml.Linq.XElement.Load%2A>。</xref:System.Xml.Linq.XElement.Load%2A> XML 树 然后它查询树根部的子元素。  
  
```vb  
' Create a simple document and  write it to a file  
File.WriteAllText("Test.xml", "<Root>" + Environment.NewLine + _  
    "    <Child1>1</Child1>" + Environment.NewLine + _  
    "    <Child2>2</Child2>" + Environment.NewLine + _  
    "    <Child3>3</Child3>" + Environment.NewLine + _  
    "</Root>")  
  
Console.WriteLine("Querying tree loaded with XElement.Load")  
Console.WriteLine("----")  
Dim doc As XElement = XElement.Load("Test.xml")  
Dim childList As IEnumerable(Of XElement) = _  
        From el In doc.Elements() _  
        Select el  
For Each e As XElement In childList  
    Console.WriteLine(e)  
Next  
```  
  
 此示例将按预期产生以下输出：  
  
```  
Querying tree loaded with XElement.Load  
----  
<Child1>1</Child1>  
<Child2>2</Child2>  
<Child3>3</Child3>  
```  
  
 下面的示例是一个相同更高版本，与 XML 树加载到<xref:System.Xml.Linq.XDocument>而不是<xref:System.Xml.Linq.XElement>。</xref:System.Xml.Linq.XElement></xref:System.Xml.Linq.XDocument>异常  
  
```vb  
' Create a simple document and  write it to a file  
File.WriteAllText("Test.xml", "<Root>" + Environment.NewLine + _  
    "    <Child1>1</Child1>" + Environment.NewLine + _  
    "    <Child2>2</Child2>" + Environment.NewLine + _  
    "    <Child3>3</Child3>" + Environment.NewLine + _  
    "</Root>")  
  
Console.WriteLine("Querying tree loaded with XDocument.Load")  
Console.WriteLine("----")  
Dim doc As XDocument = XDocument.Load("Test.xml")  
Dim childList As IEnumerable(Of XElement) = _  
        From el In doc.Elements() _  
        Select el  
For Each e As XElement In childList  
    Console.WriteLine(e)  
Next  
```  
  
 该示例产生下面的输出：  
  
```  
Querying tree loaded with XDocument.Load  
----  
<Root>  
  <Child1>1</Child1>  
  <Child2>2</Child2>  
  <Child3>3</Child3>  
</Root>  
```  
  
 请注意，同样的查询返回一个 `Root` 节点，而不是返回三个子节点。  
  
 处理这一种方法是使用<xref:System.Xml.Linq.XDocument.Root%2A>属性之前访问轴方法，如下所示︰</xref:System.Xml.Linq.XDocument.Root%2A>  
  
```vb  
' Create a simple document and  write it to a file  
File.WriteAllText("Test.xml", "<Root>" + Environment.NewLine + _  
    "    <Child1>1</Child1>" + Environment.NewLine + _  
    "    <Child2>2</Child2>" + Environment.NewLine + _  
    "    <Child3>3</Child3>" + Environment.NewLine + _  
    "</Root>")  
  
Console.WriteLine("Querying tree loaded with XDocument.Load")  
Console.WriteLine("----")  
Dim doc As XDocument = XDocument.Load("Test.xml")  
Dim childList As IEnumerable(Of XElement) = _  
        From el In doc.Root.Elements() _  
        Select el  
For Each e As XElement In childList  
    Console.WriteLine(e)  
Next  
```  
  
 此查询现在在相同的执行方式与在树上查询来源于<xref:System.Xml.Linq.XElement>。</xref:System.Xml.Linq.XElement> 此示例产生以下输出：  
  
```  
Querying tree loaded with XDocument.Load  
----  
<Child1>1</Child1>  
<Child2>2</Child2>  
<Child3>3</Child3>  
```  
  
## <a name="see-also"></a>另请参阅  
 [基本查询 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/basic-queries-linq-to-xml.md)
