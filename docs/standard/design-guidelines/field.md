---
title: "字段设计 | Microsoft Docs"
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
  - "字段中，设计准则"
  - "只读字段"
  - "成员设计准则字段"
ms.assetid: 7cb4b0f3-7a10-4c93-b84d-733f7134fcf8
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# 字段设计
封装原则是最重要的概念之一在面向对象的设计。 这一原则规定对象内部存储的数据应仅对该对象可访问。  
  
 有用的方式来解释原则是说应设计一种类型，以便对该类型 （名称或类型的更改） 的字段可以进行更改而不会破坏代码以外的其他类型的成员。 此解释立即意味着所有字段必须都为私有。  
  
 此类字段中，几乎根据定义，是因为永远不需要更改，我们会从这种严格限制，排除常数和静态只读字段。  
  
 **X 不** 提供公共或受保护的实例字段。  
  
 您应提供用于访问而不是使它们成为公共或受保护的字段的属性。  
  
 **✓ 执行** 常数字段用于将永远不会改变的常量。  
  
 编译器直接在调用代码加深 const 字段的值。 因此，可以永远不会更改常量的值，而不必冒险破坏兼容性。  
  
 **✓ 执行** 使用公共静态 `readonly` 预定义的对象实例的字段。  
  
 如果预定义的类型的实例，请将它们声明为公共只读静态字段的类型本身。  
  
 **X 不** 分配给可变类型的实例 `readonly` 字段。  
  
 可变类型是可实例化之后修改的实例的类型。 例如，数组、 大多数集合和流是可变类型，但 <xref:System.Int32?displayProperty=fullName>, ，<xref:System.Uri?displayProperty=fullName>, ，和 <xref:System.String?displayProperty=fullName> 是所有固定不变。 引用类型字段上的只读修饰符可以防止从被替换的字段中存储的实例，但不会阻止该字段的实例数据更改的实例的成员的调用被修改。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [成员设计准则](../../../docs/standard/design-guidelines/member.md)   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)