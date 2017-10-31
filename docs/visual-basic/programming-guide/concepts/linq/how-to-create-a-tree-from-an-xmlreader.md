---
title: "如何︰ 从 XmlReader (Visual Basic 中) 创建一个目录树 |Microsoft 文档"
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
ms.assetid: 6de683d8-177d-402b-b0de-d0539f1ce5d8
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a8dff4e518d8850b4050389e5677ac81ecd1e074
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-a-tree-from-an-xmlreader-visual-basic"></a>如何︰ 从 XmlReader (Visual Basic 中) 创建树
本主题演示如何直接从<xref:System.Xml.XmlReader>。</xref:System.Xml.XmlReader>创建 XML 树 若要创建<xref:System.Xml.Linq.XElement>从<xref:System.Xml.XmlReader>，则必须定位<xref:System.Xml.XmlReader>元素节点上。</xref:System.Xml.XmlReader> </xref:System.Xml.XmlReader> </xref:System.Xml.Linq.XElement> <xref:System.Xml.XmlReader>将跳过注释和处理指令，但如果<xref:System.Xml.XmlReader>是否定位在文本节点上，将引发错误。</xref:System.Xml.XmlReader> </xref:System.Xml.XmlReader> 若要避免此类错误，始终定位<xref:System.Xml.XmlReader>在元素之前创建 XML 树从<xref:System.Xml.XmlReader>。</xref:System.Xml.XmlReader>上</xref:System.Xml.XmlReader>  
  
## <a name="example"></a>示例  
 此示例使用下面的 XML 文档︰[示例 XML 文件︰ 书籍 (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-books-linq-to-xml.md)。  
  
 下面的代码创建一个 `T:System.Xml.XmlReader` 对象，然后读取节点，直到找到第一个元素节点。 然后加载<xref:System.Xml.Linq.XElement>对象。</xref:System.Xml.Linq.XElement>  
  
```vb  
Dim r As XmlReader = XmlReader.Create("books.xml")  
Do While r.NodeType <> XmlNodeType.Element  
    r.Read()  
Loop  
Dim e As XElement = XElement.Load(r)  
Console.WriteLine(e)  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Catalog>  
   <Book id="bk101">  
      <Author>Garghentini, Davide</Author>  
      <Title>XML Developer's Guide</Title>  
      <Genre>Computer</Genre>  
      <Price>44.95</Price>  
      <PublishDate>2000-10-01</PublishDate>  
      <Description>An in-depth look at creating applications   
      with XML.</Description>  
   </Book>  
   <Book id="bk102">  
      <Author>Garcia, Debra</Author>  
      <Title>Midnight Rain</Title>  
      <Genre>Fantasy</Genre>  
      <Price>5.95</Price>  
      <PublishDate>2000-12-16</PublishDate>  
      <Description>A former architect battles corporate zombies,   
      an evil sorceress, and her own childhood to become queen   
      of the world.</Description>  
   </Book>  
</Catalog>  
```  
  
## <a name="see-also"></a>另请参阅  
 [分析 XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/parsing-xml.md)
