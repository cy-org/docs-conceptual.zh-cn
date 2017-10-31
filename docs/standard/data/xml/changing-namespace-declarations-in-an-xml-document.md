---
title: "更改 XML 文档中的命名空间声明 | Microsoft Docs"
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
ms.assetid: a2758f40-e497-4964-8d8d-1bb68af14dcd
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# 更改 XML 文档中的命名空间声明
**XmlDocument** 将命名空间声明和 **xmlns** 属性公开为文档对象模型的一部分。  这些声明和属性存储在 **XmlDocument** 中，因此当保存文档时，可以保留这些属性的位置。  更改这些属性对树中现有的其他节点的 **Name**、**NamespaceURI** 和 **Prefix** 属性没有影响。  例如，如果加载以下文档，`test` 元素将具有 **NamespaceURI** `123.`  
  
```  
<test xmlns="123"/>  
```  
  
 如果如下所示移除 `xmlns` 属性，`test` 元素仍具有 **NamespaceURI** `123`。  
  
```vb  
doc.documentElement.RemoveAttribute("xmlns")  
```  
  
```csharp  
doc.documentElement.RemoveAttribute("xmlns");  
```  
  
 同样，如果如下所示将不同的 `xmlns` 属性添加到 `doc` 元素，`test` 元素仍具有 **NamespaceURI** `123`。  
  
```vb  
doc.documentElement.SetAttribute("xmlns","456");  
```  
  
```csharp  
doc.documentElement.SetAttribute("xmlns","456");  
```  
  
 因此，更改 `xmlns` 属性不会有任何影响，直到保存并重新加载 **XmlDocument** 对象。  
  
## 请参阅  
 [XML 文档对象模型 \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)