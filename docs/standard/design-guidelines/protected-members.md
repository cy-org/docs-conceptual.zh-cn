---
title: "受保护的成员 | Microsoft Docs"
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
  - "受保护成员 [.NET Framework]"
  - "受保护的成员"
  - "未密封的类 [.NET Framework]"
  - "类 [.NET Framework]，受保护成员"
  - "未密封的类"
  - "自定义类行为"
ms.assetid: aa0b58ee-3956-494d-ab48-471ae5db8740
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# 受保护的成员
受保护的成员本身不提供任何可扩展性，但这些用户可通过子类化可扩展性功能更强大。 它们可以用于公开高级自定义选项，而不必要地复杂化的主公共接口。  
  
 框架设计人员需要请慎用受保护的成员，因为"保护"的名称可以提供安全的错觉。 任何人都能够对子类的未密封类和访问受保护成员，并用于公共成员的防御性编码做法适用于受保护成员，因此完全相同。  
  
 **✓ 请考虑** 使用受保护的高级自定义的成员。  
  
 **✓ 执行** 处理为在为进行安全、 文档和兼容性分析的公共未密封类为受保护的成员。  
  
 任何人都可以继承自的类，以及访问受保护的成员。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [扩展性设计](../../../docs/standard/design-guidelines/designing-for-extensibility.md)