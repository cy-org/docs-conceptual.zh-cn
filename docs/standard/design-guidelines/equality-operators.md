---
title: "相等运算符 | Microsoft Docs"
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
  - "类库设计准则 [.NET Framework] Equals 方法"
  - "类库设计准则 [.NET Framework] 相等运算符"
  - "相等运算符 （= =） [.NET Framework]"
  - "Equals 方法"
  - "= = 运算符 （等于） [.NET Framework]"
ms.assetid: bc496a91-fefb-4ce0-ab4c-61f09964119a
caps.latest.revision: 13
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 13
---
# 相等运算符
此部分讨论重载相等运算符并引用 `operator==` 和 `operator!=` 作为相等运算符。  
  
 **X 不** 重载的相等运算符，而另一个。  
  
 **✓ 执行** 确保 <xref:System.Object.Equals%2A?displayProperty=fullName> 和相等运算符具有完全相同的语义和相似的性能特征。  
  
 这通常意味着 `Object.Equals` 需要时重载相等运算符时，会覆盖。  
  
 **X 避免** 相等运算符从引发异常。  
  
 例如，如果返回 false 的参数之一为 null 而不是引发 `NullReferenceException`。  
  
## 有关值类型的相等运算符  
 **✓ 执行** 重载相等运算符对值类型，如果相等是有意义。  
  
 在大多数编程语言中，没有默认实现的 `operator==` 对于值类型。  
  
## 对引用类型的相等运算符  
 **X 避免** 重载相等运算符对可变引用类型。  
  
 许多语言都有内置的相等运算符对于引用类型。 内置运算符通常实现引用相等性，并更改为值相等的默认行为时，许多开发人员都很惊讶。  
  
 因为不变性使得很难注意引用相等性和值相等性之间的区别，这一问题缓解对不可变的引用类型。  
  
 **X 避免** 重载相等运算符对引用类型，如果该实现可能会显著变慢的引用相等性。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [使用准则](../../../docs/standard/design-guidelines/usage-guidelines.md)