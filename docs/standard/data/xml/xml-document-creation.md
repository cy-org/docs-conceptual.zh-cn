---
title: "XML 文档创建 | Microsoft Docs"
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
ms.assetid: 877e9c62-b082-4bfb-bc5b-f47297eb30ef
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# XML 文档创建
有两种创建 XML 文档的方法。  一种方法是创建不带参数的 **XmlDocument**。  另一种方法是创建一个 **XmlDocument** 并将 XmlNameTable 作为参数传递给它。  下面的示例显示如何不使用任何参数创建一个新的空 **XmlDocument**。  
  
```vb  
Dim doc As New XmlDocument()  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
```  
  
 创建文档后，可通过 **Load** 方法从字符串、流、URL、文本读取器或 **XmlReader** 派生类为该文档加载数据。  还有另一种加载方法，即 **LoadXML** 方法，此方法从字符串中读取 XML。  有关各种 **Load** 方法的更多信息，请参见[将 XML 文档读入 DOM](../../../../docs/standard/data/xml/reading-an-xml-document-into-the-dom.md)。  
  
 有一个名为 **XmlNameTable** 的类。  此类是原子化字符串对象的表。  该表使 XML 分析器可以高效地对 XML 文档中所有重复的元素和属性的名称使用相同的字符串对象。  创建文档时（如上所示），将自动创建 **XmlNameTable**，并在加载此文档时加载属性和元素的名称。  如果已经有一个包含名称表的文档，且这些名称在另一个文档中会很有用，则可使用接受 **XmlNameTable** 参数的 **Load** 方法创建一个新文档。  使用此方法创建文档后，该文档使用现有 **XmlNameTable**，后者包含所有已从其他文档加载到此文档中的属性和元素。  它可用于有效地比较元素和属性的名称。  有关 **XmlNameTable** 的更多信息，请参见[使用 XmlNameTable 比较对象](../../../../docs/standard/data/xml/object-comparison-using-xmlnametable.md)。  有关参考，请参见 [XmlNameTable 成员](frlrfSystemXmlXmlNameTableMembersTopic)。  
  
## 请参阅  
 [XML 文档对象模型 \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)