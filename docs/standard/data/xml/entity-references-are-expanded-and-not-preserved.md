---
title: "扩展但不保留实体引用 | Microsoft Docs"
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
ms.assetid: ffd97806-ab43-4538-8de2-5828bfbbde57
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# 扩展但不保留实体引用
当扩展实体引用并用其表示的文本替换该实体引用时，将不创建 **XmlEntityReference** 节点。  相反，将分析实体声明并复制从声明中的内容创建的节点以取代 **XmlEntityReference**。  因此，在 `&publisher;` 示例中，不保存 `&publisher;` 而是创建 **XmlText** 节点。  
  
 ![展开的树结构](../../../../docs/standard/data/xml/media/xmlentityref-expanded-nodes.png "xmlentityref\_expanded\_nodes")  
扩展的实体引用的树结构  
  
 不保留 `B` 或 `<` 这类字符实体。  相反，它们总是扩展并表示为文本节点。  
  
 若要保留 **XmlEntityReference** 节点以及附加到该节点的实体引用的子节点，请将 **EntityHandling** 标志设置为 **ExpandCharEntities**。  否则，使 **EntityHandling** 标志保持为默认设置（即 **ExpandEntities**）。  这种情况下，您在 DOM 中将看不到实体引用节点。  这些节点已被作为实体声明子节点副本的节点取代。  
  
 不保留实体引用的一个副作用是，当保存文档并将其传递给另一个应用程序时，接收应用程序不知道这些节点是由实体引用生成的。  然而，当保留实体引用时，接收应用程序将查看实体引用并读取子节点。  显而易见，这些子节点表示实体声明中的信息。  例如，在保留实体引用的情况下，DOM 理论上包含以下结构。  
  
 XmlElement：发布者  
  
 XmlEntityReference：`&publisher;`  
  
 XmlText：Microsoft Press  
  
 如果在 DOM 中扩展实体引用（这是默认方法），则结构包含此类型树：  
  
 XmlElement：发布者  
  
 XmlText：Microsoft Press  
  
 注意，实体引用节点已消失，接收应用程序无法断定包含“Microsoft Press”的 **XmlText** 节点是不是从实体声明创建的。  
  
 如果使用无法解析实体的读取器，则 **Load** 方法在遇到实体引用时将引发异常。  
  
## 请参阅  
 [XML 文档对象模型 \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)