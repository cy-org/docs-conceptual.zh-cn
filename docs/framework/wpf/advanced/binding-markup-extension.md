---
title: "绑定标记扩展 | Microsoft Docs"
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
  - "Binding"
helpviewer_keywords: 
  - "绑定标记扩展"
  - "XAML, 绑定标记扩展"
ms.assetid: 83d6e2a4-1b0c-4fc8-bd96-b5e98800ab63
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# 绑定标记扩展
将属性值推迟为数据绑定值，从而在运行时创建一个中间表达式对象，并解释应用于元素及其绑定的数据上下文。  
  
## Binding 表达式用法  
  
```  
<object property="{Binding}" .../>  
-or-  
<object property="{Binding  bindProp1=value1[, bindPropN=valueN]*}" ...  
/>  
-or-  
<object property="{Binding path}" .../>  
-or  
<object property="{Binding path[, bindPropN=valueN]*}" .../>  
```  
  
## 语法说明  
 在这些语法中，`[]` 和 `*` 不是文本。  它们是一种准 BNF 表示法，用来指示可以使用零个或多个*绑定属性*`=`*值* 对，*绑定属性*`=`*值* 对之间用 `,` 分隔符隔开。  
  
 “可以使用绑定扩展设置的绑定属性”一节中列出的任何属性都可以改用 <xref:System.Windows.Data.Binding> 对象元素的特性来设置。  但是，这并非真正意义上 <xref:System.Windows.Data.Binding> 的标记扩展用法，而只是设置 CLR <xref:System.Windows.Data.Binding> 类属性的特性的一般 XAML 处理。  换句话说，`<Binding` *绑定属性1*`="`*值1*`"[` *绑定属性N*`="`*值N*`"]*/>` 是 <xref:System.Windows.Data.Binding> 对象元素用法（而不是 `Binding` 表达式用法）中特性的等效准语法。  若要了解 <xref:System.Windows.Data.Binding> 的特定属性的 XAML 特性用法，请参见 .NET Framework 类库中 <xref:System.Windows.Data.Binding> 的相关属性的“XAML 特性用法”部分。  
  
## XAML 值  
  
|||  
|-|-|  
|`bindProp1, bindPropN`|要设置的 <xref:System.Windows.Data.Binding> 或 <xref:System.Windows.Data.BindingBase> 属性的名称。  并非所有 <xref:System.Windows.Data.Binding> 属性都可以使用 `Binding` 扩展来设置，某些属性只能在 `Binding` 表达式中使用更丰富的嵌套标记扩展来设置。  请参见“可以使用绑定扩展设置的绑定属性”一节。|  
|`value1, valueN`|属性的设置值。  特性值的处理最终特定于所设置的特定 <xref:System.Windows.Data.Binding> 属性的类型和逻辑。|  
|`path`|设置隐式 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=fullName> 属性的路径字符串。  另请参见[PropertyPath XAML 语法](../../../../docs/framework/wpf/advanced/propertypath-xaml-syntax.md)。|  
  
## 非限定 {Binding}  
 “绑定表达式用法”中介绍的 `{Binding}` 用法使用默认值创建 <xref:System.Windows.Data.Binding> 对象，其中包括的 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=fullName> 初始值为 `null`。  这在很多情况下仍然有用，因为所创建的 <xref:System.Windows.Data.Binding> 可能依赖于关键数据绑定属性，例如在运行时数据上下文中所设置的 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=fullName> 和 <xref:System.Windows.Data.Binding.Source%2A?displayProperty=fullName>。  有关数据上下文概念的更多信息，请参见[数据绑定](../../../../docs/framework/wpf/data/data-binding-wpf.md)。  
  
## 隐式路径  
 `Binding` 标记扩展使用 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=fullName> 作为概念上的“默认属性”，其中 `Path=` 不需要出现在表达式中。  如果以隐式路径指定 `Binding` 表达式，则隐式路径必须位于表达式的最前面，即位于其他任何按名称指定 <xref:System.Windows.Data.Binding> 属性的 `bindProp`\=`value` 对之前。  例如：`{Binding PathString}`，其中 `PathString` 是一个字符串，其值为由标记扩展用法创建的 <xref:System.Windows.Data.Binding> 中的 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=fullName> 值。  可以在隐式路径后依次追加逗号分隔符和其他命名属性，例如 `{Binding LastName, Mode=TwoWay}`。  
  
## 可以使用绑定扩展设置的绑定属性  
 本主题介绍的语法使用泛型 `bindProp`\=`value` 的近似形式，因为 <xref:System.Windows.Data.BindingBase> 或 <xref:System.Windows.Data.Binding> 的许多读\/写属性可以通过 `Binding` 标记扩展\/表达式语法来设置。  可以按任何顺序设置这些属性，但隐式 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=fullName> 除外。  （您可以显式指定 `Path=`，在这种情况下可以按任何顺序对其进行设置。）  一般说来，可以使用逗号分隔的 `bindProp`\=`value` 对来设置下面列表中的零个或多个属性。  
  
 其中几个属性值需要不支持本机类型转换的对象类型，因此需要更丰富的标记扩展用法才能在 XAML 中设置为特性值。  有关每个属性的更多信息，请查看 .NET Framework 类库中的“XAML 特性用法”部分；带有或不带有更丰富标记扩展用法的 XAML 特性语法所使用的字符串基本上与 `Binding` 表达式中指定的值相同，不同之处在于 `Binding` 表达式中的每个 `bindProp`\=`value` 两边不带引号。  
  
-   <xref:System.Windows.Data.BindingBase.BindingGroupName%2A>：一个字符串，标识可能的绑定组。  这是一个相对高级的绑定概念；请参见 <xref:System.Windows.Data.BindingBase.BindingGroupName%2A> 的参考页。  
  
-   <xref:System.Windows.Data.Binding.BindsDirectlyToSource%2A>：布尔值，可以为 `true` 或 `false`。  默认值为 `false`。  
  
-   <xref:System.Windows.Data.Binding.Converter%2A>：可在表达式中设置为 `bindProp`\=`value` 字符串，但是这样做将需要值的对象引用，如 [StaticResource 标记扩展](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)。  在这种情况下，该值是自定义转换器类的一个实例。  
  
-   <xref:System.Windows.Data.Binding.ConverterCulture%2A>：可在表达式中设置为基于标准的标识符；请参见 <xref:System.Windows.Data.Binding.ConverterCulture%2A> 的参考主题。  
  
-   <xref:System.Windows.Data.Binding.ConverterParameter%2A>：可在表达式中设置为 `bindProp`\=`value` 字符串，但这依赖于所传递的参数的类型。  如果为值传递一个引用类型，则需要对象引用，如嵌套的 [StaticResource 标记扩展](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)。  
  
-   <xref:System.Windows.Data.Binding.ElementName%2A>：与 <xref:System.Windows.Data.Binding.RelativeSource%2A> 和 <xref:System.Windows.Data.Binding.Source%2A> 互斥；上述每个绑定属性都代表一种特定的绑定方法。  请参见 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。  
  
-   <xref:System.Windows.Data.BindingBase.FallbackValue%2A>：可在表达式中设置为 `bindProp`\=`value` 字符串，但这依赖于所传递的值的类型。  如果传递一个引用类型，则需要对象引用，如嵌套的 [StaticResource 标记扩展](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)。  
  
-   <xref:System.Windows.Data.Binding.IsAsync%2A>：布尔值，可以为 `true` 或 `false`。  默认值为 `false`。  
  
-   <xref:System.Windows.Data.Binding.Mode%2A>：*值* 是 <xref:System.Windows.Data.BindingMode> 枚举中的一个常量名称。  例如 `{Binding Mode=OneWay}`。  
  
-   <xref:System.Windows.Data.Binding.NotifyOnSourceUpdated%2A>：布尔值，可以为 `true` 或 `false`。  默认值为 `false`。  
  
-   <xref:System.Windows.Data.Binding.NotifyOnTargetUpdated%2A>：布尔值，可以为 `true` 或 `false`。  默认值为 `false`。  
  
-   <xref:System.Windows.Data.Binding.NotifyOnValidationError%2A>：布尔值，可以为 `true` 或 `false`。  默认值为 `false`。  
  
-   <xref:System.Windows.Data.Binding.Path%2A>：一个字符串，描述到数据对象或常规对象模型的路径。  该格式提供了几种不同的遍历对象模型的约定，本主题无法对这些约定进行详细介绍。  请参见 [PropertyPath XAML 语法](../../../../docs/framework/wpf/advanced/propertypath-xaml-syntax.md)。  
  
-   <xref:System.Windows.Data.Binding.RelativeSource%2A>：与 <xref:System.Windows.Data.Binding.ElementName%2A> 和 <xref:System.Windows.Data.Binding.Source%2A> 互斥；上述每个属性都代表一种特定的绑定方法。  请参见 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。  需要嵌套的 [RelativeSource MarkupExtension](../../../../docs/framework/wpf/advanced/relativesource-markupextension.md)用法才能指定该值。  
  
-   <xref:System.Windows.Data.Binding.Source%2A>：与 <xref:System.Windows.Data.Binding.RelativeSource%2A> 和 <xref:System.Windows.Data.Binding.ElementName%2A> 互斥；上述每个绑定属性都代表一种特定的绑定方法。  请参见 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。  需要嵌套的扩展用法，通常是从键控资源字典引用对象数据源的 [StaticResource 标记扩展](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)。  
  
-   <xref:System.Windows.Data.BindingBase.StringFormat%2A>：一个字符串，描述绑定数据的字符串格式约定。  这是一个相对高级的绑定概念；请参见 <xref:System.Windows.Data.BindingBase.StringFormat%2A> 的参考页。  
  
-   <xref:System.Windows.Data.BindingBase.TargetNullValue%2A>：可在表达式中设置为 `bindProp`\=`value` 字符串，但这依赖于所传递的参数的类型。  如果为值传递一个引用类型，则需要对象引用，如嵌套的 [StaticResource 标记扩展](../../../../docs/framework/wpf/advanced/staticresource-markup-extension.md)。  
  
-   <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>：*值* 是 <xref:System.Windows.Data.UpdateSourceTrigger> 枚举中的一个常量名称。  例如 `{Binding UpdateSourceTrigger=LostFocus}`。  特定的控件可能具有与此绑定属性不同的默认值。  请参见 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>。  
  
-   <xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A>：布尔值，可以为 `true` 或 `false`。  默认值为 `false`。  请参见"备注"。  
  
-   <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A>：布尔值，可以为 `true` 或 `false`。  默认值为 `false`。  请参见"备注"。  
  
-   <xref:System.Windows.Data.Binding.XPath%2A>：一个字符串，描述到 XML 数据源的 XMLDOM 的路径。  请参见 [使用 XMLDataProvider 和 XPath 查询绑定到 XML 数据](../../../../docs/framework/wpf/data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)。  
  
 以下是无法使用 `Binding` 标记扩展\/`{Binding}` 表达式设置的 <xref:System.Windows.Data.Binding> 的属性。  
  
-   <xref:System.Windows.Data.Binding.UpdateSourceExceptionFilter%2A>：此属性需要对回调实现的引用。  不能在 XAML 语法中引用事件处理程序以外的回调\/方法。  
  
-   <xref:System.Windows.Data.Binding.ValidationRules%2A>：该属性接受 <xref:System.Windows.Controls.ValidationRule> 对象的泛型集合。  这可以表示为 <xref:System.Windows.Data.Binding> 对象元素中的属性元素，但对于 `Binding` 表达式中的用法，没有可直接使用的特性分析技术。  请参见 <xref:System.Windows.Data.Binding.ValidationRules%2A> 的参考主题。  
  
-   <xref:System.Windows.Data.Binding.XmlNamespaceManager%2A>  
  
## 备注  
  
> [!IMPORTANT]
>  在依赖项属性优先级方面，`Binding` 表达式等效于本地设置的值。  如果为先前已具有 `Binding` 表达式的属性设置了本地值，则会完全移除 `Binding`。  有关详细信息，请参见[依赖项属性值优先级](../../../../docs/framework/wpf/advanced/dependency-property-value-precedence.md)。  
  
 此主题不介绍在基本级别上描述数据绑定。  请参见 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。  
  
> [!NOTE]
>  <xref:System.Windows.Data.MultiBinding> 和 <xref:System.Windows.Data.PriorityBinding> 不支持 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 扩展语法。相反您会用到属性元素。  请参见 <xref:System.Windows.Data.MultiBinding> 和 <xref:System.Windows.Data.PriorityBinding> 的参考主题。  
  
 XAML 的布尔值不区分大小写。  例如，您可以指定 `{Binding NotifyOnValidationError=true}` 或 `{Binding NotifyOnValidationError=True}`。  
  
 通常由显式 `Binding` 元素而不是 `{Binding ...}` 表达式指定涉及数据有效性的绑定，而且在表达式中的设置 <xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A> 或 <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A> 并不常见。  这是因为配套属性 <xref:System.Windows.Data.Binding.ValidationRules%2A> 无法很容易地在表达式窗体中进行设置。  有关更多信息，请参见[实现绑定验证](../../../../docs/framework/wpf/data/how-to-implement-binding-validation.md)。  
  
 `Binding` 是标记扩展。  当要求转义特性值应为非文本值或非处理程序名称时，通常会实现标记扩展，相对于只在某些类型或属性上放置类型转换器而言，此要求更具有全局性。  XAML 中的所有标记扩展在其特性语法中都使用 `{` 和 `}` 字符，XAML 处理器通过这一约定识别出该字符串必须由标记扩展处理。  有关更多信息，请参见 [标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)。  
  
 `Binding` 是非典型标记扩展，因为实现 WPF 的 XAML 实现的扩展功能的 <xref:System.Windows.Data.Binding> 类还实现与 XAML 无关的其他一些方法和属性。  其他成员旨在令 <xref:System.Windows.Data.Binding> 成为功能更多且独立的类，除用作 XAML 标记扩展外，还可以满足许多数据绑定方案的需求。  
  
## 请参阅  
 <xref:System.Windows.Data.Binding>   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)