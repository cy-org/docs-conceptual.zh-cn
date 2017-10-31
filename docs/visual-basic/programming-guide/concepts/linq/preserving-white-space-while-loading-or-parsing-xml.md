---
title: "加载或分析 XML2 时保留空白 |Microsoft 文档"
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
ms.assetid: ef6518e0-2c8d-462c-8b92-a16e9dc737ad
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
ms.openlocfilehash: 39e4270acc0e9a9df5c3855f8c087f41d9612197
ms.lasthandoff: 03/13/2017

---
# <a name="preserving-white-space-while-loading-or-parsing-xml"></a>在加载或分析 XML 时保留空白
本主题说明如何控制 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 的空白行为。  
  
 一种常用情况是读取缩进的 XML，在内存中创建一个没有任何空白文本节点（即不保留空白）的 XML 树，对该 XML 执行某些操作，然后保存带缩进的 XML。 在序列化带格式的 XML 时，只保留 XML 树中有意义的空白。 这是 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 的默认行为。  
  
 另一个常见的情况是读取和修改已经有意缩进的 XML。 您可能不想以任何方式更改这种缩进。 若要在 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 中执行此操作，您要在加载或解析 XML 时保留空白，并在序列化 XML 时禁用格式设置。  
  
 本主题说明用于填充 XML 树的方法的空白行为。 有关序列化 XML 树时控制空白区域的信息，请参阅[保留空白时序列化](../../../../visual-basic/programming-guide/concepts/linq/preserving-white-space-while-serializing.md)。  
  
## <a name="behavior-of-methods-that-populate-xml-trees"></a>用于填充 XML 树的方法的行为  
 中的以下方法<xref:System.Xml.Linq.XElement>和<xref:System.Xml.Linq.XDocument>类填充 XML 树。</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> 您可以填充 XML 树从一个文件， <xref:System.IO.TextReader>、 <xref:System.Xml.XmlReader>，或一个字符串︰</xref:System.Xml.XmlReader> </xref:System.IO.TextReader>  
  
-   <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=fullName></xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName></xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName>  
  
-   <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=fullName></xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=fullName>  
  
 如果该方法不采用<xref:System.Xml.Linq.LoadOptions>作为参数，该方法将不保留无关紧要的空白区域。</xref:System.Xml.Linq.LoadOptions>  
  
 在大多数情况下，如果该方法采用<xref:System.Xml.Linq.LoadOptions>作为参数，您可以选择保留无意义的空白作为 XML 树中的文本节点。</xref:System.Xml.Linq.LoadOptions> 但是，如果该方法从 XML 加载<xref:System.Xml.XmlReader>，则<xref:System.Xml.XmlReader>确定是否保留空白区域。</xref:System.Xml.XmlReader> </xref:System.Xml.XmlReader> 设置<xref:System.Xml.Linq.LoadOptions>不起作用。</xref:System.Xml.Linq.LoadOptions>  
  
 使用这些方法，如果保留空白，无关紧要的空白区域插入到 XML 树中作为<xref:System.Xml.Linq.XText>节点。</xref:System.Xml.Linq.XText> 如果不保留空白，则不会插入文本节点。  
  
 可以通过使用<xref:System.Xml.XmlWriter>。</xref:System.Xml.XmlWriter>创建 XML 树 写入到的节点<xref:System.Xml.XmlWriter>在树中填充。</xref:System.Xml.XmlWriter> 但在使用此方法生成 XML 树时，不管节点是否为空白或是否为无意义的空白，都将保留所有节点。  
  
## <a name="see-also"></a>另请参阅  
 [分析 XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/parsing-xml.md)
