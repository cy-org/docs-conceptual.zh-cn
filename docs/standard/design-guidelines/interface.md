---
title: "界面设计 | Microsoft Docs"
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
  - "接口 [.NET Framework] 设计准则"
  - "类型设计准则接口"
  - "类库设计准则 [.NET Framework] 接口"
ms.assetid: a016bd18-6710-4358-9438-9f190a295392
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# 界面设计
尽管大多数 Api 最好使用类和结构进行建模，一些情况下在其中更合适或接口的唯一选择。  
  
 CLR 不支持多重继承 （即，CLR 类不能从多个基类继承），但它确实允许实现除了继承自基类的类的一个或多个接口的类型。 因此，接口通常用于实现多重继承的效果。 例如， <xref:System.IDisposable> 是一个接口，允许类型以支持 disposability 独立于他们想要参与任何其他继承的层次结构。  
  
 另外一种在哪个定义一个接口有适当的情况是在创建了公共接口，可支持的几种类型，包括某些值类型。 值类型不能从继承类型以外 <xref:System.ValueType>, ，但它们可以实现接口，因此使用的接口是为了提供一个公共基类型的唯一选项。  
  
 **✓ 执行** 定义一个接口，如果您需要一些常见的 API 来支持的一组类型，其中包含值类型。  
  
 **✓ 请考虑** 定义一个接口，如果您需要对已继承某些其他类型的类型支持它的功能。  
  
 **X 避免** 使用标记接口 （不包含任何成员的接口）。  
  
 如果您需要将类标记为具有特定特征 （标记），一般情况下，使用自定义特性，而不是一个接口。  
  
 **✓ 执行** 提供至少一种类型的接口的实现。  
  
 执行此可帮助验证接口的设计。 例如， <xref:System.Collections.Generic.List%601> 是实现 <xref:System.Collections.Generic.IList%601> 接口。  
  
 **✓ 执行** 提供至少一个使用您定义每个接口的 API （作为参数或属性采用该接口的方法类型化为接口）。  
  
 执行此可帮助验证界面设计。 例如， <xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=fullName> 使用 <xref:System.Collections.Generic.IComparer%601?displayProperty=fullName> 接口。  
  
 **X 不** 将成员添加到具有以前发布的接口。  
  
 这样做将会破坏接口的实现。 为了避免版本控制问题，应创建新的接口。  
  
 除了这些指南中所述的情况下，您应，一般情况下，选择类，而不是接口在设计托管的代码的可重用库。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [类型设计准则](../../../docs/standard/design-guidelines/type.md)   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)