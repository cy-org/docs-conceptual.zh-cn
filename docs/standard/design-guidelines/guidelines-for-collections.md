---
title: "集合准则 | Microsoft Docs"
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
ms.assetid: 297b8f1d-b11f-4dc6-960a-8e990817304e
caps.latest.revision: 4
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 4
---
# 集合准则
任何专门用于操作的一组具有一些公共特征的对象的类型可被视为集合。 几乎始终是适用于这种类型来实现 <xref:System.Collections.IEnumerable> 或 <xref:System.Collections.Generic.IEnumerable%601>, ，因此在本部分中我们只考虑实现一个或两个接口的类型是集合。  
  
 **X 不** 公共 Api 中使用弱类型化的集合。  
  
 所有的返回值和参数表示集合的项的类型应为确切项类型，不是任何 （这仅适用于集合中的公共成员） 及其基类型。  
  
 **X 不** 使用 <xref:System.Collections.ArrayList> 或 <xref:System.Collections.Generic.List%601> 公共 Api 中。  
  
 这些类型是用于在内部实现中，不在公共 Api 而专门设计的数据结构。`List<T>` 已针对性能和成本的 Api 和灵活性 cleanness 电源优化。 例如，如果您返回 `List<T>`, ，曾经无法在客户端代码将修改的集合时收到通知。 此外， `List<T>` 公开多个成员，如 <xref:System.Collections.Generic.List%601.BinarySearch%2A>, ，不是有用或在许多情况下适用。 以下两节介绍专门设计用于公共 Api 中的类型 （抽象）。  
  
 **X 不** 使用 `Hashtable` 或 `Dictionary<TKey,TValue>` 公共 Api 中。  
  
 这些类型是用于在内部实现而专门设计的数据结构。 应使用公共 Api <xref:System.Collections.IDictionary>, ，`IDictionary <TKey, TValue>`, ，或实现一个或两个接口的自定义类型。  
  
 **X 不** 使用 <xref:System.Collections.Generic.IEnumerator%601>, ，<xref:System.Collections.IEnumerator>, ，或实现这些接口，任一除用作返回类型的任何其他类型 `GetEnumerator` 方法。  
  
 从方法返回枚举器以外的类型 `GetEnumerator` 不能与使用 `foreach` 语句。  
  
 **X 不** 两者均实现 `IEnumerator<T>` 和 `IEnumerable<T>` 上相同的类型。 这同样适用于非泛型接口 `IEnumerator` 和 `IEnumerable`。  
  
## 收集参数  
 **✓ 执行** 可能的最小专用类型用作参数类型。 获取集合作为参数使用的大多数成员 `IEnumerable<T>` 接口。  
  
 **X 避免** 使用 <xref:System.Collections.Generic.ICollection%601> 或 <xref:System.Collections.ICollection> 作为参数只是为了访问 `Count` 属性。  
  
 实际上，可以考虑使用 `IEnumerable<T>` 或 `IEnumerable` 和动态检查该对象是否实现 `ICollection<T>` 或 `ICollection`。  
  
## 集合的属性和返回值  
 **X 不** 提供可设置的集合属性。  
  
 用户可以通过首先清除该集合，然后添加新内容替换该集合的内容。 如果替换整个集合是一种常见情况，请考虑提供 `AddRange` 集合方法。  
  
 **✓ 执行** 使用 `Collection<T>` 或其子类 `Collection<T>` 属性或返回值表示的读\/写集合。  
  
 如果 `Collection<T>` 不满足某些需求 \(例如，集合必须实现 <xref:System.Collections.IList>\)，使用自定义集合，方法是实现 `IEnumerable<T>`, ，`ICollection<T>`, ，或 <xref:System.Collections.Generic.IList%601>。  
  
 **✓ 执行** 使用 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>, 的子类 `ReadOnlyCollection<T>`, ，或在极少数情况下 `IEnumerable<T>` 属性或返回值表示的只读集合。  
  
 通常，首选 `ReadOnlyCollection<T>`。 如果不满足某些需求 \(例如，集合必须实现 `IList`\)，使用自定义集合，方法是实现 `IEnumerable<T>`, ，`ICollection<T>`, ，或 `IList<T>`。 如果您实现自定义的只读集合，实现 `ICollection<T>.ReadOnly` 返回 false。  
  
 在其中你确信你将想要支持的唯一情况是只进迭代的情况下，您只需使用 `IEnumerable<T>`。  
  
 **✓ 请考虑** 而不直接使用集合使用的泛型基集合子类。  
  
 这样更合适的名称以及添加帮助器在基集合类型不存在的成员。 这是特别适用于高级 Api。  
  
 **✓ 请考虑** 返回的一个子类 `Collection<T>` 或 `ReadOnlyCollection<T>` 从很常用的方法和属性。  
  
 这将使您可以添加帮助器方法或更改在将来的集合实现。  
  
 **✓ 请考虑** 使用键控的集合，如果在集合中存储的项具有唯一键 （名称、 Id 等。）。 键控的集合是集合，可按一个整数和一个密钥索引通常通过继承来实现 `KeyedCollection<TKey,TItem>`。  
  
 键控的集合通常较大的内存需求量，如果内存开销超过了拥有密钥的好处不应使用。  
  
 **X 不** 返回空值，从集合属性或方法返回的集合。 而是返回一个空集合或为空数组。  
  
 一般规则是应为 null 和空 （0 项） 集合或数组的处理相同。  
  
### 而不是实时的集合的快照  
 表示时间在某一时刻的状态的集合都称为快照集合。 例如，包含从数据库查询返回行的集合是快照。 始终表示为当前状态的集合都称为活动的集合。 例如，集合 `ComboBox` 项是实时的集合。  
  
 **X 不** 从属性中返回快照集合。 属性应返回实时的集合。  
  
 属性 getter 应非常轻量的操作。 返回快照需要 o （n） 操作中创建一份内部集合。  
  
 **✓ 执行** 使用快照集合或某一处于活动 `IEnumerable<T>` （或其子类型） 来表示的是可变的集合 （即，可以更改而无需显式修改集合）。  
  
 一般情况下，所有集合表示共享的资源 （例如，目录中的文件） 都是可变的。 此类集合是很难或不可能实现作为实时集合，除非实现只是一个只进的枚举数。  
  
## 数组和集合之间进行选择  
 **✓ 执行** 首选集合，而数组。  
  
 集合提供更好地控制内容，可以随时间而并且更易于使用。 此外，对于只读方案中使用数组是建议使用，因为克隆该数组的成本过高。 可用性研究表明，一些开发人员更喜欢使用基于集合的 Api。  
  
 但是，如果您正在开发低级别的 Api，它可能是更好的做法数组用于读写方案。 数组具有较小的内存需求量，这有助于减少工作集，并对数组中元素的访问速度更快，因为它由运行时优化。  
  
 **✓ 请考虑** 在低级别的 Api 中使用数组，最大程度减少内存消耗，并最大化性能。  
  
 **✓ 执行** 而不是集合的字节将字节数组。  
  
 **X 不** 用于属性的数组，如果该属性也必须返回一个新数组，（例如，内部数组的副本） 每次调用属性 getter。  
  
## 实现自定义集合  
 **✓ 请考虑** 继承自 `Collection<T>`, ，`ReadOnlyCollection<T>`, ，或 `KeyedCollection<TKey,TItem>` 设计新的集合时。  
  
 **✓ 执行** 实现 `IEnumerable<T>` 设计新的集合时。 请考虑实施 `ICollection<T>` 甚至 `IList<T>` 有意义。  
  
 在实现此类自定义集合时，遵循由建立 API 模式 `Collection<T>` 和 `ReadOnlyCollection<T>` 尽可能接近。 即，显式实现相同的成员、 命名参数，如这两个集合命名它们，等等。  
  
 **✓ 请考虑** 实现非泛型集合接口 \(`IList` 和 `ICollection`\) 如果该集合将通常被传递到 Api 采用这些接口作为输入。  
  
 **X 避免** 在类型中的集合接口实现使用复杂的 Api 与集合的概念无关。  
  
 **X 不** 如继承自非泛型基集合 `CollectionBase`。 使用 `Collection<T>`, ，`ReadOnlyCollection<T>`, ，和 `KeyedCollection<TKey,TItem>` 相反。  
  
### 命名自定义集合  
 集合 \(类型实现 `IEnumerable`\) 创建主要有两个原因: （1） 若要创建新的数据结构与结构特定的操作通常比现有数据结构的不同性能特征 \(例如，  <xref:System.Collections.Generic.List%601>, ，<xref:System.Collections.Generic.LinkedList%601>, ，<xref:System.Collections.Generic.Stack%601>\)，和 （2） 若要创建专用的集合用于保存一组特定的项 \(例如，  <xref:System.Collections.Specialized.StringCollection>\)。 数据结构最常用的应用程序和库的内部实现中。 专用的集合是主要是为了在 （作为属性和参数类型） 的 Api 中公开。  
  
 **✓ 执行** 实现的抽象名称中使用"字典"后缀 `IDictionary` 或 `IDictionary<TKey,TValue>`。  
  
 **✓ 执行** 实现的类型名称中使用"集合"后缀 `IEnumerable` （或其任意后代），表示项的列表。  
  
 **✓ 执行** 使用自定义数据结构的相应的数据结构名称。  
  
 **X 避免** 集合抽象的名称中使用暗示特定实现，如"LinkedList"或"哈希表，"任何后缀。  
  
 **✓ 请考虑** 前缀同名的项类型的集合名称。 例如，存储类型的项集合 `Address` \(实现 `IEnumerable<Address>`\) 应命名为 `AddressCollection`。 如果项类型是一个接口，"I"前缀的项的类型，则可以省略。 因此，集合 <xref:System.IDisposable> 可调用项 `DisposableCollection`。  
  
 **✓ 请考虑** 只读集合的名称中使用"ReadOnly"前缀，如果相应的可写集合可能添加或框架中已存在。  
  
 例如，应调用一个只读字符串集合 `ReadOnlyStringCollection`。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [使用准则](../../../docs/standard/design-guidelines/usage-guidelines.md)