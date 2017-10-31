---
title: "类型设计准则 | Microsoft Docs"
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
  - "类型设计准则"
  - "类型设计准则，关于类型设计准则"
  - "类库设计准则 [.NET Framework] 类型设计准则"
  - "类型 [.NET Framework] 设计准则"
ms.assetid: 6b49314e-8bba-43ea-97ca-4e0255812f95
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# 类型设计准则
从 CLR 角度来看，有以下类型的仅有两个类别 — 引用类型和值类型，但为了框架设计有关的讨论，我们可以将类型划分为多个逻辑组，每个都有其自己特定的设计规则。  
  
 类是引用类型的一般情况。 它们构成了大量的大部分框架中的类型。 类到一组面向对象的功能，它们支持的丰富和它们的常规适用性欠其受欢迎程度。 基类和抽象类是与扩展相关的特殊逻辑分组。  
  
 接口是通过引用类型和值类型可以实现的类型。 因此，它们可以作为引用类型和值类型的多态层次结构的根。 此外，可以使用接口来模拟多个继承，CLR 不本机支持。  
  
 结构是值类型的一般情况下，且应该保留对于小型的简单类型，类似于语言基元。  
  
 枚举是用来定义短组数值，如一周，控制台颜色，诸如此类的各天的值类型的特殊情况。  
  
 静态类是旨在适用于静态成员的容器的类型。 它们通常用于提供指向其他操作的快捷方式。  
  
 委托、 异常、 属性、 数组和集合是适用于特定用途的引用类型的所有特殊情况，并为其设计和使用情况的指导原则本书在别处讨论。  
  
 **✓ 执行** 确保每种类型是一组定义完善的相关成员，而不仅仅是随机的不相关功能的集合。  
  
## 本节内容  
 [类和结构之间进行选择](../../../docs/standard/design-guidelines/choosing-between-class-and-struct.md)  
 [抽象类设计](../../../docs/standard/design-guidelines/abstract-class.md)  
 [静态类设计](../../../docs/standard/design-guidelines/static-class.md)  
 [界面设计](../../../docs/standard/design-guidelines/interface.md)  
 [结构设计](../../../docs/standard/design-guidelines/struct.md)  
 [枚举设计](../../../docs/standard/design-guidelines/enum.md)  
 [嵌套类型](../../../docs/standard/design-guidelines/nested-types.md)  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)