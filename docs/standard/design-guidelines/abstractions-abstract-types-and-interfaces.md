---
title: "抽象 （抽象类型和接口） | Microsoft Docs"
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
  - "抽象接口 [.NET Framework]"
  - "抽象接口 [.NET Framework]"
  - "抽象类型 [.NET Framework]"
  - "抽象类型 [.NET Framework]"
ms.assetid: 0a632bc7-9b03-44ee-8842-c82f88672a45
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# 抽象 （抽象类型和接口）
一种抽象是用于描述一个协定，但不提供完整实现的协定类型。 通常作为抽象类或接口，来实现的抽象，而且随附一组定义完善的参考文档描述实现协定的类型所需的语义。 .NET Framework 中最重要的抽象的一些 <xref:System.IO.Stream>, ，<xref:System.Collections.Generic.IEnumerable%601>, ，和 <xref:System.Object>。  
  
 您可以通过实现支持协定的抽象的具体类型并将此具体的类型与框架 Api 使用 （操作系统上） 使用扩展框架的抽象。  
  
 能够承受时间的考验的有意义，而且有用抽象是很难进行设计。 主要困难获取组的成员，没有更多和更少不适当。 如果一种抽象具有太多的成员，它将成为难于或甚至不可能实现。 如果它具有针对所承诺的功能太少成员，它将成为无用的许多有趣的情形。  
  
 一种框架中的太多抽象也有负面影响框架的可用性。 通常是很难了解一种抽象，而不了解它如何适用于具体的实现和针对抽象的操作的 Api 的较大的图片。 此外，抽象和其成员的名称是一定是抽象类，这通常会使它们比较难懂并且 unapproachable 而不首先了解及其用法的更广泛的上下文。  
  
 但是，抽象提供极强大其他可扩展性机制通常不能与匹配的可扩展性。 会面临许多体系结构模式中，即插即用接程序之类的核心控制反转 \(IoC\)、 管道、 和等等。 它们也是非常重要的可测试性的框架。 很好的抽象，使其可以去掉用于单元测试的大量依赖关系。 总之，抽象负责广受欢迎的丰富功能，现代面向对象的框架。  
  
 **X 不** 提供抽象，除非它们所测试的开发几个具体实现和使用抽象的 Api。  
  
 **✓ 执行** 设计一种抽象时，请仔细选择一个抽象类和接口之间。  
  
 **✓ 请考虑** 提供抽象的具体实现的引用测试。 此类测试应允许用户以测试是否它们的实现正确地实现该协定。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [扩展性设计](../../../docs/standard/design-guidelines/designing-for-extensibility.md)