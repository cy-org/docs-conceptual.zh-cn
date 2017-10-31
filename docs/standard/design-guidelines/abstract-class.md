---
title: "抽象类设计 | Microsoft Docs"
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
  - "类型设计准则，抽象类"
  - "抽象类，设计准则"
  - "类库设计准则 [.NET Framework] 类"
  - "抽象类 [.NET Framework]"
  - "类 [.NET Framework] 设计准则"
  - "类型设计准则类"
ms.assetid: d3646e6d-5c1f-4922-8fb0-ec5effb30d60
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# 抽象类设计
**X 不** 在抽象类型中定义公共或受保护的内部构造函数。  
  
 构造函数应为公共的仅当用户将需要创建该类型的实例。 因为您无法创建抽象类型的实例，具有公共构造函数的抽象类型，并且错误地设计令人误解的用户。  
  
 **✓ 执行** 在抽象类中定义为受保护或内部构造函数。  
  
 受保护的构造函数更常见，而且只是允许基类可以创建子类型时执行自己的初始化。  
  
 内部构造函数可以用于限制对程序集定义的类的抽象类的具体实现。  
  
 **✓ 执行** 提供至少一个继承自您所发运的每个抽象类的具体类型。  
  
 执行此可帮助验证抽象类的设计。 例如，  <xref:System.IO.FileStream?displayProperty=fullName> 是实现 <xref:System.IO.Stream?displayProperty=fullName> 抽象类。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [类型设计准则](../../../docs/standard/design-guidelines/type.md)   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)