---
title: "NamedNodeMap 和 NodeList 中的节点集合 | Microsoft Docs"
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
ms.assetid: 025954b8-7aa8-47c5-a1c1-f81064fb4d65
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# NamedNodeMap 和 NodeList 中的节点集合
可以检索节点集并将其放在已排序或未排序的集合中。  将节点集放在未排序的集合中时，万维网联合会 \(W3C\) 将此节点集称为 NamedNodeMap；在这种类型的集合中可以按名称或索引检索数据。  将节点集放入已排序的集合中时，W3C 将其称为 NodeList；可以按从零开始的索引检索数据。  NamedNodeMap 和 NodeList 由 W3C 描述。  NamedNodeMap 在 Microsoft .NET Framework 中的实现为 **XmlNamedNodeMap**，而 NodeList 由 **XmlNodeList** 实现。  
  
 有关未排序集合的信息，请参见[按名称或索引检索未排序节点](../../../../docs/standard/data/xml/unordered-node-retrieval-by-name-or-index.md)。  有关已排序集合的信息，请参见[按索引检索已排序节点](../../../../docs/standard/data/xml/ordered-node-retrieval-by-index.md)。  
  
## 请参阅  
 [XML 文档对象模型 \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)