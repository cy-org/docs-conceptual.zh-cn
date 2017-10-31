---
title: "XPath 查询识别的节点类型 | Microsoft Docs"
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
ms.assetid: 1d33e22d-18e5-43f8-a466-2e3d0a8dd094
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# XPath 查询识别的节点类型
XPath 查询识别的节点类型与文档对象模型 \(DOM\) 中的节点类型不同。  
  
## W3C XPath 节点类型  
 XPath 查询识别的节点类型与文档对象模型 \(DOM\) 中的节点类型不同。  以下是通过 <xref:System.Xml.XPath.XPathNodeType> 枚举表示的 XPath 节点类型。  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
-   <xref:System.Xml.XPath.XPathNodeType>  
  
 这些节点类型基于 XPath 数据模型，其中的节点从 XML 信息集派生。  <xref:System.Xml.XPath.XPathNodeType> 和 <xref:System.Xml.XPath.XPathNodeType> 节点类型是 Microsoft .NET Framework 对 XPath 数据模型中所述的基本节点类型的扩展。  
  
 属性节点类型在 XPath 数据模型中的用法与在 DOM 中的用法不同。  在 XPath 数据模型中，元素具有相关的属性节点集，且元素是每个属性节点的父级。  但在 DOM 中，元素节点是所有者，而不是父级。  在这两种模型中，属性和命名空间节点都不被视为元素节点的子节点。  
  
 命名空间节点类型是 XPath 数据模型的补充，并且不是可识别的 DOM 节点类型。  
  
 有关浏览元素的更多信息，请参见[使用 XPathNavigator 的节点集定位](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md)和[使用 XPathNavigator 的属性和命名空间节点定位](../../../../docs/standard/data/xml/attribute-and-namespace-node-navigation-using-xpathnavigator.md)。  
  
## 请参阅  
 <xref:System.Xml.XmlDocument>   
 <xref:System.Xml.XPath.XPathDocument>   
 <xref:System.Xml.XPath.XPathNavigator>   
 [使用 XPath 数据模型处理 XML 数据](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)   
 [使用 XPathNavigator 选择 XML 数据](../../../../docs/standard/data/xml/select-xml-data-using-xpathnavigator.md)   
 [使用 XPathNavigator 计算 XPath 表达式](../../../../docs/standard/data/xml/evaluate-xpath-expressions-using-xpathnavigator.md)   
 [使用 XPathNavigator 匹配节点](../../../../docs/standard/data/xml/matching-nodes-using-xpathnavigator.md)   
 [XPath 查询和命名空间](../../../../docs/standard/data/xml/xpath-queries-and-namespaces.md)   
 [已编译的 XPath 表达式](../../../../docs/standard/data/xml/compiled-xpath-expressions.md)