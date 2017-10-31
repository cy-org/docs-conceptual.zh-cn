---
title: "创建新实体引用 | Microsoft Docs"
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
ms.assetid: a42f81b3-0403-4e34-b346-7d2129804e54
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# 创建新实体引用
**CreateEntityReference** 方法创建新的 **XmlEntityReference** 节点。  XML 文档对象模型 \(DOM\) 查看是否已声明了引用的实体名称。  如果已声明，则从实体声明节点复制 **XmlEntityReference** 节点的子节点。  如果没有匹配的实体声明，则附加一个空的文本节点作为实体引用节点的唯一子级。  由于 **XmlEntityReference** 节点的子节点是其他节点的副本，因此这些子节点是只读的，无法修改。  
  
 当复制节点时，在实体引用所处的范围内可能存在一个命名空间。  此命名空间影响生成的任何元素或属性节点的配置。  
  
> [!NOTE]
>  仅当将 **EntityReference** 节点插入到文档中时，DOM 才将子节点添加到 **EntityReference**。  新创建的 **EntityReference** 节点没有子节点。  
  
 尽管 **XmlDataDocument** 是 **XmlDocument** 的派生类，但 **XmlDataDocument** 不支持实体引用的创建。  这是因为 **EntityReference** 子级是只读的。  **EntityReference** 节点的子级可以跨一个以上的区域。  在这种情况下，行中与包含 **EntityReference** 一部分的区域关联的部分将是只读的。  
  
## 请参阅  
 [XML 文档对象模型 \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)