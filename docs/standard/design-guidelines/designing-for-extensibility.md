---
title: "扩展性设计 | Microsoft Docs"
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
  - "扩展类库"
  - ".NET Framework 中的类库的可扩展性"
  - "类库设计准则 [.NET Framework] 可扩展性"
  - "类库扩展性 [.NET Framework]"
ms.assetid: 1cdb8740-871a-456c-9bd9-db96ca8d79b3
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# 扩展性设计
设计一种框架的一个重要方面确保仔细考虑框架的扩展性。 这需要了解的成本和收益与各种可扩展性机制相关联。 这一章可帮助您决定哪些可扩展性机制 — 子类化、 事件、 虚拟成员、 回调，等等 — 能够最好地满足您的框架的要求。  
  
 有多种方法，以便可扩展性框架中。 它们范围为功能较差，但成本较低至非常强大但成本高昂。 对于任何给定的可扩展性要求，则应选择符合要求的最低成本高昂的扩展性机制。 请记住，通常可以添加更大的扩展性更高版本，但您可以永远不会收回它而不会引入的重大更改。  
  
## 本节内容  
 [未密封的类](../../../docs/standard/design-guidelines/unsealed-classes.md)  
 [受保护的成员](../../../docs/standard/design-guidelines/protected-members.md)  
 [事件和回调](../../../docs/standard/design-guidelines/events-and-callbacks.md)  
 [虚成员](../../../docs/standard/design-guidelines/virtual-members.md)  
 [抽象 （抽象类型和接口）](../../../docs/standard/design-guidelines/abstractions-abstract-types-and-interfaces.md)  
 [用于实现抽象基类](../../../docs/standard/design-guidelines/base-classes-for-implementing-abstractions.md)  
 [如果要密封](../../../docs/standard/design-guidelines/sealing.md)  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)