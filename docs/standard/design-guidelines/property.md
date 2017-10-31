---
title: "属性设计 | Microsoft Docs"
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
  - "成员设计准则属性"
  - "设计指南的属性 [.NET Framework]"
ms.assetid: 127cbc0c-cbed-48fd-9c89-7c5d4f98f163
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# 属性设计
尽管从技术上讲非常类似于方法属性，但它们是在其使用情况方面大不相同。 它们应被视为智能字段。 它们具有字段中，调用语法和方法的灵活性。  
  
 **✓ 执行** 创建只读属性，如果调用方不应能够更改属性的值。  
  
 请记住，如果类型的属性是可变的引用类型，可以更改属性值，即使属性是只读属性。  
  
 **X 不** 提供具有更广泛的可访问性比 getter 的 setter 设置只读属性。  
  
 例如，请使用公共 setter 和受保护的 getter 使用属性。  
  
 如果不能提供的属性 getter，请改为实现此功能作为一种方法。 请考虑从开始的方法名 `Set` 并在后面加什么您将已命名属性。 例如， <xref:System.AppDomain> 具有一个名为方法 `SetCachePath` 而不是让一个名为仅限组的属性 `CachePath`。  
  
 **✓ 执行** 提供适当的默认值为所有属性，确保，默认值不会导致安全漏洞或非常低效的代码。  
  
 **✓ 执行** 允许将属性按任意顺序设置，即使这将导致临时无效状态的对象。  
  
 给定的相同对象上的其他属性的值是常见的两个或多个要相互关联到一个属性的某些值可能无效的点的属性。 在这种情况下，从无效状态导致异常应该会推迟，直到相互关联的属性由该对象使用实际上在一起。  
  
 **✓ 执行** 保留之前的值，如果属性 setter 引发异常。  
  
 **X 避免** 属性 getter 从引发异常。  
  
 属性 getter 应该是简单的操作，并且不应具有任何前置条件。 如果一个 getter 可能会引发异常，它应可能重新设计为一种方法。 请注意，此规则不适用于索引器，我们执行预期结果验证参数的异常的位置。  
  
### 索引的属性设计  
 索引的属性是一个特殊属性，它可以具有参数，可以调用使用特殊语法类似于数组索引。  
  
 索引的属性通常被称为索引器。 应仅在 Api，可提供访问的逻辑集合中的项中使用索引器。 例如，字符串是一组字符和在索引器 <xref:System.String?displayProperty=fullName> 加以访问其中的字符。  
  
 **✓ 请考虑** 使用索引器提供对存储在内部数组中的数据的访问。  
  
 **✓ 请考虑** 提供索引器表示的项的集合的类型。  
  
 **X 避免** 使用索引属性具有多个参数。  
  
 如果设计需要多个参数，请重新考虑是否属性实际上表示取值函数的逻辑集合。 如果不存在，请改为使用方法。 请考虑从开始的方法名 `Get` 或 `Set`。  
  
 **X 避免** 参数类型，而不具有索引器 <xref:System.Int32?displayProperty=fullName>, ，<xref:System.Int64?displayProperty=fullName>, ，<xref:System.String?displayProperty=fullName>, ，<xref:System.Object?displayProperty=fullName>, ，或枚举。  
  
 如果设计需要其他类型的参数，强烈重新评估是否 API 确实表示对逻辑集合取值函数。 如果不存在，使用一种方法。 请考虑从开始的方法名 `Get` 或 `Set`。  
  
 **✓ 执行** 起名为 `Item` 的索引属性，除非有很明显更好的名称 \(例如，请参阅 <xref:System.String.Chars%2A> 属性 `System.String`\)。  
  
 在 C\# 中，索引器默认情况下名为项。<xref:System.Runtime.CompilerServices.IndexerNameAttribute> 可以用于自定义此名称。  
  
 **X 不** 提供索引器和在语义上等效的方法。  
  
 **X 不** 提供多个系列中一种类型的重载索引器。  
  
 这是由 C\# 编译器实施的。  
  
 **X 不** 使用非默认索引属性。  
  
 这是由 C\# 编译器实施的。  
  
### 属性更改通知事件  
 有时很有用提供事件通知中的属性值的更改的用户。 例如， `System.Windows.Forms.Control` 引发 `TextChanged` 事件之后的值及其 `Text` 属性已更改。  
  
 **✓ 请考虑** 引发更改通知事件时在高级别 Api （通常是设计器组件） 中的属性值会被修改。  
  
 如果用户不必知道当更改对象的属性的一种好方案，该对象应引发更改通知事件的属性。  
  
 但是，不太值得为低级别的 Api，如基类型或集合会引发此类事件的系统开销。 例如， <xref:System.Collections.Generic.List%601> 不会引发此类事件，当新项添加到列表和 `Count` 属性更改。  
  
 **✓ 请考虑** 引发更改通知事件时的属性值发生更改时通过外部因素。  
  
 如果通过某种外部因素 （以通过在对象上调用方法以外的其他方式） 更改的属性值，会引发事件指示向开发人员正在更改的值，且已更改。 一个典型示例是 `Text` 文本框控件的属性。 当用户键入中文 `TextBox`, ，属性值将自动更改。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [成员设计准则](../../../docs/standard/design-guidelines/member.md)   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)