---
title: "用于实现抽象基类 | Microsoft Docs"
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
  - "抽象 [.NET Framework]"
  - "基类、 抽象"
ms.assetid: 37a2d9a4-9721-482a-a40f-eee2c1d97875
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# 用于实现抽象基类
严格地说，类成为基类的类，当另一个类派生自它时。 但是，对于本部分中，基类是主要用于提供一个共同抽象或能够重用某些其他类的默认实现但是继承的类。 基类，这些类通常位于以下位置继承层次结构，层次结构根部的抽象和底部的多个自定义实现之间的中间。  
  
 它们作为实现帮助器用于实现抽象。 例如，对于有序集合的项的框架的抽象之一就是 <xref:System.Collections.Generic.IList%601> 接口。 实现 <xref:System.Collections.Generic.IList%601> 并非易事，，因此框架提供了多个基类，这些类，如 <xref:System.Collections.ObjectModel.Collection%601> 和 <xref:System.Collections.ObjectModel.KeyedCollection%602>, ，它可以充当帮助程序实现自定义集合。  
  
 基类，这些类通常是不适合作为抽象本身，因为他们往往会包含太多的实现。 例如， `Collection<T>` 基类提供了很多实现与它实现非泛型的事实相关的 `IList` 接口 （用于与非泛型集合更好地集成），表明它不存储在内存中其域中的一个项的集合。  
  
 如前面所述，基类，这些类可以提供宝贵帮助的用户需要实现的抽象，但在同一时间可重大的责任。 他们添加外围应用和增加继承层次结构的深度并因此从概念上讲使框架变得复杂。 因此，仅当它们为框架的用户提供了巨大的价值，则应使用基类，这些类。 如果它们仅对的框架中，顺序区分大小来自委托，而不是继承的内部实现的基类应强考虑实施者提供值，它们应避免使用。  
  
 **✓ 请考虑** 使基本类抽象，即使它们不包含任何抽象成员。 这清楚地对用户进行通信的类旨在仅从继承。  
  
 **✓ 请考虑** 置于单独的命名空间从主线方案类型的基类，这些类。 根据定义，基类，这些类适用于高级的扩展性方案，因此它们不感兴趣的大多数用户。  
  
 **X 避免** 命名"基"后缀结尾的基类，如果类适用于在公共 Api 中使用。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [扩展性设计](../../../docs/standard/design-guidelines/designing-for-extensibility.md)