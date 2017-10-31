---
title: "事件和回调 | Microsoft Docs"
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
  - "扩展的事件 [.NET Framework]"
  - "且执行回调的方法 [.NET Framework]"
  - "回调方法"
  - "回调"
ms.assetid: 48b55c60-495f-4089-9396-97f9122bba7c
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# 事件和回调
回调将扩展点，允许一个框架，用于回调到用户代码中通过一个委托。 通常，这些委托将传递到框架通过一种方法的参数。  
  
 事件是一种特殊的回调情况提供委托 （事件处理程序） 支持便捷且一致的语法。 此外，Visual Studio 的语句完成功能和设计器提供的帮助中使用基于事件的 Api。 （请参阅[事件设计](../../../docs/standard/design-guidelines/event.md)。）  
  
 **✓ 请考虑** 使用回调以允许用户提供自定义代码要执行的框架。  
  
 **✓ 请考虑** 使用事件以允许用户自定义一个框架，而无需了解的面向对象设计的行为。  
  
 **✓ 执行** 事件想要优先选择普通回调，因为它们是更广泛的开发人员更熟悉，与 Visual Studio 语句完成功能集成。  
  
 **X 避免** 性能敏感的 Api 中使用回调。  
  
 **✓ 执行** 使用新 `Func<...>`, ，`Action<...>`, ，或 `Expression<...>` 而不是在回调中定义的 Api 时的自定义委托的类型。  
  
 `Func<...>` 和 `Action<...>` 表示泛型委托。`Expression<...>` 表示函数定义，可以编译并随后在运行时调用但可还被序列化并传递到远程进程。  
  
 **✓ 执行** 测量和了解使用性能影响的 `Expression<...>`, ，而不是使用 `Func<...>` 和 `Action<...>` 委托。  
  
 `Expression<...>` 类型是在逻辑上等同于大多数情况下 `Func<...>` 和 `Action<...>` 委托。 主要区别在于，委托将用于本地进程内方案;表达式适用于的情况下十分有用和可能在远程进程或计算机中的表达式进行求值。  
  
 **✓ 执行** 了解，通过调用一个委托，正在执行任意代码，并可能具有安全、 正确性和兼容性的负面影响。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [扩展性设计](../../../docs/standard/design-guidelines/designing-for-extensibility.md)   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)