---
title: "参数设计 | Microsoft Docs"
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
  - "成员设计准则 [.NET Framework] 参数"
  - "参数的成员 [.NET Framework]"
  - "参数的名称 [.NET Framework]"
  - "参数，设计准则"
  - "保留的参数"
ms.assetid: 3f33bf46-4a7b-43b3-bb78-1ffebe0dcfa6
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# 参数设计
本部分提供全面的指南参数的设计方案，其中包括用于检查参数的指导原则的部分。 此外，您应该参考中所述的准则 [命名参数](../../../docs/standard/design-guidelines/naming-parameters.md)。  
  
 **✓ 执行** 使用派生程度最低参数提供的类型的成员所需的功能。  
  
 例如，假设您希望设计枚举集合，并输出到控制台的每个项的方法。 这种方法应接受 <xref:System.Collections.IEnumerable> 作为参数，不 <xref:System.Collections.ArrayList> 或 <xref:System.Collections.IList>, ，例如。  
  
 **X 不** 使用保留的参数。  
  
 如果某些未来版本中需要更多输入成员，则可以添加的新重载。  
  
 **X 不** 已公开的指针、 数组的指针或多维数组作为参数的方法。  
  
 指针和多维数组是相对较难正确使用。 在几乎所有情况下，可以重新设计的 Api 来避免这些类型作为参数。  
  
 **✓ 执行** 放置所有 `out` 后所有按值的参数和 `ref` 参数 （不包括参数数组），即使这会导致在重载间排序的参数中存在不一致 \(请参阅 [对成员进行重载](../../../docs/standard/design-guidelines/member-overloading.md)\)。  
  
 `out` 参数可将其视为额外返回值，并将它们组合在一起使方法签名易于理解。  
  
 **✓ 执行** 命名参数，当重写成员或实现接口成员中保持一致。  
  
 这更好地进行通信的方法之间的关系。  
  
### 枚举和布尔参数之间进行选择  
 **✓ 执行** 如果成员本来有两个或多个布尔参数，请使用枚举。  
  
 **X 不** 使用布尔值，除非您确信绝对不会对两个以上值的需求。  
  
 枚举为您提供一些空间以便将来添加值，但您一定要注意的将值添加到枚举中所述的所有隐患 [枚举设计](../../../docs/standard/design-guidelines/enum.md)。  
  
 **✓ 请考虑** 使用的是真正的二态值，只需用来初始化布尔型属性构造函数参数的布尔值。  
  
### 验证参数  
 **✓ 执行** 验证传递给公共、 受保护，或显式实现的成员的参数。 引发 <xref:System.ArgumentException?displayProperty=fullName>, ，或一个子类，如果验证失败。  
  
 请注意，实际验证不一定有发生这种情况在公共或受保护成员本身中。 它可能在某些私有或内部的例程中较低级别。 主要目的是提供给最终用户的整个表面区域，会检查参数。  
  
 **✓ 执行** 引发 <xref:System.ArgumentNullException> 如果 null 参数进行传递，并且该成员不支持 null 参数。  
  
 **✓ 执行** 验证枚举参数。  
  
 不要假定 enum 参数会在枚举定义范围内。 CLR 允许任何整数值转换为枚举值，即使未在枚举中定义的值。  
  
 **X 不** 使用 <xref:System.Enum.IsDefined%2A?displayProperty=fullName> 枚举范围进行检查。  
  
 **✓ 执行** 请注意，在经过验证后，可能已更改可变参数。  
  
 如果该成员是敏感的安全，我们鼓励您在制作副本，然后验证和处理参数。  
  
### 参数传递  
 从框架设计器的角度来看，有以下三个主要组的参数︰ 通过值传递参数， `ref` 参数，并 `out` 参数。  
  
 当通过按值参数传递的参数，则该成员会收到一份中传递的实参。 如果参数是值类型，则参数的副本将放在堆栈上。 如果参数为引用类型，引用的副本将放在堆栈上。 最常用的 CLR 语言，如 C\#、 VB.NET 和 c \+ \+，默认情况下按值传递参数。  
  
 当参数传递通过 `ref` 参数，该成员会接收对传入的实际参数的引用。 如果参数是值类型，对参数的引用放在堆栈上。 如果参数为引用类型，对该引用的引用放在堆栈上。`Ref` 可以使用参数，以便成员可以修改由调用方传递的参数。  
  
 `Out` 参数是类似于 `ref` 参数，但存在一些小的差异。 该参数最初被认为是未分配和之前向其分配某些值不能读取成员正文中。 此外，该参数必须被分配一些值，才能成员将返回。  
  
 **X 避免** 使用 `out` 或 `ref` 参数。  
  
 使用 `out` 或 `ref` 参数要求具有使用指针，了解值类型和引用类型的不同之处，以及能处理具有多个返回值的方法的体验。 此外，之间的差异 `out` 和 `ref` 参数没有得到广泛了解。 为一般用户设计的框架架构师不应指望用户掌握了 `out` 或 `ref` 参数。  
  
 **X 不** 通过引用传递引用类型。  
  
 有几种有限的例外规则，例如，可用于交换引用的方法。  
  
### 具有可变数目的参数的成员  
 可以采用可变数量的参数的成员表示通过提供的数组参数。 例如， <xref:System.String> 提供以下方法︰  
  
```  
public class String {  
    public static string Format(string format, object[] parameters);  
}  
```  
  
 然后，用户可以调用 <xref:System.String.Format%2A?displayProperty=fullName> 方法，如下所示︰  
  
 `String.Format("File {0} not found in {1}",new object[]{filename,directory});`  
  
 将 C\# params 关键字添加到的数组参数更改为所谓的参数数组参数的参数，并提供创建临时数组的快捷方式。  
  
```  
public class String {  
    public static string Format(string format, params object[] parameters);  
}  
```  
  
 执行此操作允许用户通过直接在参数列表中传递的数组元素调用该方法。  
  
 `String.Format("File {0} not found in {1}",filename,directory);`  
  
 请注意 params 关键字，可以添加仅对在参数列表中的最后一个参数。  
  
 **✓ 请考虑** 将 params 关键字添加到数组参数中，如果您希望最终用户将与少量的元素的数组传递。 如果期望，大量元素将传递在常见方案，用户可能不会传递这些元素内联不管怎样，并因此没有必要 params 关键字。  
  
 **X 避免** 使用参数数组，如果调用方将几乎总是具有输入已经在数组中。  
  
 例如，通过将单个字节几乎从不会调用通过字节数组参数的成员。 出于此原因，.NET Framework 中的字节数组参数不要使用 params 关键字。  
  
 **X 不** 如果数组修改成员采用 params 数组参数使用 params 数组。  
  
 由于许多编译器写入临时数组中的调用站点处打开该成员的参数，该数组可能是临时对象，并因此对数组进行任何修改都将丢失。  
  
 **✓ 请考虑** 使用 params 关键字在简单的重载中，即使更复杂的重载不能使用它。  
  
 问问自己，是否用户将采用一个重载的参数数组，即使它不是所有重载中的值。  
  
 **✓ 执行** 尝试于订单参数，以使其可以使用 params 关键字。  
  
 **✓ 请考虑** 调用只有少量极性能敏感的 Api 中的参数提供特殊重载和代码路径。  
  
 这样可以避免使用少量的参数调用 API 时创建的数组对象。 通过采用数组参数的单数形式，并添加数值后缀而形成的参数的名称。  
  
 只有当将特殊设置这样的整个代码路径，而不仅仅是创建数组，并调用更常用的方法的保护时，才应该这样做。  
  
 **✓ 执行** 注意可以作为参数数组参数中传递 null。  
  
 您应验证数组不在处理之前为 null。  
  
 **X 不** 使用 `varargs` 方法，也称为省略号。  
  
 某些 CLR 语言，例如，c \+ \+ 支持备用约定传递变量参数列表调用 `varargs` 方法。 约定不应在框架，因为它不是符合 CLS。  
  
### 指针参数  
 一般情况下，指针不应出现在一个设计良好的托管的代码的框架的公共外围应用。 大多数情况下，应封装的指针。 但是，在某些情况下指针所需的互操作性方面的考虑，并且才适合这种情况下使用指针。  
  
 **✓ 执行** 为采用一个指针作为参数，任何成员提供一种替代方法，因为指针不是符合 CLS。  
  
 **X 避免** 执行高开销检查的指针参数的参数。  
  
 **✓ 执行** 设计具有使用指针的成员时遵循公共指针相关的约定。  
  
 例如，没有必要将传递的起始索引，因为可以使用简单指针算法来达到相同的结果。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [成员设计准则](../../../docs/standard/design-guidelines/member.md)   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)