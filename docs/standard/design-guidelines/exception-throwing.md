---
title: "引发异常 | Microsoft Docs"
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
  - "引发的异常"
  - "显式引发异常"
  - "引发异常，设计指南"
ms.assetid: 5388e02b-52f5-460e-a2b5-eeafe60eeebe
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# 引发异常
引发异常的准则，本节中所述需要正确定义执行失败的含义。 每当某一成员不能执行它时执行失败时发生设计目的 （什么成员名称所示）。 例如，如果 `OpenFile` 方法无法返回给调用方的打开的文件句柄，它将被认为执行失败。  
  
 大多数开发人员已变得越来越熟悉使用由零或空引用异常除之类的用法错误。 在框架中，异常用于所有错误条件，包括执行错误。  
  
 **X 不** 返回的错误代码。  
  
 例外是框架中的错误报告的主要方式。  
  
 **✓ 执行** 通过引发异常来报告执行失败。  
  
 **✓ 请考虑** 终止的进程通过调用 `System.Environment.FailFast` （.NET Framework 2.0 功能） 而不是引发异常，如果您的代码遇到进一步执行不安全的情况。  
  
 **X 不** 正常流的控制能力，如有可能使用异常。  
  
 除了系统故障和具有潜在的争用情况的操作，框架设计人员应设计 Api，以便用户可以编写代码并不会引发异常。 例如，可以提供一种方法，以便用户可以编写不引发异常的代码在调用成员之前检查前提条件。  
  
 用于检查另一个成员的前置条件的成员通常称为测试人员，而实际奏效的成员称为 doer。  
  
 一些情形下 Tester\-doer 模式可能带来严重的性能开销。 在这种情况下，应考虑所谓的重试分析模式 \(请参阅 [异常和性能](../../../docs/standard/design-guidelines/exceptions-and-performance.md) 有关详细信息\)。  
  
 **✓ 请考虑** 引发异常的性能影响。 每秒 100 以上 throw 率很有可能明显影响大多数应用程序的性能。  
  
 **✓ 执行** 文档由于与成员的冲突而引发的公开可调用的成员的所有异常协定 （而不是系统故障），并将它们视为协定的一部分。  
  
 异常是协定的一部分，不应到下一个更改从一个版本 （即，不应更改异常类型，并不应添加新的异常）。  
  
 **X 不** 是否可以引发的公共成员基于具有某些选项。  
  
 **X 不** 具有作为返回值返回异常的公共成员或 `out` 参数。  
  
 返回从公共 Api 而不会引发这些异常会使无效的许多优点的基于异常的错误报告。  
  
 **✓ 请考虑** 使用异常生成器方法。  
  
 很容易从不同位置引发同一异常。 若要避免代码膨胀，使用使用帮助器方法创建异常并初始化其属性。  
  
 此外，不会引发异常的成员进行内联。 移动 throw 语句生成器可能会使要成为内联的成员。  
  
 **X 不** 异常筛选器块中引发异常。  
  
 当异常筛选器引发异常时，CLR 中，捕捉异常并且该筛选器返回 false。 此行为很难区分从筛选器执行并显式将返回 false，因此很难进行调试。  
  
 **X 避免** 显式从引发异常 finally 块。 导致调用的方法引发的隐式引发的异常是可接受的。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [异常设计准则](../../../docs/standard/design-guidelines/exceptions.md)