---
title: "XML 文档对象模型 (DOM) 层次结构 | Microsoft Docs"
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
ms.assetid: 9d187d4f-c76e-4223-a670-cc290783ce47
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# XML 文档对象模型 (DOM) 层次结构
下图显示了 XML 文档对象模型 \(DOM\) 的类层次结构，其中万维网联合会 \(W3C\) 名称用括号括起来，另外还有相关的类名。  
  
 ![XML 文档对象模型 &#40;DOM&#41; 层次结构](../../../../docs/standard/data/xml/media/dom-class-hierarchy.gif "Dom\_class\_hierarchy")  
XML 文档对象模型 \(DOM\) 层次结构  
  
 下列类不从 **XmlNode** 继承：  
  
-   **XmlImplementation**  
  
-   **XmlNamedNodeMap**  
  
-   **XmlNodeList**  
  
-   **XmlNodeChangedEventArgs**  
  
 **XmlImplementation** 类用于创建 XML 文档。  有关更多信息，请参见 [XML 文档创建](../../../../docs/standard/data/xml/xml-document-creation.md)。  
  
 **XmlNamedNodeMap** 类处理未排序的节点集。  有关更多信息，请参见[按名称或索引检索未排序节点](../../../../docs/standard/data/xml/unordered-node-retrieval-by-name-or-index.md)。  
  
 **XmlNodeList** 类处理已排序的节点列表。  有关更多信息，请参见[按索引检索已排序节点](../../../../docs/standard/data/xml/ordered-node-retrieval-by-index.md)。  
  
 **XmlNodeChangedEventArgs** 类处理在 **XmlDocument** 上注册的事件处理程序。  有关更多信息，请参见[使用 XmlNodeChangedEventArgs 的 XML 文档中的事件处理](../../../../docs/standard/data/xml/event-handling-in-an-xml-document-using-the-xmlnodechangedeventargs.md)。  
  
 **XmlLinkedNode** 类从 **XmlNode** 继承。  其目的是重写 **XmlNode** 中的两个方法：**PreviousSibling** 和 **NextSibling** 方法。  然后，这些重写方法由具有上一个和下一个同辈的类 **XmlCharacterData**、**XmlDeclaration**、**XmlDocumentType**、**XmlElement**、**XmlEntityReference** 和 **XmlProcessingInstruction** 继承和使用。  
  
## 请参阅  
 [XML 文档对象模型 \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)