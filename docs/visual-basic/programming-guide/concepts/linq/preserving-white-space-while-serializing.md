---
title: "保留空白时 Serializing2 |Microsoft 文档"
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
ms.assetid: 2d7abbd4-37f4-422b-89dd-0a694b5edc17
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
ms.openlocfilehash: 9efa2940af9321401e7f9c01d6fb9d1f48616711
ms.lasthandoff: 03/13/2017

---
# <a name="preserving-white-space-while-serializing"></a>在序列化时保留空白
本主题描述在序列化 XML 树时如何控制空白。  
  
 一种常用情况是读取缩进的 XML，在内存中创建一个没有任何空白文本节点（即不保留空白）的 XML 树，对该 XML 执行某些操作，然后保存带缩进的 XML。 在序列化带格式的 XML 时，只保留 XML 树中有意义的空白。 这是 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 的默认行为。  
  
 另一个常见的情况是读取和修改已经有意缩进的 XML。 您可能不想以任何方式更改这种缩进。 若要在 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 中执行此操作，您要在加载或解析 XML 时保留空白，并在序列化 XML 时禁用格式设置。  
  
## <a name="white-space-behavior-of-methods-that-serialize-xml-trees"></a>用于序列化 XML 树的方法的空白行为  
 中的以下方法<xref:System.Xml.Linq.XElement>和<xref:System.Xml.Linq.XDocument>类序列化 XML 树。</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> 一个文件中，将 XML 树序列化为<xref:System.IO.TextReader>，或<xref:System.Xml.XmlReader>.</xref:System.Xml.XmlReader> </xref:System.IO.TextReader> `ToString` 方法序列化为字符串。  
  
-   <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName></xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XElement.ToString%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.ToString%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XDocument.ToString%2A?displayProperty=fullName></xref:System.Xml.Linq.XDocument.ToString%2A?displayProperty=fullName>  
  
 如果该方法不采用<xref:System.Xml.Linq.SaveOptions>作为参数，那么该方法将格式化 （缩进） 序列化的 XML。</xref:System.Xml.Linq.SaveOptions> 在这种情况下，将丢弃 XML 树中所有无意义的空白。  
  
 如果方法采用<xref:System.Xml.Linq.SaveOptions>作为参数，那么您可以指定该方法不格式化 （缩进） 序列化的 XML。</xref:System.Xml.Linq.SaveOptions> 在这种情况下，将保留 XML 树中的所有空白。  
  
## <a name="see-also"></a>另请参阅  
 [序列化 XML 树 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/serializing-xml-trees.md)
