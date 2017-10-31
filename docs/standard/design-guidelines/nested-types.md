---
title: "嵌套类型 | Microsoft Docs"
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
  - "嵌套类型"
  - "公共嵌套的类型"
  - "类型设计准则，嵌套类型"
  - "嵌套类型"
  - "类型的成员 [.NET Framework]"
  - "类库设计准则 [.NET Framework]，嵌套类型"
ms.assetid: 12feb7f0-b793-4d96-b090-42d6473bab8c
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# 嵌套类型
嵌套的类型是在另一个类型，称为封闭类型的作用域内定义的类型。 嵌套的类型都有其封闭类型的所有成员访问权限。 例如，它有权访问在封闭的类型，以及以受保护的所有祖先的封闭类型中定义的字段定义的私有字段。  
  
 一般情况下，应谨慎使用嵌套的类型。 其原因有若干： 有些开发人员不完全熟悉的概念。 这些开发人员可能，例如，具有与声明的嵌套类型的变量的语法问题。 嵌套的类型与其封闭类型还非常紧密耦合，并且因此是一般用途的类型不适合。  
  
 嵌套的类型很适合于建模其封闭类型的实现详细信息。 最终用户应几乎不需要声明嵌套类型的变量，并几乎永远不能进行显式实例化嵌套的类型。 例如，集合的枚举器可以为该集合中的嵌套的类型。 枚举器通常由其封闭类型实例化，由于许多语言支持 foreach 语句，因此枚举器变量几乎不需要由最终用户声明。  
  
 **✓ 执行** 成员可访问性语义是理想的嵌套的类型和其外部类型之间的关系时使用嵌套的类型。  
  
 **X 不** 使用公共嵌套的类型作为自己的逻辑分组构造; 使用此命名空间。  
  
 **X 避免** 公开嵌套的类型。 唯一的例外是如果需要仅在极少数情况下，如生成子类或其他高级自定义应用场景中声明的嵌套类型的变量。  
  
 **X 不** 使用嵌套的类型，如果类型为可能包含类型的外部引用。  
  
 例如，传递到方法的类上定义的枚举应不定义为类中的嵌套类型。  
  
 **X 不** 使用嵌套的类型，如果他们需要由客户端代码实例化。  如果类型具有公共构造函数，它可能不应进行嵌套。  
  
 如果可实例化一个类型，这种方法似乎以指示该类型具有自己的框架中的位置 （可以创建、 使用它，并将其销毁而完全不必使用外部类型），并因此不应进行嵌套。 在没有任何关系的外部类型之外，内部类型应不广泛重用为外部类型的技术。  
  
 **X 不** 嵌套的类型定义为接口的成员。 许多语言不支持此类构造。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [类型设计准则](../../../docs/standard/design-guidelines/type.md)   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)