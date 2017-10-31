---
title: "System.Xml 使用情况 | Microsoft Docs"
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
ms.assetid: 82302f0d-a621-4c6f-b57d-999bd61f21a6
caps.latest.revision: 4
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 4
---
# System.Xml 使用情况
本部分将介绍几种类型中驻留的使用情况 <xref:System.Xml?displayProperty=fullName> 可以用于表示 XML 数据的命名空间。  
  
 **X 不** 使用 <xref:System.Xml.XmlNode> 或 <xref:System.Xml.XmlDocument> 来表示 XML 数据。 倾向于使用的实例 <xref:System.Xml.XPath.IXPathNavigable>, ，<xref:System.Xml.XmlReader>, ，<xref:System.Xml.XmlWriter>, ，或子类型 <xref:System.Xml.Linq.XNode> 相反。`XmlNode` 和 `XmlDocument` 不适用于公共 Api 中公开。  
  
 **✓ 执行** 使用 `XmlReader`, ，`IXPathNavigable`, ，或子类型 `XNode` 作为输入或输出的接受或返回 XML 的成员。  
  
 使用而不是这些抽象 `XmlDocument`, ，`XmlNode`, ，或 <xref:System.Xml.XPath.XPathDocument>, ，因为这将从内存中 XML 文档的特定实现的方法分离开来，使他们能够使用虚拟公开的 XML 数据源 `XNode`, ，`XmlReader`, ，或 <xref:System.Xml.XPath.XPathNavigator>。  
  
 **X 不** 子类 `XmlDocument` 如果想要创建表示基础对象模型或数据源的 XML 视图的类型。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [使用准则](../../../docs/standard/design-guidelines/usage-guidelines.md)