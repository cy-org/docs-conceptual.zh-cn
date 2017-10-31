---
title: "System.Xml 类中的类型支持 | Microsoft Docs"
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
ms.assetid: 63570538-06e3-4401-ad4d-ac50be90c7bf
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# System.Xml 类中的类型支持
在 .NET Framework 2.0 版中，核心 XML 类已得到增强，具有类型支持功能。  <xref:System.Xml.XmlReader>、<xref:System.Xml.XmlWriter> 和 <xref:System.Xml.XPath.XPathNavigator> 类具有类型支持功能，可以在 XML 架构类型和公共语言运行库 \(CLR\) 类型之间转换。  
  
 在 .NET Framework 2.0 版中，<xref:System.Xml.XmlReader>、<xref:System.Xml.XmlWriter> 和 <xref:System.Xml.XPath.XPathNavigator> 类已得到增强，具有类型支持功能。  
  
-   <xref:System.Xml.XmlReader> 和 <xref:System.Xml.XPath.XPathNavigator> 类均具有 **SchemaInfo** 属性，返回节点的架构信息。  
  
-   **ReadContentAs** 和 **ReadElementContentAs** 以及 <xref:System.Xml.XmlReader> 类的方法在单个方法调用中读取文本值并将其转换为 CLR 值。  
  
-   在写出 XML 时，<xref:System.Xml.XmlWriter> 类的 <xref:System.Xml.XmlWriter.WriteValue%2A> 方法将 CLR 类型转换为 XML 架构类型。  
  
-   <xref:System.Xml.XPath.XPathNavigator> 类的 **ValueAs** 和 <xref:System.Xml.XPath.XPathNavigator.TypedValue%2A> 属性在单个方法调用中返回节点值并将其转换为 CLR 值。  
  
> [!NOTE]
>  在 .NET Framework 1.0 版中，需要使用 <xref:System.Xml.XmlConvert> 类在 XML 架构和 CLR 类型之间进行转换。  
  
## 本节内容  
 [将 XML 数据类型映射到 CLR 类型](../../../../docs/standard/data/xml/mapping-xml-data-types-to-clr-types.md)  
 介绍 XML 数据类型与 CLR 类型的默认映射。  
  
 [XML 类型支持实现说明](../../../../docs/standard/data/xml/xml-type-support-implementation-notes.md)  
 介绍一些类型支持实现的详细信息。  
  
 [XML 数据类型的转换](../../../../docs/standard/data/xml/conversion-of-xml-data-types.md)  
 描述如何使用 <xref:System.Xml.XmlConvert> 类在 XML 架构和 CLR 类型之间进行转换。  
  
## 相关章节  
 [使用 XPathNavigator 访问强类型 XML 数据](../../../../docs/standard/data/xml/accessing-strongly-typed-xml-data-using-xpathnavigator.md)