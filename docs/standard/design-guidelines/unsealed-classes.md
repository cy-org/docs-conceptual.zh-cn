---
title: "未密封的类 | Microsoft Docs"
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
  - "未密封的类 [.NET Framework]"
  - "未密封的类"
  - "继承中类"
ms.assetid: 9a3bd505-90f5-4053-9f0d-3cf5fa3d3ebf
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# 未密封的类
密封的类不能被继承，并会阻止可扩展性。 与此相反，可以从继承的类称为未密封的类。  
  
 **✓ 请考虑** 没有使用未密封的类添加虚拟或受保护成员，如提供成本较低的好办法尚未非常感谢到框架的扩展性。  
  
 开发人员往往需要从以便添加方便成员，如自定义构造函数、 新方法或方法重载的非密封类继承。 例如，  `System.Messaging.MessageQueue` 未密封，因此允许用户创建到特定队列路径该默认值的自定义队列的步骤或添加自定义方法来简化用于特定方案的 API。  
  
 类在大多数编程语言中，默认情况下未密封的这也是框架中的大多数类建议的默认设置。 未密封的类型所提供的可扩展性是由框架用户获得赏识得多和成本不高由于出现与未密封的类型相关联的相对较低的测试成本提供。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [扩展性设计](../../../docs/standard/design-guidelines/designing-for-extensibility.md)   
 [如果要密封](../../../docs/standard/design-guidelines/sealing.md)