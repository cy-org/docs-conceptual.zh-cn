---
title: "正则表达式中的编译和重复使用 | Microsoft Docs"
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
  - ".NET Framework 正则表达式, 编译"
  - ".NET Framework 正则表达式, 引擎"
  - "编译, 正则表达式"
  - "分析带有正则表达式的文本, 编译"
  - "正则表达式的模式匹配, 编译"
  - "正则表达式, 编译"
  - "正则表达式, 引擎"
  - "用正则表达式搜索, 编译"
ms.assetid: 182ec76d-5a01-4d73-996c-0b0d14fcea18
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# 正则表达式中的编译和重复使用
通过了解正则表达式引擎编译表达式的方式以及正则表达式的缓存方式，可以优化大量使用正则表达式的应用程序的性能。  本主题讨论编译和缓存。  
  
## 已编译的正则表达式  
 默认情况下，正则表达式引擎将正则表达式编译成内部指令序列（这些指令序列是不同于 Microsoft 中间语言 \(MSIL\) 的高级代码）。  当引擎执行正则表达式时，它解释该内部代码。  
  
 如果 <xref:System.Text.RegularExpressions.Regex> 对象是通过 <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> 选项构造的，则它会将正则表达式编译为显式 MSIL 代码，而非高级正则表达式内部指令。  这使 .NET Framework 的实时 \(JIT\) 编译器可以将表达式转换为本机代码以获得更高的性能。  
  
 但是，生成的 MSIL 不能被卸载。  卸载代码的唯一方法是卸载整个应用程序域（也就是说，卸载您的应用程序的所有代码）。  实际上，一旦用 <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> 选项编译了正则表达式，.NET Framework 就永远不会释放由编译的表达式使用的资源，即使创建该正则表达式的 <xref:System.Text.RegularExpressions.Regex> 对象本身已被释放并进行了垃圾回收，情况也是如此。  
  
 您必须注意限制用 <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> 选项编译的不同正则表达式的数目，以避免消耗过多的资源。  如果应用程序必须使用较大数量或极大数量的正则表达式，则应该解释每一表达式，而非编译它们。  但是，如果重复使用数目较少的正则表达式，则应使用 <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> 来编译它们，以获得更好的性能。  另外一个选择是使用预编译的正则表达式。  可以使用 <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A> 方法将所有表达式编译到一个可重用的 DLL 中。  这样就无需在运行时进行编译，同时仍可受益于已编译正则表达式的速度。  
  
## 正则表达式缓存  
 为了提高性能，正则表达式引擎为已编译的正则表达式维护了一个应用程序范围的缓存。  该缓存只存储静态方法调用中使用的正则表达式模式（提供给实例方法的正则表达式模式将不被缓存）。这样在每次使用正则表达式时，就无需将正则表达式重新分析成高级字节代码。  
  
 缓存的正则表达式的最大数目由 `static`（在 Visual Basic 中为 `Shared`）<xref:System.Text.RegularExpressions.Regex.CacheSize%2A?displayProperty=fullName> 属性的值决定。  默认情况下，正则表达式引擎最多可缓存 15 个已编译的正则表达式。  如果已编译正则表达式的数目超过缓存大小，则丢弃最早使用的正则表达式并缓存新的正则表达式。  
  
> [!IMPORTANT]
>  在 .NET Framework 2.0 版本中，正则表达式的缓存方式与 .NET Framework 1.0 和 1.1 版本中的行为明显不同。  在 .NET Framework 1.0 和 1.1 中，所有正则表达式都会被缓存，而不论它们是在静态方法调用中使用的，还是在实例方法调用中使用的。  缓存会自动扩展以存储新的正则表达式。  而在 .NET Framework 2.0 中，只有静态方法调用中使用的正则表达式才会被缓存。  默认情况下会缓存最后 15 个正则表达式，但是缓存的大小可通过设置 <xref:System.Text.RegularExpressions.Regex.CacheSize%2A> 属性的值加以调整。  
  
 您的应用程序可通过以下两种方式之一来利用预编译的正则表达式：  
  
-   通过使用 <xref:System.Text.RegularExpressions.Regex> 对象的静态方法定义正则表达式。  如果要使用的正则表达式模式已在其他静态方法调用中定义，则正则表达式引擎将从缓存中检索该模式。  如果不是这样，则引擎将编译正则表达式并将其添加到缓存中。  
  
-   通过重用现有的 <xref:System.Text.RegularExpressions.Regex> 对象（在需要使用其正则表达式模式时）。  
  
 由于对象实例化和正则表达式编译会产生大量的系统开销，因此创建大量 <xref:System.Text.RegularExpressions.Regex> 对象并迅速销毁它们的过程将占用大量的资源。  对于使用大量不同正则表达式的应用程序，可通过调用静态方法 `Regex` 并尽量增加正则表达式缓存的大小来优化其性能。  
  
## 请参阅  
 [.NET Framework 正则表达式](../../../docs/standard/base-types/regular-expressions.md)