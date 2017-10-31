---
title: "使用 XML 声明 (Visual Basic 中) 进行序列化 |Microsoft 文档"
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
ms.assetid: 8726f79e-2bb0-4ba0-969d-197cca591647
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
ms.openlocfilehash: 373df9b28ae7434d33ae81eba701d289cf1aa4f7
ms.lasthandoff: 03/13/2017

---
# <a name="serializing-with-an-xml-declaration-visual-basic"></a>使用 XML 声明 (Visual Basic 中) 进行序列化
本主题说明如何控制序列化是否生成 XML 声明。  
  
## <a name="xml-declaration-generation"></a>XML 声明的生成  
 序列化为<xref:System.IO.File>或<xref:System.IO.TextWriter>使用<xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName>方法或<xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName>方法生成 XML 声明。</xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName> </xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName> </xref:System.IO.TextWriter> </xref:System.IO.File> 在序列化为<xref:System.Xml.XmlWriter>，编写器设置 (在指定<xref:System.Xml.XmlWriterSettings>对象) 确定是否生成 XML 声明。</xref:System.Xml.XmlWriterSettings> </xref:System.Xml.XmlWriter>  
  
 如果要使用 `ToString` 方法序列化为字符串，则生成的 XML 不会包括 XML 声明。  
  
### <a name="serializing-with-an-xml-declaration"></a>使用 XML 声明进行序列化  
 下面的示例创建<xref:System.Xml.Linq.XElement>、 将文档保存到文件中，并打印到控制台文件︰</xref:System.Xml.Linq.XElement>  
  
```vb  
Dim root As XElement = <Root>  
                           <Child>child content</Child>  
                       </Root>  
root.Save("Root.xml")  
Dim str As String = File.ReadAllText("Root.xml")  
Console.WriteLine(str)  
```  
  
 该示例产生下面的输出：  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<Root>  
  <Child>child content</Child>  
</Root>  
```  
  
### <a name="serializing-without-an-xml-declaration"></a>不带 XML 声明的序列化  
 下面的示例演示如何将保存<xref:System.Xml.Linq.XElement>到<xref:System.Xml.XmlWriter>。</xref:System.Xml.XmlWriter> </xref:System.Xml.Linq.XElement>  
  
```vb  
Dim sb As StringBuilder = New StringBuilder()  
Dim xws As XmlWriterSettings = New XmlWriterSettings()  
xws.OmitXmlDeclaration = True  
  
Using xw As XmlWriter = XmlWriter.Create(sb, xws)  
    Dim root = <Root>  
                   <Child>child content</Child>  
               </Root>  
    root.Save(xw)  
End Using  
Console.WriteLine(sb.ToString())  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Root><Child>child content</Child></Root>  
```  
  
## <a name="see-also"></a>另请参阅  
 [序列化 XML 树 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/serializing-xml-trees.md)
