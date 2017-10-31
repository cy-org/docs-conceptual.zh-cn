---
title: "类和结构之间进行选择 | Microsoft Docs"
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
  - "类库设计准则 [.NET Framework] 结构"
  - "类库设计准则 [.NET Framework] 类"
  - "与类的结构 [.NET Framework]"
  - "类 [.NET Framework] 设计准则"
  - "类型设计准则结构"
  - "结构 [.NET Framework] 设计准则"
  - "与结构类 [.NET Framework]"
  - "类型设计准则类"
ms.assetid: f8b8ec9b-0ba7-4dea-aadf-a93395cd804f
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# 类和结构之间进行选择
每个框架设计器所面临的基本设计决策之一是设计一种类型作为类 （引用类型） 还是为结构 （值类型）。 好地理解的引用类型和值类型的行为差异是做出此选择中至关重要的。  
  
 引用类型和值类型，我们将考虑第一个区别是引用类型是在堆上分配和垃圾回收，而值类型为分配堆栈或以内联形式在包含类型上并在堆栈展开时释放，或者当其包含类型获取已释放。 因此，分配和释放的值类型是在常规价格低于分配和释放的引用类型。  
  
 接下来，引用类型的数组分配行，这意味着的数组元素是对驻留在堆上的引用类型的实例的只是引用。 以内联方式，这意味着数组元素值类型的实际实例所分配值类型数组。 因此，分配和释放的值类型数组将比分配和释放的引用类型数组的便宜得多。 此外，在大多数情况下值类型数组表现出多更好的引用地址。  
  
 下一个差异与内存使用量。 获取装箱值类型，当强制转换为引用类型或它们实现的接口之一。 他们获得未装箱时将强制转换回值类型。 因为框是在堆上分配，它们是作为垃圾回收、 过多装箱和取消装箱的对象可以对堆、 垃圾回收器，并最终应用程序性能的负面影响。  与此相反，没有这种值类型装箱时间那样引用类型强制转换。  
  
 接下来，引用类型分配复制该引用，而值类型分配复制的整个值。 因此，较大的引用类型的分配都比大型值类型的分配成本更低。  
  
 最后，引用类型是通过引用传递，而通过值传递的值类型。 引用类型的实例的更改会影响指向实例的所有引用。 通过值传递时，并复制值类型实例。 值类型的实例进行更改时，它当然不会影响任何其副本。 由于副本很不由用户显式创建，而隐式创建的参数传递或返回值返回时，可以更改的值类型可以是给许多用户造成混淆。 因此，值类型应具有永久性。  
  
 一条经验法则，大部分框架中的类型应该是类。 有，但是，某些情况下，在其中值类型的特性使其更适合使用结构。  
  
 **✓ 请考虑** 定义一个结构，而不是类，如果该类型的实例很小，通常生存期短或嵌入在其他对象中。  
  
 **X 避免** 定义结构，除非该类型具有所有以下特征︰  
  
-   它在逻辑上表示单个值，类似于基元类型 \(`int`, ，`double`, ，等等。\)。  
  
-   它具有实例大小小于 16 字节。  
  
-   它是不可变。  
  
-   它不需要频繁地进行装箱。  
  
 在所有其他情况下，您应为类定义您的类型。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [类型设计准则](../../../docs/standard/design-guidelines/type.md)   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)