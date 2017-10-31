---
title: "使用 XslCompiledTransform 类 | Microsoft Docs"
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
ms.assetid: f9b074f6-d6f4-49dd-a093-df510bf0cf7b
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# 使用 XslCompiledTransform 类
<xref:System.Xml.Xsl.XslCompiledTransform> 类是 Microsoft .NET Framework XSLT 处理器。  此类用于编译样式表并执行 XSLT 转换。  
  
> [!NOTE]
>  尽管 <xref:System.Xml.Xsl.XslCompiledTransform> 类的总体性能优于 <xref:System.Xml.Xsl.XslTransform> 类，但在首次对转换调用时，<xref:System.Xml.Xsl.XslCompiledTransform> 类的 <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> 方法可能比 <xref:System.Xml.Xsl.XslTransform> 类的 <xref:System.Xml.Xsl.XslTransform.Load%2A> 方法慢。  这是因为必须先编译 XSLT 文件，才能加载该文件。  有关更多信息，请参见以下博客帖子：[XslCompiledTransform 比 XslTransform 慢？](http://go.microsoft.com/fwlink/?LinkId=130590)（可能为英文网页）  
  
## 本节内容  
 [XslCompiledTransform 类的输入](../../../../docs/standard/data/xml/inputs-to-the-xslcompiledtransform-class.md)  
 介绍可用的 XSLT 输入选项。  
  
 [XslCompiledTransform 类的输出选项](../../../../docs/standard/data/xml/output-options-on-the-xslcompiledtransform-class.md)  
 介绍可用的 XSLT 输出选项。  
  
 [在 XSLT 处理期间解析外部资源](../../../../docs/standard/data/xml/resolving-external-resources-during-xslt-processing.md)  
 讨论如何使用 <xref:System.Xml.XmlResolver> 类解析外部资源。  
  
 [扩展 XSLT 样式表](../../../../docs/standard/data/xml/extending-xslt-style-sheets.md)  
 讨论如何支持 XSLT 扩展。  
  
|||  
|-|-|  
|[可恢复的 XSLT 错误](../../../../docs/standard/data/xml/recoverable-xslt-errors.md)|列出万维网联合会 \(W3C\) XSLT 1.0 建议所允许的任意行为，并介绍如何通过 <xref:System.Xml.Xsl.XslCompiledTransform> 类处理这些行为。|  
|[如何：转换节点片断](../../../../docs/standard/data/xml/how-to-transform-a-node-fragment.md)|介绍如何转换节点片断。|  
  
## 相关章节  
 [从 XslTransform 类迁移](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)  
 讨论如何从 <xref:System.Xml.Xsl.XslTransform> 类迁移代码。  
  
## 请参阅  
 <xref:System.Xml.Xsl.XsltSettings>   
 <xref:System.Xml.Xsl.XsltMessageEncounteredEventArgs>