---
title: "序列化为文件、 Textwriter 和 XmlWriters3 |Microsoft 文档"
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
ms.assetid: 7a0c24df-79ef-41a0-87f5-e6cf79382da9
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
ms.openlocfilehash: 98662b8d84459ed051d048084c2755fa7aaf8247
ms.lasthandoff: 03/13/2017

---
# <a name="serializing-to-files-textwriters-and-xmlwriters"></a>序列化为文件、TextWriter 和 XmlWriter
您可以序列化 XML 树<xref:System.IO.File>、 <xref:System.IO.TextWriter>，或<xref:System.Xml.XmlWriter>.</xref:System.Xml.XmlWriter> </xref:System.IO.TextWriter> </xref:System.IO.File>  
  
 您可以序列化的任何 XML 组件，包括<xref:System.Xml.Linq.XDocument>和<xref:System.Xml.Linq.XElement>，为通过使用字符串`ToString`方法。</xref:System.Xml.Linq.XElement> </xref:System.Xml.Linq.XDocument>  
  
 如果您想要禁止格式化序列化为一个字符串时，可以使用<xref:System.Xml.Linq.XNode.ToString%2A?displayProperty=fullName>方法。</xref:System.Xml.Linq.XNode.ToString%2A?displayProperty=fullName>  
  
 序列化为文件时的默认行为是格式化 （缩进） 生成的 XML 文档。 缩进时，不会保留 XML 树中无意义的空白。 若要使用格式序列化时，使用不采用以下方法的重载之一<xref:System.Xml.Linq.SaveOptions>作为参数︰</xref:System.Xml.Linq.SaveOptions>  
  
-   <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName></xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName>  
  
 如果要选择不缩进，并保留无意义的空白 XML 树中，使用采用下列任一方法的重载之一<xref:System.Xml.Linq.SaveOptions>作为参数︰</xref:System.Xml.Linq.SaveOptions>  
  
-   <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName></xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName>  
  
 有关示例，请参见相应的参考主题。  
  
## <a name="see-also"></a>另请参阅  
 [序列化 XML 树 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/serializing-xml-trees.md)
