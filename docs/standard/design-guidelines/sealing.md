---
title: "如果要密封 | Microsoft Docs"
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
  - "限制扩展性"
  - "密封类 [.NET Framework]"
  - "防止自定义"
  - "密封类"
ms.assetid: cc42267f-bb7a-427a-845e-df97408528d4
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# 如果要密封
面向对象的框架的功能之一是开发人员可以扩展和它们的方式自定义未预料到框架设计器。 这是设计的两个电源和可扩展的危险。 当您设计您的框架时，它，因此是非常重要，仔细设计可扩展性，当需要它时，并限制可扩展性时这是很危险。  
  
 密封了强大的机制，以防止可扩展性。 您可以先密封类或单个成员。 密封类可防止用户从类继承。 如果要密封成员可防止用户重写的特定成员。  
  
 **X 不** 密封类，而无需有充分的理由，若要这样做。  
  
 密封类，因为您不能将可扩展性方案不是一个充分的理由。 Framework 用户喜欢由于各种 nonobvious 原因，如添加方便成员从类继承。 请参阅 [未密封的类](../../../docs/standard/design-guidelines/unsealed-classes.md) nonobvious 原因，例如用户想要从一个类型继承。  
  
 密封类充分的理由如下︰  
  
-   此类是静态的类。 请参阅 [静态类设计](../../../docs/standard/design-guidelines/static-class.md)。  
  
-   类继承的受保护成员中存储安全敏感机密信息。  
  
-   类继承多个虚成员，并分别对它们进行密封的成本会得不偿失将保留未密封的类。  
  
-   类是需要非常快的运行时查找的属性。 密封的属性具有比未密封的略高性能级别。 请参阅 [特性](../../../docs/standard/design-guidelines/特性.md)。  
  
 **X 不** 在密封类型中声明受保护或虚拟成员。  
  
 根据定义，不能从继承密封的类型。 这意味着，不能调用密封类型上的受保护的成员，并且不能重写密封类型上的虚拟方法。  
  
 **✓ 请考虑** 密封重写的成员。  
  
 引入虚拟成员所产生的问题 \(中所述 [虚成员](../../../docs/standard/design-guidelines/virtual-members.md)\) 适用于重写，尽管用于稍有一定程度上。 如果要密封替代可以为您屏蔽的继承层次结构中该点开始这些问题。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [扩展性设计](../../../docs/standard/design-guidelines/designing-for-extensibility.md)   
 [未密封的类](../../../docs/standard/design-guidelines/unsealed-classes.md)