---
title: "XSLT 转换 | Microsoft Docs"
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
ms.assetid: 202f8820-224c-494f-b61e-cd127eac6e03
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# XSLT 转换
可扩展样式表语言转换 \(XSLT\) 可以将源 XML 文档的内容转换为另一个格式或结构不同的文档。  例如，可以使用 XSLT 将 XML 转换为在网站上使用的 HTML 或转换为只包含应用程序所需字段的文档。  此转换过程由 [W3C XSL 转换 \(XSLT\) 1.0 版建议](http://go.microsoft.com/fwlink/?LinkID=49919)指定。  
  
 <xref:System.Xml.Xsl.XslCompiledTransform> 类是 .NET Framework 中的 XSLT 处理器。  <xref:System.Xml.Xsl.XslCompiledTransform> 类支持 W3C XSLT 1.0 建议。  
  
> [!NOTE]
>  <xref:System.Xml.Xsl.XslTransform> 类在 .NET Framework 2.0 版中已过时。  <xref:System.Xml.Xsl.XslCompiledTransform> 类是 XSLT 引擎的新实现。  它包括性能改进和新的安全功能。  建议的做法是使用 <xref:System.Xml.Xsl.XslCompiledTransform> 类创建 XSLT 应用程序。  
  
## 本节内容  
 [使用 XslCompiledTransform 类](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md)  
 提供如何使用 <xref:System.Xml.Xsl.XslCompiledTransform> 类的信息。  
  
 [从 XslTransform 类迁移](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)  
 讨论如何从 <xref:System.Xml.Xsl.XslTransform> 类迁移代码。  
  
 [XSLT 编译器 \(xsltc.exe\)](../../../../docs/standard/data/xml/xslt-compiler-xsltc-exe.md)  
 提供有关如何使用 XSLT 编译器的信息。  
  
 [XslTransform 类的 XSLT 转换](../../../../docs/standard/data/xml/xslt-transformations-with-the-xsltransform-class.md)  
 提供如何使用 <xref:System.Xml.Xsl.XslTransform> 类的信息。  
  
 **注意** <xref:System.Xml.Xsl.XslTransform> 类在 .NET Framework 2.0 版中已过期。  
  
## 参考  
 <xref:System.Xml.Xsl.XslCompiledTransform>  
  
 <xref:System.Xml.Xsl.XsltArgumentList>  
  
 <xref:System.Xml.Xsl.XsltSettings>  
  
## 相关章节  
 [XML 文档和数据](../../../../docs/standard/data/xml/index.md)