---
title: "LINQ to XML 类概述 (Visual Basic) |Microsoft 文档"
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
ms.assetid: f11b62b5-d522-4c23-92ae-23186dc16447
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
ms.openlocfilehash: 12885f93bb7e56dd66d36090d41700195313e944
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-xml-classes-overview-visual-basic"></a>LINQ to XML 类概述 (Visual Basic)
本主题提供了一份[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]中的类<xref:System.Xml.Linq>命名空间，以及每个简短说明。</xref:System.Xml.Linq>  
  
## <a name="linq-to-xml-classes"></a>LINQ to XML 类  
  
### <a name="xattribute-class"></a>XAttribute 类  
 <xref:System.Xml.Linq.XAttribute>表示一个 XML 属性。</xref:System.Xml.Linq.XAttribute> 有关详细的信息和示例，请参阅[XAttribute 类概述 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/xattribute-class-overview.md)。  
  
### <a name="xcdata-class"></a>XCData 类  
 <xref:System.Xml.Linq.XCData>表示一个 CDATA 文本节点。</xref:System.Xml.Linq.XCData>  
  
### <a name="xcomment-class"></a>XComment 类  
 <xref:System.Xml.Linq.XComment>表示一个 XML 注释。</xref:System.Xml.Linq.XComment>  
  
### <a name="xcontainer-class"></a>XContainer 类  
 <xref:System.Xml.Linq.XContainer>是可以有子节点的所有节点的抽象基类。</xref:System.Xml.Linq.XContainer> 下面的类派生自<xref:System.Xml.Linq.XContainer>类︰</xref:System.Xml.Linq.XContainer>  
  
-   <xref:System.Xml.Linq.XElement>  
  
-   <xref:System.Xml.Linq.XDocument></xref:System.Xml.Linq.XDocument>  
  
### <a name="xdeclaration-class"></a>XDeclaration 类  
 <xref:System.Xml.Linq.XDeclaration>表示一个 XML 声明。</xref:System.Xml.Linq.XDeclaration> XML 声明用于声明 XML 版本和文档的编码。 此外，XML 声明还指定 XML 文档是否为独立文档。 如果文档是独立文档，则在外部 DTD 或从内部子集引用的外部参数实体中不存在外部标记声明。  
  
### <a name="xdocument-class"></a>XDocument 类  
 <xref:System.Xml.Linq.XDocument>表示 XML 文档。</xref:System.Xml.Linq.XDocument> 有关详细的信息和示例，请参阅[XDocument 类概述 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/xdocument-class-overview.md)。  
  
### <a name="xdocumenttype-class"></a>XDocumentType 类  
 <xref:System.Xml.Linq.XDocumentType>表示 XML 文档类型定义 (DTD)。</xref:System.Xml.Linq.XDocumentType>  
  
### <a name="xelement-class"></a>XElement 类  
 <xref:System.Xml.Linq.XElement>表示一个 XML 元素。</xref:System.Xml.Linq.XElement> 有关详细的信息和示例，请参阅[XElement 类概述 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/xelement-class-overview.md)。  
  
### <a name="xname-class"></a>XName 类  
 <xref:System.Xml.Linq.XName>表示元素的名称 (<xref:System.Xml.Linq.XElement>) 和属性 (<xref:System.Xml.Linq.XAttribute>)。</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement></xref:System.Xml.Linq.XName> 有关详细的信息和示例，请参阅[XDocument 类概述 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/xdocument-class-overview.md)。  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 旨在使 XML 名称尽可能简单。 XML 名称由于复杂而通常被视为 XML 中的高级主题。 有证据证明，这种复杂性不是由开发人员编程时通常使用的命名空间造成的，而是由命名空间前缀造成的。 使用命名空间前缀可以减少输入 XML 时需要的击键数或使 XML 更具可读性。 但是，前缀通常是只需使用的快捷方式的完整 XML 命名空间，并且不要求在大多数情况下。 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]通过将所有前缀都解析为其对应的 XML 命名空间，简化了 XML 名称。 前缀是可用的如果需要，通过这些<xref:System.Xml.Linq.XElement.GetPrefixOfNamespace%2A>方法。</xref:System.Xml.Linq.XElement.GetPrefixOfNamespace%2A>  
  
 如果有必要，可以控制命名空间前缀。 在某些情况下，如果使用的是其他 XML 系统（如 XSLT 或 XAML），则需要控制命名空间前缀。 例如，如果 XPath 表达式使用命名空间前缀且嵌入在 XSLT 样式表中，则将必须确保使用与 XPath 表达式中使用的前缀相匹配的命名空间前缀来序列化 XML 文档。  
  
### <a name="xnamespace-class"></a>XNamespace 类  
 <xref:System.Xml.Linq.XNamespace>表示一个命名空间<xref:System.Xml.Linq.XElement>或<xref:System.Xml.Linq.XAttribute>.</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XElement></xref:System.Xml.Linq.XNamespace> 命名空间是<xref:System.Xml.Linq.XName>。</xref:System.Xml.Linq.XName>的组件  
  
### <a name="xnode-class"></a>XNode 类  
 <xref:System.Xml.Linq.XNode>是一个抽象类表示 XML 树的节点。</xref:System.Xml.Linq.XNode> 下面的类派生自<xref:System.Xml.Linq.XNode>类︰</xref:System.Xml.Linq.XNode>  
  
-   <xref:System.Xml.Linq.XText></xref:System.Xml.Linq.XText>  
  
-   <xref:System.Xml.Linq.XContainer></xref:System.Xml.Linq.XContainer>  
  
-   <xref:System.Xml.Linq.XComment></xref:System.Xml.Linq.XComment>  
  
-   <xref:System.Xml.Linq.XProcessingInstruction></xref:System.Xml.Linq.XProcessingInstruction>  
  
-   <xref:System.Xml.Linq.XDocumentType></xref:System.Xml.Linq.XDocumentType>  
  
### <a name="xnodedocumentordercomparer-class"></a>XNodeDocumentOrderComparer 类  
 <xref:System.Xml.Linq.XNodeDocumentOrderComparer>提供用于比较节点文档顺序的功能。</xref:System.Xml.Linq.XNodeDocumentOrderComparer>  
  
### <a name="xnodeequalitycomparer-class"></a>XNodeEqualityComparer 类  
 <xref:System.Xml.Linq.XNodeEqualityComparer>提供用于比较节点值相等的功能。</xref:System.Xml.Linq.XNodeEqualityComparer>  
  
### <a name="xobject-class"></a>XObject 类  
 <xref:System.Xml.Linq.XObject>是一个抽象基类和<xref:System.Xml.Linq.XNode><xref:System.Xml.Linq.XAttribute>。</xref:System.Xml.Linq.XAttribute> </xref:System.Xml.Linq.XNode></xref:System.Xml.Linq.XObject> 它提供批注和事件功能。  
  
### <a name="xobjectchange-class"></a>XObjectChange 类  
 <xref:System.Xml.Linq.XObjectChange>以团队<xref:System.Xml.Linq.XObject>。</xref:System.Xml.Linq.XObject>引发事件时指定的事件类型</xref:System.Xml.Linq.XObjectChange>  
  
### <a name="xobjectchangeeventargs-class"></a>XObjectChangeEventArgs 类  
 <xref:System.Xml.Linq.XObjectChangeEventArgs>将提供数据供<xref:System.Xml.Linq.XObject.Changing>和<xref:System.Xml.Linq.XObject.Changed>事件。</xref:System.Xml.Linq.XObject.Changed> </xref:System.Xml.Linq.XObject.Changing></xref:System.Xml.Linq.XObjectChangeEventArgs>  
  
### <a name="xprocessinginstruction-class"></a>XProcessingInstruction 类  
 <xref:System.Xml.Linq.XProcessingInstruction>表示一个 XML 处理指令。</xref:System.Xml.Linq.XProcessingInstruction> 处理指令将信息传递给处理 XML 的应用程序。  
  
### <a name="xtext-class"></a>XText 类  
 <xref:System.Xml.Linq.XText>表示一个文本节点。</xref:System.Xml.Linq.XText> 多数情况下都不必使用此类。 此类主要用于混合内容。  
  
## <a name="see-also"></a>另请参阅  
 [LINQ to XML 编程概述 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)
