---
title: "复制现有节点 | Microsoft Docs"
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
ms.assetid: 2aa8f65c-cc62-4638-9c46-129dc15be786
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# 复制现有节点
XML 文档对象模型 \(DOM\) 中有许多方法和属性可用来选择节点，如 **SelectSingleNode**、**ChildNodes\[int i\]**、**Attributes\[int i\]**。  选择节点后，可以使用适用于特定节点类型的插入方法之一将该节点插入到树中。  将节点插入到树中的唯一限制是在插入节点后文档的格式仍必须是正确的。  将现有节点插入到 DOM 树中时，该节点从其原始位置移除并添加到它的目标位置。  
  
## 请参阅  
 [XML 文档对象模型 \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)