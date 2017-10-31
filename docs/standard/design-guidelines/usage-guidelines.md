---
title: "使用准则 | Microsoft Docs"
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
helpviewer_keywords: 
  - "类库设计准则 [.NET Framework] 使用准则"
ms.assetid: 42215ffa-a099-4a26-b14e-fb2bdb6f95b7
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# 使用准则
本部分包含在可公开访问的 Api 中使用公共类型的指导原则。 它处理的内置框架类型 （例如，序列化属性） 和重载常用运算符直接使用。  
  
 <xref:System.IDisposable?displayProperty=fullName> 接口在此部分中，不会对其进行介绍，但在讨论 [释放模式](../../../docs/standard/design-guidelines/dispose-pattern.md) 部分。  
  
> [!NOTE]
>  指南和其他常见有关其他信息，内置的.NET Framework 类型，请参阅下面的参考主题︰ <xref:System.DateTime?displayProperty=fullName>, ，<xref:System.DateTimeOffset?displayProperty=fullName>, ，<xref:System.ICloneable?displayProperty=fullName>, ，<xref:System.IComparable%601?displayProperty=fullName>, ，<xref:System.IEquatable%601?displayProperty=fullName>, ，<xref:System.Nullable%601?displayProperty=fullName>, ，<xref:System.Object?displayProperty=fullName>, ，<xref:System.Uri?displayProperty=fullName>。  
  
## 本节内容  
 [数组](../../../docs/standard/design-guidelines/arrays.md)  
 [特性](../../../docs/standard/design-guidelines/特性.md)  
 [集合](../../../amples/snippets/cpp/VS_Snippets_Misc/cx_collections/cpp/collections.vcxproj)  
 [序列化](../../../docs/standard/design-guidelines/序列化.md)  
 [System.Xml 使用情况](../../../docs/standard/design-guidelines/system-xml-usage.md)  
 [相等运算符](../../../docs/standard/design-guidelines/equality-operators.md)  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)