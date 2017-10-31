---
title: "在 DOM 中创建新节点 | Microsoft Docs"
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
ms.assetid: 6c2b9789-b61a-49f9-b33f-db01a945edf2
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# 在 DOM 中创建新节点
<xref:System.Xml.XmlDocument>具有的所有节点类型的创建方法。 为该方法提供名称（需要时）以及那些具有内容的节点（如文本节点）的内容或其他参数，这样便可创建节点。 下面的方法需要填充名称和几个其他参数以创建相应的节点。  
  
-   <xref:System.Xml.XmlDocument.CreateCDataSection%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateComment%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateDocumentFragment%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateDocumentType%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateElement%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateNode%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateProcessingInstruction%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateSignificantWhitespace%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateTextNode%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateWhitespace%2A>  
  
-   <xref:System.Xml.XmlDocument.CreateXmlDeclaration%2A>  
  
 其他节点类型不仅仅只要求向参数提供数据。  
  
 属性的信息，请参阅[为 DOM 中的元素创建新属性](../../../../docs/standard/data/xml/creating-new-attributes-for-elements-in-the-dom.md)。 元素和属性名验证的信息，请参阅[XML 元素和属性名验证时创建新节点](../../../../docs/standard/data/xml/xml-element-and-attribute-name-verification-when-creating-new-nodes.md)。 有关如何创建实体引用，请参阅[创建新实体引用](../../../../docs/standard/data/xml/creating-new-entity-references.md)。 命名空间如何影响实体引用扩展的信息，请参阅[对实体引用扩展的新节点包含元素和属性的 Namespace 影响](../../../../docs/standard/data/xml/namespace-affect-on-entity-ref-expansion-for-new-nodes.md)。  
  
 创建新节点后，有几个方法可用于将其插入到树中。 下表列出了这些方法，并描述了新节点在 XML 文档对象模型 (DOM) 中的位置。  
  
|方法|节点位置|  
|------------|--------------------|  
|<xref:System.Xml.XmlNode.InsertBefore%2A>|插入到引用节点之前。 例如，在位置 5 插入新节点：<br /><br /> `Dim refChild As XmlNode = node.ChildNodes(4) 'The reference is zero-based.node.InsertBefore(newChild, refChild);`<br /><br /> `XmlNode refChild = node.ChildNodes[4]; //The reference is zero-based. node.InsertBefore(newChild, refChild);`<br /><br /> 有关详细信息，请参阅<xref:System.Xml.XmlNode.InsertBefore%2A>方法。|  
|<xref:System.Xml.XmlNode.InsertAfter%2A>|插入到引用节点之后。 例如：<br /><br /> `node.InsertAfter(newChild, refChild)`<br /><br /> `node.InsertAfter(newChild, refChild);`<br /><br /> 有关详细信息，请参阅<xref:System.Xml.XmlNode.InsertAfter%2A>方法。|  
|<xref:System.Xml.XmlNode.AppendChild%2A>|将节点添加到给定节点的子节点列表的末尾。 如果所添加的节点是<xref:System.Xml.XmlDocumentFragment>，将文档片段的全部内容移至该节点的子列表。 有关详细信息，请参阅<xref:System.Xml.XmlNode.AppendChild%2A>方法。|  
|<xref:System.Xml.XmlNode.PrependChild%2A>|将节点添加到给定节点的子节点列表的开头。 如果所添加的节点是<xref:System.Xml.XmlDocumentFragment>，将文档片段的全部内容移至该节点的子列表。 有关详细信息，请参阅<xref:System.Xml.XmlNode.PrependChild%2A>方法。|  
|<xref:System.Xml.XmlAttributeCollection.Append%2A>|追加<xref:System.Xml.XmlAttribute>节点到与元素关联的属性集合的末尾。 有关详细信息，请参阅<xref:System.Xml.XmlAttributeCollection.Append%2A>方法。|  
  
## <a name="see-also"></a>另请参阅  
 [XML 文档对象模型 (DOM)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)