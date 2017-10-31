---
title: "扩展方法 | Microsoft Docs"
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
ms.assetid: 5de945cb-88f4-49d7-b0e6-f098300cf357
caps.latest.revision: 4
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 4
---
# 扩展方法
扩展方法是一种语言功能，允许使用实例方法调用语法来调用静态方法。 这些方法必须采用至少一个参数，它表示的方法是在上运行的实例。  
  
 定义此类扩展方法的类中被称为"发起人"类，并必须声明为静态。 若要使用扩展方法，其中一个必须导入的命名空间定义的赞助者类。  
  
 **X 避免** frivolously 定义扩展方法，尤其是在您自己的类型。  
  
 如果您拥有的一种类型的源代码，请考虑改为使用常规的实例方法。 如果你拥有，并且你想要添加一个方法，要非常小心。 扩展方法的自由使用有可能会干扰 Api 未设计为具有这些方法的类型。  
  
 **✓ 请考虑** 的任何以下情况下使用扩展方法︰  
  
-   若要提供的帮助器可以将功能与每个接口实现的如果说功能编写方面的核心接口。 这是因为具体实现否则不能分配给接口。 例如， `LINQ to Objects` 运算符作为扩展方法实现所有 <xref:System.Collections.Generic.IEnumerable%601> 类型。 因此，任何 `IEnumerable<>` 实现是自动启用 LINQ 的。  
  
-   依赖于某些类型，但这种依赖关系的实例方法中引入时，将会破坏依赖关系管理规则。 例如，依赖项从 <xref:System.String> 到 <xref:System.Uri?displayProperty=fullName> 可能是不可取，，因此 `String.ToUri()` 返回的实例方法 `System.Uri` 从依赖项管理角度来看问题的设计非常。 静态扩展方法 `Uri.ToUri(this string str)` 返回 `System.Uri` 会多更好的设计。  
  
 **X 避免** 上定义的扩展方法 <xref:System.Object?displayProperty=fullName>。  
  
 VB 用户不能使用该扩展方法的语法的对象引用上调用此类方法。 VB 不支持调用此类方法，因为在 VB 中声明的引用，因为对象会强制所有方法调用它以进行后期绑定 （名为的实际成员确定在运行时），而绑定到扩展方法在编译时 （早期绑定） 确定。  
  
 请注意，相同的绑定行为存在，或者不支持扩展方法，该原则也适用于其他语言。  
  
 **X 不** 置于扩展的类型相同的命名空间的扩展方法，除非它是为添加到接口的方法或依赖关系管理。  
  
 **X 避免** 定义两个或多个具有相同签名的扩展方法，即使它们位于不同的命名空间。  
  
 **✓ 请考虑** 如果类型是接口，并且如果扩展方法旨在用于在大多数或所有情况下在扩展的类型相同的命名空间中定义的扩展方法。  
  
 **X 不** 定义在正常情况下与其他功能相关联的命名空间中实现功能的扩展方法。 相反，在与他们属于此功能关联的命名空间中定义它们。  
  
 **X 避免** 通用的方式命名的命名空间专用于扩展方法 （例如，"扩展"）。 使用描述性的名称 （例如，"路由"） 相反。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [成员设计准则](../../../docs/standard/design-guidelines/member.md)   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)