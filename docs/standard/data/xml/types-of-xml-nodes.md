---
title: "XML 节点类型 | Microsoft Docs"
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
ms.assetid: 71d03b78-6898-4ce7-b0fc-1282573f31f7
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# XML 节点类型
当将 XML 文档作为节点树读入内存时，这些节点的节点类型在创建节点时确定。  XML 文档对象模型 \(DOM\) 具有多种节点类型，这些类型由万维网联合会 \(W3C\) 确定并在 1.1.1 节“The DOM Structure Model”中列出。  下表列出了节点类型、分配给该节点类型的对象以及每种节点类型的简短说明。  
  
|DOM 节点类型|对象|描述|  
|--------------|--------|--------|  
|Document|[XmlDocument 类](frlrfSystemXmlXmlDocumentClassTopic)|树中所有节点的容器。  它也称作文档根，文档根并非总是与根元素相同。|  
|DocumentFragment|[XmlDocumentFragment 类](frlrfSystemXmlXmlDocumentFragmentClassTopic)|包含一个或多个不带任何树结构的节点的临时袋。|  
|DocumentType|[XmlDocumentType 类](frlrfSystemXmlXmlDocumentTypeClassTopic)|表示 `<!DOCTYPE >` 节点。|  
|EntityReference|[XmlEntityReference 类](frlrfSystemXmlXmlEntityReferenceClassTopic)|表示非扩展的实体引用文本。|  
|元素|[XmlElement 类](frlrfSystemXmlXmlElementClassTopic)|表示元素节点。|  
|Attr|[XmlAttribute 类](frlrfSystemXmlXmlAttributeClassTopic)|为元素的属性。|  
|ProcessingInstruction|[XmlProcessingInstruction 类](frlrfSystemXmlXmlProcessingInstructionClassTopic)|为处理指令节点。|  
|注释|[XmlComment 类](frlrfSystemXmlXmlCommentClassTopic)|注释节点。|  
|Text|[XmlText 类](frlrfSystemXmlXmlTextClassTopic)|属于某个元素或属性的文本。|  
|CDATASection|[XmlCDataSection 类](frlrfSystemXmlXmlCDataSectionClassTopic)|表示 CDATA。|  
|实体|[XmlEntity 类](frlrfSystemXmlXmlEntityClassTopic)|表示 XML 文档（来自内部文档类型定义 \(DTD\) 子集或来自外部 DTD 和参数实体）中的 `<!ENTITY >` 声明。|  
|Notation|[XmlNotation 类](frlrfSystemXmlXmlNotationClassTopic)|表示 DTD 中声明的表示法。|  
  
 尽管属性 \(*attr*\) 在 W3C DOM 级别 1 的 1.2 节“Fundamental Interfaces”中作为节点列出，但不能将其视为任何元素节点的子级。  
  
 下表显示了 W3C 未定义的其他节点类型，但这些类型可作为 **XmlNodeType** 枚举在 Microsoft .NET Framework 对象模型中使用。  因此，这些节点类型不存在匹配的 DOM 节点类型列。  
  
|节点类型|描述|  
|----------|--------|  
|<xref:System.Xml.XmlDeclaration>|表示声明节点 `<?xml version="1.0" >`。|  
|<xref:System.Xml.XmlSignificantWhitespace>|表示有效空白（混合内容中的空白）。|  
|<xref:System.Xml.XmlWhitespace>|表示元素内容中的空白。|  
|EndElement|当 **XmlReader** 到达元素的末尾时返回。<br /><br /> 示例 XML：**\<\/item\>**<br /><br /> 有关更多信息，请参见 [XmlNodeType 枚举](frlrfSystemXmlXmlNodeTypeClassTopic)。|  
|EndEntity|当 **XmlReader** 由于调用 <xref:System.Xml.XmlReader.ResolveEntity%2A> 而到达实体替换的末尾时返回。  有关更多信息，请参见 [XmlNodeType 枚举](frlrfSystemXmlXmlNodeTypeClassTopic)。|  
  
 若要查看读入 XML 并对节点类型使用 case 构造以打印有关节点及其内容的信息的代码示例，请参见 [XmlSignificantWhitespace.NodeType 属性](frlrfSystemXmlXmlSignificantWhitespaceClassNodeTypeTopic)。  
  
 有关节点类型及其等效对象名的对象层次结构的更多信息，请参见 [XML 文档对象模型 \(DOM\) 层次结构](../../../../docs/standard/data/xml/xml-document-object-model-dom-hierarchy.md)。  有关在节点树中创建的对象的更多信息，请参见[将对象层次结构映射到 XML 数据](../../../../docs/standard/data/xml/mapping-the-object-hierarchy-to-xml-data.md)。  
  
## 请参阅  
 [XML 文档对象模型 \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)