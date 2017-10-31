---
title: "x:Array Markup Extension | Microsoft Docs"
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
  - "x:Array"
  - "xArray"
helpviewer_keywords: 
  - "x:Array [XAML Services]"
  - "XAML [XAML Services], x:Array markup extension"
ms.assetid: c5358e14-d24c-44c7-b5eb-6062a4fd981c
caps.latest.revision: 20
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 20
---
# x:Array Markup Extension
通过标记扩展，对 XAML 中的对象组提供一般支持。  这对应于 \[MS\-XAML\] 中的 `x:ArrayExtension` XAML 类型。  
  
## XAML 对象元素用法  
  
```  
<x:Array Type="typeName">  
  arrayContents  
</x:Array>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`typeName`|您的 `x:Array` 将要包含的类型的名称。  `typeName` 可能（而且通常）为包含 XAML 类型定义的 XAML 命名空间带前缀。|  
|`arrayContents`|分配给内在 `ArrayExtension.Items` 属性的项内容。  通常，这些项被指定为包含在 `x:Array` 开始标记和结束标记内的一个或多个对象元素。  此处指定的对象应可以分配给 `typeName` 中指定的 XAML 类型。|  
  
## 备注  
 `Type` 对于所有 `x:Array` 对象元素是必需的特性。  `Type` 参数值不需要使用 `x:Type` 标记扩展；该类型的短名称为 XAML 类型，可将其指定为字符串。  
  
 在 .NET Framework XAML 服务实现中，已创建数组的输入 XAML 类型与输出 CLR <xref:System.Type> 之间的关系受标记扩展名的影响。  根据 XAML 架构上下文查找必需的 <xref:System.Xaml.XamlType> 和上下文提供的 <xref:System.Windows.Markup.IXamlTypeResolver> 服务后，输出 <xref:System.Type> 是输入 XAML 类型的 <xref:System.Xaml.XamlType.UnderlyingType%2A>。  
  
 当处理时，数组内容被分配给 `ArrayExtension.Items` 内部属性。  在 <xref:System.Windows.Markup.ArrayExtension> 实现中，这由 <xref:System.Windows.Markup.ArrayExtension.Items%2A?displayProperty=fullName> 表示。  
  
 在 .NET Framework XAML 服务实现中，对此标记扩展的处理由 <xref:System.Windows.Markup.ArrayExtension> 类定义。  <xref:System.Windows.Markup.ArrayExtension> 未密封，可用作自定义数组类型的标记扩展实现的基础。  
  
 `x:Array` 更主要的用途是用于 XAML 中的通用语言扩展性。  但是 `x:Array` 还可以用于使用指定某些属性的 XAML 值，这些属性将 XAML 支持的集合用作结构化属性内容。  例如，您可以通过 `x:Array` 用法指定 <xref:System.Collections.IEnumerable> 属性的内容。  
  
 `x:Array` 是标记扩展。  当要求转义属性 \(Attribute\) 值应为非文本值或非处理程序名称时，通常会实现标记扩展，相对于只在某些类型或属性 \(Property\) 上放置类型转换器而言，此要求更具有全局性。  `x:Array` 在是部分规则的例外，因为 `x:Array` 没有提供另类特性值处理，而是提供其内部文本内容的另类处理。  此行为启用可能不受将归组到数组的现有上下文模型支持及稍后通过访问命名数组在代码后置中加以引用的类型；您可以调用 <xref:System.Array> 方法来获取单独的数组项。  
  
 XAML 中的所有标记扩展在其属性语法中都使用大括号 \({,}`)`，XAML 处理器通过这一约定识别出该属性值必须由标记扩展处理。  有关标记扩展的更多一般信息，请参见 [Type Converters and Markup Extensions for XAML](../../../docs/framework/xaml-services/type-converters-and-markup-extensions-for-xaml.md)。  
  
 在 XAML 2009 `x:Array` 被定义为一种语言基元，而不是标记扩展。  有关更多信息，请参见 [Built\-in Types for Common XAML Language Primitives](../../../docs/framework/xaml-services/built-in-types-for-common-xaml-language-primitives.md)。  
  
## WPF 用法说明  
 通常情况下，填充 `x:Array` 的对象元素不是存在于 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] XAML 命名空间中的元素，需要一个到非默认 XAML 命名空间的前缀映射。  
  
 例如，下面是由两个字符串组成的简单数组，并在数组级别定义了 `sys` 前缀（以及 `x`）。  
  
 \[xaml\]  
  
 `<x:Array Type="sys:String" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`  
  
 `xmlns:sys="clr-namespace:System;assembly=mscorlib">`  
  
 `<sys:String>Hello</sys:String>`  
  
 `<sys:String>World</sys:String>`  
  
 `</x:Array>`  
  
 对于用作数组元素的自定义类型，类还必须支持在 XAML 中作为对象元素实例化的要求。  有关更多信息，请参见 [XAML 及 WPF 的自定义类](../../../ocs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)。  
  
## 请参阅  
 [标记扩展和 WPF XAML](../../../ocs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)   
 [Types Migrated from WPF to System.Xaml](../../../docs/framework/xaml-services/types-migrated-from-wpf-to-system-xaml.md)