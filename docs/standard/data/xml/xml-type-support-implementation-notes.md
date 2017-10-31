---
title: "XML 类型支持实现说明 | Microsoft Docs"
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
ms.assetid: 26b071f3-1261-47ef-8690-0717f5cd93c1
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# XML 类型支持实现说明
本主题介绍一些要注意的实现细节。  
  
## 列表映射  
 <xref:System.Collections.IList>、<xref:System.Collections.ICollection>、<xref:System.Collections.IEnumerable>、**Type\[\]** 和 <xref:System.String> 类型用于表示 XML 架构定义语言 \(XSD\) 的列表类型。  
  
## 联合映射  
 联合类型使用 <xref:System.Xml.Schema.XmlAtomicValue> 或 <xref:System.String> 类型表示。  因此，源类型或目标类型必须始终为 <xref:System.String> 或 <xref:System.Xml.Schema.XmlAtomicValue>。  
  
 如果 <xref:System.Xml.Schema.XmlSchemaDatatype> 对象表示列表类型，该对象会将输入字符串值转换为一个或多个对象的列表。  如果 <xref:System.Xml.Schema.XmlSchemaDatatype> 表示联合类型，则尝试将输入值作为联合的成员类型进行分析。  如果尝试分析失败，将尝试使用联合的下一个成员进行转换，依此类推，直到转换成功，或没有其他成员类型可以尝试，在这种情况下将引发异常。  
  
## CLR 和 XML 数据类型之间的区别  
 下文介绍 CLR 类型和 XML 数据类型之间可能发生的某些不匹配情况以及如何处理这些情况。  
  
> [!NOTE]
>  `xs` 前缀映射到 http:\/\/www.w3.org\/2001\/XMLSchema 和命名空间 URI。  
  
### System.TimeSpan 和 xs:duration  
 `xs:duration` 类型进行部分排序，因为存在某些不同但是等效的持续时间值。  这意味着对于 `xs:duration` 类型，1 个月 \(P1M\) 之类的值少于 32 天 \(P32D\)，多于 27 天 \(P27D\)，等效于 28、29 或 30 天。  
  
 <xref:System.TimeSpan> 类不支持此部分排序。  而是为 1 年和 1 个月选取特定的天数；分别为 365 天和 30 天。  
  
 有关 `xs:duration` 类型的更多信息，请参见“W3C XML Schema Part 2: Datatypes Recommendation”（W3C XML 架构第 2 部分：数据类型建议），其网址为：http:\/\/www.w3.org\/TR\/xmlschema\-2\/。  
  
### xs:time、公历数据类型和 System.DateTime  
 `xs:time` 值映射到 <xref:System.DateTime> 对象时，<xref:System.DateTime.MinValue> 字段用于将 <xref:System.DateTime> 对象的日期属性（例如 <xref:System.DateTime.Year%2A>、<xref:System.DateTime.Month%2A> 和 <xref:System.DateTime.Day%2A>）初始化为 <xref:System.DateTime> 可能的最小值。  
  
 同样，`xs:gMonth`、`xs:gDay`、`xs:gYear`、`xs:gYearMonth` 和 `xs:gMonthDay` 的实例也映射到 <xref:System.DateTime> 对象。  <xref:System.DateTime> 对象上未使用的属性初始化为 <xref:System.DateTime.MinValue> 中的值。  
  
> [!NOTE]
>  如果内容类型化为 `xs:gMonthDay`，则不能使用 <xref:System.DateTime.Year%2A?displayProperty=fullName> 值。  在这种情况下，<xref:System.DateTime.Year%2A?displayProperty=fullName> 值始终设置为 1904。  
  
### xs:anyURI 和 System.Uri  
 表示相对 URI 的 `xs:anyURI` 的实例映射到 <xref:System.Uri> 时，<xref:System.Uri> 对象没有基 URI。  
  
## 请参阅  
 [System.Xml 类中的类型支持](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)