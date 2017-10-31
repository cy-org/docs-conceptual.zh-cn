---
title: "加载 DOM 时的空白和有效空白处理 | Microsoft Docs"
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
ms.assetid: 1b141a0a-50d8-4ebd-83cd-a84449bb22b2
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# 加载 DOM 时的空白和有效空白处理
加载文档时，可以设置保留空白并在文档树中创建 **XmlWhitespace** 节点的选项。  若要创建空白节点，请将 **PreserveWhitespace** 属性设置为 true。  如果此属性设置为默认值 **false**，则不创建空白节点。  总是保留有效空白节点，并且总是在内存中创建 **XmlSignificantWhitespace** 节点以表示此数据，与 **PreserveWhitespace** 标志的设置无关。  
  
 如果文档从读取器加载，只有 **XmlTextReader** 上的 **WhitespaceHandling** 属性未设置为 **WhitespaceHandling.None** 时，**XmlDocument** 类上 **PreserveWhitespace** 标志属性的设置才会影响 **XmlWhitespace** 节点的创建，  读取器上 **WhitespaceHandling** 属性的值优先于 **XmlDocument** 上该标志的设置。  有关 **XmlSignificantWhitespace** 的更多信息，请参见 [XmlSignificantWhitespace 类](frlrfSystemXmlXmlSignificantWhitespaceClassTopic)。  
  
## 请参阅  
 [XML 文档对象模型 \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)