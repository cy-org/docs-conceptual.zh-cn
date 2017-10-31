---
title: "保留实体引用 | Microsoft Docs"
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
ms.assetid: 000a6cae-5972-40d6-bd6c-a9b7d9649b3c
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# 保留实体引用
当不扩展而是保留实体引用时，XML 文档对象模型 \(DOM\) 在遇到实体引用时生成 **XmlEntityReference** 节点。  
  
 使用以下 XML，  
  
```  
<author>Fred</author>  
<pubinfo>Published by &publisher;</pubinfo>  
```  
  
 DOM 在遇到 `&publisher;` 引用时生成 **XmlEntityReference** 节点。  **XmlEntityReference** 包含从实体声明的内容中复制的子节点。  前面的代码示例包含实体声明中的文本，因此创建 **XmlText** 节点作为实体引用节点的子节点。  
  
 ![保留的实体引用的树结构](../../../../docs/standard/data/xml/media/xmlentityref-notexpanded-nodes.gif "xmlentityref\_notexpanded\_nodes")  
保留的实体引用的树结构  
  
 **XmlEntityReference** 的子节点是在遇到实体声明时从 **XmlEntity** 节点创建的所有子节点的副本。  
  
> [!NOTE]
>  从 **XmlEntity** 中复制的节点并非始终是曾放置在实体引用节点下面的相同副本。  可以有在实体引用节点范围内并影响子节点的最终配置的命名空间。  
  
 默认情况下，保留常规实体（如 `&abc;`）并总是创建 **XmlEntityReference** 节点。  
  
## 请参阅  
 [XML 文档对象模型 \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)