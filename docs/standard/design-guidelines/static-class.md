---
title: "静态类设计 | Microsoft Docs"
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
  - "类型设计准则静态类"
  - "类库设计准则 [.NET Framework] 类"
  - "类 [.NET Framework] 静态"
  - "静态类 [.NET Framework]"
  - "类 [.NET Framework] 设计准则"
  - "类型设计准则类"
ms.assetid: d67c14d8-c4dd-443f-affb-4ccae677c9b6
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# 静态类设计
一个静态类定义为仅包含静态成员的类 \(当然除了从继承的实例成员 <xref:System.Object?displayProperty=fullName> 和可能是一个专用的构造函数\)。 某些语言中为静态类提供内置支持。 在 C\# 2.0 及更高版本，一个类声明为静态，它是密封、 抽象的可以重写任何实例成员，或将其声明。  
  
 静态类是纯粹的面向对象的设计和简单性的折衷。 它们通常用于提供指向其他操作的快捷方式 \(如 <xref:System.IO.File?displayProperty=fullName>\)，扩展方法或为其完整的面向对象的包装是没有保证的功能的持有者 \(如 <xref:System.Environment?displayProperty=fullName>\)。  
  
 **✓ 执行** 静态类应谨慎使用。  
  
 静态类应只可用作支持面向对象的框架的核心类。  
  
 **X 不** 静态类视为无所不包。  
  
 **X 不** 声明或重写中的静态类的实例成员。  
  
 **✓ 执行** 静态类声明为密封的抽象，并添加一个私有实例构造函数，如果您的编程语言不具有对静态类的内置支持。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [类型设计准则](../../../docs/standard/design-guidelines/type.md)   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)