---
title: "正则表达式中的线程安全 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - ".NET Framework 正则表达式, 线程"
  - "分析带有正则表达式的文本, 线程"
  - "正则表达式的模式匹配, 线程"
  - "正则表达式, 线程"
  - "用正则表达式搜索, 线程"
ms.assetid: 7c4a167b-5236-4cde-a2ca-58646230730f
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# 正则表达式中的线程安全
<xref:System.Text.RegularExpressions.Regex> 类本身是线程安全和不可变的（只读的）。  也就是说，**Regex** 对象可以在任何线程上创建并在线程间共享；可以从任何线程调用匹配方法并且永远不会更改任何全局状态。  
  
 但是，应在单个线程上使用由 **Regex** 返回的结果对象（**Match** 和 **MatchCollection**）。  尽管其中许多对象是逻辑上不可变的，但这些对象的实现可以延迟一些结果的计算以提高性能；因此，调用方必须序列化对这些对象的访问。  
  
 如果需要在多个线程上共享 **Regex** 结果对象，则通过调用这些对象的同步方法，可以将它们转换成线程安全的实例。  除枚举数之外，所有正则表达式类都是线程安全的或者可以通过同步方法转换成线程安全对象。  
  
 枚举数是唯一的例外。  应用程序必须序列化对集合枚举数的调用。  规则为，如果可以在多个线程上同时枚举一个集合，则您应该同步由枚举数遍历的集合的根对象上的枚举数方法。  
  
## 请参阅  
 [.NET Framework 正则表达式](../../../docs/standard/base-types/regular-expressions.md)