---
title: "结构设计 | Microsoft Docs"
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
  - "类库设计准则 [.NET Framework] 结构"
  - "释放结构"
  - "分配结构"
  - "值类型结构"
  - "结构设计"
  - "类型设计准则结构"
  - "结构 [.NET Framework] 设计准则"
ms.assetid: 1f48b2d8-608c-4be6-9ba4-d8f203ed9f9f
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# 结构设计
一般用途的值类型通常称为结构，其 C\# 关键字。 本部分提供有关常规的结构设计指导原则。  
  
 **X 不** 为结构提供一个默认构造函数。  
  
 遵循这一准则允许的结构，而无需在该数组的每个项上运行构造函数创建的数组。 请注意，C\# 不允许结构拥有默认构造函数。  
  
 **X 不** 定义可变值类型。  
  
 可变值类型有以下几个问题。 例如，在属性 getter 返回值类型时，调用方将收到一个副本。 隐式创建的复制，因为开发人员可能不知道该副本，而不是原始值会变化。 此外，某些语言 （尤其是动态语言） 有问题使用可变值类型，因为即使本地变量，在取消引用时，会产生一个副本进行。  
  
 **✓ 执行** 确保其中所有实例数据的状态设置为零，false，则为 null （根据需要） 无效。  
  
 这样可以防止意外创建无效的实例时创建的结构数组。  
  
 **✓ 执行** 实现 <xref:System.IEquatable%601> 有关值类型。  
  
 <xref:System.Object.Equals%2A?displayProperty=fullName> 值类型上的方法会导致装箱，和它的默认实现不是非常高效，因为它使用反射。<xref:System.IEquatable%601.Equals%2A> 可以更好的性能，并且可以实现，以便它不会导致装箱。  
  
 **X 不** 显式延长 <xref:System.ValueType>。 实际上，大多数语言禁止此行为。  
  
 一般情况下，结构可以非常有用，但仅用于不经常装箱的小规模、 单个的不可变值。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [类型设计准则](../../../docs/standard/design-guidelines/type.md)   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [类和结构之间进行选择](../../../docs/standard/design-guidelines/choosing-between-class-and-struct.md)