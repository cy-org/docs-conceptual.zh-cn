---
title: "Framework 设计准则 | Microsoft Docs"
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
  - "库，.NET Framework 类库"
  - "有关类类库设计准则 [.NET Framework]"
  - "类库设计准则 [.NET Framework]"
ms.assetid: 5fbcaf4f-ea2a-4d20-b0d6-e61dee202b4b
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Framework 设计准则
本部分提供指导原则设计库，可以扩展并与.NET Framework 进行交互。 旨在帮助类库设计人员通过提供用于开发的编程语言无关的统一编程模型，确保 API 一致性和易用性。 我们建议开发的类和扩展.NET Framework 的组件时遵从这些设计原则。 不一致的库设计产生负面影响开发人员工作效率并不鼓励采用。  
  
 指导原则按简单的条件为前缀的建议组织 `Do`, ，`Consider`, ，`Avoid`, ，和 `Do not`。 这些指南旨在帮助类库设计人员了解不同的解决方案之间权衡。 可能有好的库设计要求您违反这些设计原则的情况。 这种情况下应该很少见，并具有您的决定一个清晰且令人信服的理由是很重要。  
  
 这些准则摘自本书 *Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式*, 、 Krzysztof Cwalina 和 Brad Abrams。  
  
## 本节内容  
 [命名准则](../../../docs/standard/design-guidelines/naming-guidelines.md)  
 命名的程序集、 命名空间、 类型和类库中的成员提供了准则。  
  
 [类型设计准则](../../../docs/standard/design-guidelines/type.md)  
 提供了使用静态和抽象类、 接口、 枚举、 结构和其他类型的指导原则。  
  
 [成员设计准则](../../../docs/standard/design-guidelines/member.md)  
 提供设计和使用属性、 方法、 构造函数、 字段、 事件、 运算符和参数的准则。  
  
 [扩展性设计](../../../docs/standard/design-guidelines/designing-for-extensibility.md)  
 讨论可扩展性机制，例如子类化，使用事件、 虚拟成员和回调，并说明如何选择最好地满足您的框架要求的机制。  
  
 [异常设计准则](../../../docs/standard/design-guidelines/exceptions.md)  
 描述设计、 引发和捕获异常的设计准则。  
  
 [使用准则](../../../docs/standard/design-guidelines/usage-guidelines.md)  
 描述使用公共类型，如数组、 属性和集合、 支持序列化，以及重载相等运算符的准则。  
  
 [常见设计模式](../../../docs/standard/design-guidelines/common-design-patterns.md)  
 提供选择和实现依赖关系属性和 dispose 模式的准则。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [概述](../../../docs/framework/get-started/overview.md)   
 [.NET Framework 的路线图](http://msdn.microsoft.com/zh-cn/0b46b7c6-9163-4f99-8e58-0d1ee7da8c67)   
 [开发指南](../../../docs/framework/development-guide.md)