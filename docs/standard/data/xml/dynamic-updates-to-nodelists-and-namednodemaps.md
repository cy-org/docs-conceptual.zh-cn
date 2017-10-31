---
title: "NodeList 和 NamedNodeMap 的动态更新 | Microsoft Docs"
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
ms.assetid: 76c511fd-6704-4ca4-8078-860a68d898ad
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# NodeList 和 NamedNodeMap 的动态更新
由于 **XmlNodeList** 和 **XmlNamedNodeMap** 包含节点集，而 XML 文档加载到内存中并被修改，因此万维网联合会 \(W3C\) 规定这些包含节点集的对象应是动态的。  也就是说，如果基础文档更改，则这两个对象中的数据也应更改。  因此，如果您的 **XmlNodeList** 包含特定元素（例如元素 X）的所有子元素，然后您在文档中的元素 X 下添加了另外一个元素 Q。  **XmlNodeList** 也应将新元素 Q 添加到其集合中。  反过来也一样。  如果将节点添加到 **XmlNodeList**，则基础文档同样也更新。  
  
## 请参阅  
 [XML 文档对象模型 \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)