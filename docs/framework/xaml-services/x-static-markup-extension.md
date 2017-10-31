---
title: "x:Static Markup Extension | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "StaticExtension"
  - "xStatic"
  - "x:Static"
helpviewer_keywords: 
  - "x:Static markup extension [XAML Services]"
  - "Static markup extension in XAML [XAML Services]"
  - "XAML [XAML Services], x:Static markup extension"
ms.assetid: 056aee79-7cdd-434f-8174-dfc856cad343
caps.latest.revision: 25
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 25
---
# x:Static Markup Extension
按值引用以符合 [!INCLUDE[TLA#tla_cls](../../../includes/tlasharptla-cls-md.md)] 的方式定义的任何静态代码实体。  引用的静态属性可以用来提供在 XAML 中的属性的值。  
  
## XAML 属性用法  
  
```  
<object property="{x:Static prefix:typeName.staticMemberName}" .../>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`prefix`|可选。  引用映射的非默认 XAML 命名空间的前缀。  `prefix` 在该用法中显式表示，这是因为您很少引用来自默认 XAML 命名空间的静态属性。  请参见"备注"。|  
|`typeName`|必选。  定义所需静态成员类型的名称。|  
|`staticMemberName`|必选。  所需的静态值成员的名称（常量、静态属性、字段或枚举值）。|  
  
## 备注  
 引用的代码实体必须是下面的某一项：  
  
-   常数  
  
-   静态属性  
  
-   字段  
  
-   一个枚举值。  
  
 指定任何其他代码实体（例如一个非静态属性）时，将导致编译时错误（如果标记编译 XAML），或 XAML 加载时间分析异常。  
  
 可以为当前 XAML 文档对不在默认 XAML 命名空间中的静态字段或属性进行 `x:Static` 引用，但这需要前缀映射。  几乎总是在 XAML 文档的根元素上定义 XAML 命名空间。  
  
 当它们与默认 XAML 架构上下文一起运行时，对静态属性的查找操作可以由 .NET Framework XAML 服务及其 XAML 读取器和 XAML 编写器执行。  此 XAML 架构上下文可以使用 CLR 反射来为对象图构造提供必要的静态值。  您指定的 `typeName` 实际上是一个 XAML 类型名称，而不是 CLR 类型的名称，虽然这在使用默认的 XAML 架构上下文或所有现有基于 CLR 的 XAML 实施框架时是本质上相同的名称。  
  
 在进行并非直接是属性值的类型的 `x:Static` 引用时要谨慎。  在 XAML 处理序列中，从标记扩展提供的值不调用其他值转换。  即使您的 `x:Static` 引用创建了文本字符串，也是如此，且基于文本字符串的特性值的值转换通常针对特定成员发生，或针对返回类型的任何成员值发生。  
  
 特性语法是最常用于此标记扩展的语法。  在 `x:Static` 标识符字符串之后提供的字符串标记被指定为基础 <xref:System.Windows.Markup.StaticExtension> 扩展类的 <xref:System.Windows.Markup.StaticExtension.Member%2A> 值。  
  
 技术上，有其他两个可能的 XAML 用法。  但是，这些用法并不常见，因为它们不必太详细：  
  
 **对象元素语法：** `<x:Static Member="``prefix``:``typeName``.``staticMemberName``" .../>`  
  
 **包含初始化字符串显示成员属性的特性语法：** `<``object````property``="{x:Static Member=``prefix``:``typeName``.``staticMemberName``}" .../>`  
  
 在 .NET Framework XAML 服务实现中，对此标记扩展的处理由 <xref:System.Windows.Markup.StaticExtension> 类定义。  
  
 `x:Static` 是标记扩展。  XAML 中的所有标记扩展在其特性语法中都使用 `{` 和 `}` 字符，XAML 处理器通过这一约定识别出标记扩展必须提供一个值。  有关标记扩展的更多信息，请参见[Markup Extensions for XAML Overview](../../../docs/framework/xaml-services/markup-extensions-for-xaml-overview.md)。  
  
## WPF 用法说明  
 用于 WPF 编程的默认 XAML 命名空间不包含许多有用的静态属性，且大多数有用静态属性有支持，例如不需要请求 `{x:Static}` 就可以对该用法有帮助的类型转换器。  对于静态属性，如果以下值之一为 true，则您必须为 XAML 命名空间映射一个前缀：  
  
-   您所引用的类型存在于 WPF 中，但不属于用于 WPF \([!INCLUDE[TLA#tla_wpfxmlnsv1](../../../includes/tlasharptla-wpfxmlnsv1-md.md)]\) 的默认 XAML 命名空间的一部分。  这是一种非常常见的使用 `x:Static` 的情况。  例如，可以将 `x:Static` 引用与映射到 <xref:System> CLR 命名空间和 mscorlib 程序集的 XAML 命名空间一起使用，以便引用 <xref:System.Environment> 类的静态属性。  
  
-   您从自定义程序集引用类型。  
  
-   您所引用的类型存在于 WPF 程序集中，但该类型所在的 CLR 命名空间未映射为 WPF 默认 XAML 命名空间的一部分。  CLR 命名空间到用于 WPF 的默认 XAML 命名空间的映射可以由多种 WPF 程序集中的定义来执行（有关此概念的详细信息，请参见 [WPF XAML 的 XAML 命名空间和命名空间映射](../../../ocs/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)）。  如果 CLR 命名空间大部分由通常不用于 XAML 的类定义（如 <xref:System.Windows.Threading>）组成，则未映射的 CLR 命名空间可能存在。  
  
 有关如何使用前缀和 WPF 的 XAML 命名空间的更多信息，请参见 [WPF XAML 的 XAML 命名空间和命名空间映射](../../../ocs/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)。  
  
## 请参阅  
 [x:Type Markup Extension](../../../docs/framework/xaml-services/x-type-markup-extension.md)   
 [Types Migrated from WPF to System.Xaml](../../../docs/framework/xaml-services/types-migrated-from-wpf-to-system-xaml.md)