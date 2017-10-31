---
title: "虚成员 | Microsoft Docs"
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
  - "可重写成员"
  - "虚拟成员"
  - "成员 [.NET Framework] 虚拟"
ms.assetid: 8ff4eb97-0364-43ec-8a02-934b5cd94d19
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# 虚成员
虚拟成员可以被重写，因此更改行为的子类。 它们是非常类似于在它们提供的可扩展性方面的回调，但它们是在执行性能和内存消耗方面更好。 此外，虚拟成员感觉更自然需要创建一个特殊类型的现有类型 （专用） 的方案中。  
  
 虚拟成员优于回调和事件，但不是比非虚方法的更好地执行。  
  
 虚拟成员的主要缺点是，虚拟成员的行为只能在编译时修改。 可以在运行时修改回调的行为。  
  
 虚拟成员，如回调 （和可能有多个回调），是成本设计、 测试和维护，因为对某个虚拟成员的任何调用可以在不可预测的方式中重写并可以执行任意代码。 此外，更多的工作量通常要求以明确定义的协定的虚拟成员，使设计和记录它们的成本较高。  
  
 **X 不** 虚成员，除非您有充足的理由，若要这样做，并且您注意的设计、 测试和维护虚拟成员与相关的所有成本。  
  
 虚拟成员都是在可以对它们进行而不会破坏兼容性的更改方面更少严格。 此外，它们是比非虚拟成员，主要是因为对虚拟成员的调用将不内联。  
  
 **✓ 请考虑** 限制于仅是绝对必要的扩展性。  
  
 **✓ 执行** 首选受保护的辅助功能的虚拟成员，而公共可访问性。 公共成员应通过调用受保护的虚拟成员提供可扩展性 （如果需要）。  
  
 一个类的公共成员应为此类的直接使用者提供正确的功能集。 旨在子类，在中重写虚拟成员和受保护的可访问性是作用域为使用其中的所有虚拟的扩展点的好办法。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [扩展性设计](../../../docs/standard/design-guidelines/designing-for-extensibility.md)