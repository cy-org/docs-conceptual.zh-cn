---
title: "预先原子化 XName 对象 (LINQ to XML) (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 06ea104b-f44c-4bb2-9c34-889ae025c80d
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 519b64a96e03e098d7325cfb779bcd5d53db3741
ms.lasthandoff: 03/13/2017


---
# <a name="pre-atomization-of-xname-objects-linq-to-xml-visual-basic"></a>预先原子化 XName 对象 (LINQ to XML) (Visual Basic)
提高 LINQ to XML 中的性能的一种方法是预原子化<xref:System.Xml.Linq.XName>对象。</xref:System.Xml.Linq.XName> 预原子化是指将分配到的字符串<xref:System.Xml.Linq.XName>对象之前使用的构造函数创建 XML 树<xref:System.Xml.Linq.XElement>和<xref:System.Xml.Linq.XAttribute>类。</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XName> 然后，而不是将字符串传递给构造函数，此过程将使用隐式转换从字符串到<xref:System.Xml.Linq.XName>，传递初始化<xref:System.Xml.Linq.XName>对象。</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XName>  
  
 当创建其中重复出现特定名称的大型 XML 树时，这样可以提高性能。 若要执行此操作，您可以声明并初始化<xref:System.Xml.Linq.XName>对象之前构造 XML 树，然后使用<xref:System.Xml.Linq.XName>对象而不是指定元素和属性名称的字符串。</xref:System.Xml.Linq.XName> </xref:System.Xml.Linq.XName> 当创建大量具有相同名称的元素（或属性）时，此技术可以显著提高性能。  
  
 应针对您的方案测试预原子化以确定是否应使用它。  
  
## <a name="example"></a>示例  
 下面的示例演示这一操作。  
  
```vb  
Dim Root__1 As XName = "Root"  
Dim Data As XName = "Data"  
Dim ID As XName = "ID"  
  
Dim root__2 As New XElement(Root__1, New XElement(Data, New XAttribute(ID, "1"), "4,100,000"), New XElement(Data, New XAttribute(ID, "2"), "3,700,000"), New XElement(Data, New XAttribute(ID, "3"), "1,150,000"))  
  
Console.WriteLine(root__2)  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Root>  
  <Data ID="1">4,100,000</Data>  
  <Data ID="2">3,700,000</Data>  
  <Data ID="3">1,150,000</Data>  
</Root>  
```  
  
 下面的示例演示针对命名空间中的 XML 文档的相同技术：  
  
```vb  
Dim aw As XNamespace = "http://www.adventure-works.com"  
Dim Root__1 As XName = aw + "Root"  
Dim Data As XName = aw + "Data"  
Dim ID As XName = "ID"  
  
Dim root__2 As New XElement(Root__1, New XAttribute(XNamespace.Xmlns + "aw", aw), New XElement(Data, New XAttribute(ID, "1"), "4,100,000"), New XElement(Data, New XAttribute(ID, "2"), "3,700,000"), New XElement(Data, New XAttribute(ID, "3"), "1,150,000"))  
  
Console.WriteLine(root__2)  
```  
  
 该示例产生下面的输出：  
  
```xml  
<aw:Root xmlns:aw="http://www.adventure-works.com">  
  <aw:Data ID="1">4,100,000</aw:Data>  
  <aw:Data ID="2">3,700,000</aw:Data>  
  <aw:Data ID="3">1,150,000</aw:Data>  
</aw:Root>  
```  
  
 下面的示例更类似于实际中可能遇到的情况。 在此示例中，元素的内容由查询提供：  
  
```vb  
Dim Root__1 As XName = "Root"  
Dim Data As XName = "Data"  
Dim ID As XName = "ID"  
  
Dim t1 As DateTime = DateTime.Now  
Dim root__2 As New XElement(Root__1, From i In System.Linq.Enumerable.Range(1, 100000)New XElement(Data, New XAttribute(ID, i), i * 5))  
Dim t2 As DateTime = DateTime.Now  
  
Console.WriteLine("Time to construct:{0}", t2 - t1)  
```  
  
 上一示例的执行性能优于下面的示例（其中未对名称进行预原子化）：  
  
```vb  
Dim t1 As DateTime = DateTime.Now  
Dim root As New XElement("Root", From i In System.Linq.Enumerable.Range(1, 100000)New XElement("Data", New XAttribute("ID", i), i * 5))  
Dim t2 As DateTime = DateTime.Now  
  
Console.WriteLine("Time to construct:{0}", t2 - t1)  
```  
  
## <a name="see-also"></a>另请参阅  
 [性能 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/performance-linq-to-xml.md)   
 [原子化 XName 和 XNamespace 对象 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/atomized-xname-and-xnamespace-objects-linq-to-xml.md)
