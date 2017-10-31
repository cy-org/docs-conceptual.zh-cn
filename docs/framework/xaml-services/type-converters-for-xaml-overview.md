---
title: "Type Converters for XAML Overview | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "XAML [XAML Services], type converters"
  - "XAML [XAML Services], TypeConverter"
  - "type conversion for XAML [XAML Services]"
ms.assetid: 51a65860-efcb-4fe0-95a0-1c679cde66b7
caps.latest.revision: 14
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 14
---
# Type Converters for XAML Overview
类型转换器为对象编写器提供逻辑，用于从 XAML 标记中的字符串转换为对象图中的特定对象。 在 .NET Framework XAML 服务中，类型转换器必须是派生自 <xref:System.ComponentModel.TypeConverter> 的类。 某些转换器还支持 XAML 保存路径，可以用于将对象从序列化标记序列化为字符串形式。 本主题介绍如何以及何时调用 XAML 中的类型转换器，以及为 <xref:System.ComponentModel.TypeConverter> 的方法重写提供实现建议。  
  
<a name="type_conversion_concepts"></a>   
## 类型转换概念  
 以下各节介绍有关 XAML 如何使用字符串，以及 .NET Framework XAML 服务中的对象编写器如何使用类型转换器处理在 XAML 源中遇到的某些字符串值的基本概念。  
  
### XAML 和字符串值  
 在 XAML 文件中设置特性值时，该值的初始类型在一般意义上是字符串，在 XML 意义上是字符串特性值。 甚至其他基元（如 <xref:System.Double>）最初对于 XAML 处理器都是字符串。  
  
 在大多数情况下，XAML 处理器需要两条信息来处理特性值。 第一条信息是所设置的属性的值类型。 定义特性值以及在 XAML 中进行处理的任何字符串都必须最终转换或解析为该类型的值。 如果值是 XAML 分析器可理解的基元（如数值），则会尝试直接转换字符串。 如果特性的值引用枚举，则会检查提供的字符串中是否存在与该枚举中的命名常量匹配的名称。 如果值既不是分析器可理解的基元，也不是枚举中的常量名，则适用的类型必须能够提供基于转换后的字符串的值或引用。  
  
> [!NOTE]
>  XAML 语言指令不使用类型转换器。  
  
### 类型转换器和标记扩展  
 标记扩展用法必须先由 XAML 处理器进行处理，然后才能检查属性类型和其他注意事项。 例如，如果设置为特性的属性通常具有类型转换，但在特定情况下通过标记扩展用法进行设置，则标记扩展行为会首先进行处理。 需要标记扩展的一种常见情况是使对已存在的对象进行引用。 对于这种情况，无状态类型转换器只能生成新实例，这可能并不理想。 有关标记扩展的详细信息，请参阅 [Markup Extensions for XAML Overview](../../../docs/framework/xaml-services/markup-extensions-for-xaml-overview.md)。  
  
### 本机类型转换器  
 在 WPF 和 .NET XAML 服务实现中，某些 CLR 类型具有本机类型转换处理，但是，这些 CLR 类型不会按惯例视为基元。 这种类型的一个示例是 <xref:System.DateTime>。 造成这种情况的原因之一是 .NET Framework 体系结构的工作原理：类型 <xref:System.DateTime> 在 mscorlib（.NET 中最基本的库中）中定义。 不允许 <xref:System.DateTime> 使用来自引入依赖关系的另一个程序集的特性进行特性化（<xref:System.ComponentModel.TypeConverterAttribute> 来自系统）；因此，无法支持通过特性化进行的正常类型转换器发现机制。 相反，XAML 分析器具有需要本机处理的类型的列表，它可通过与真正基元的处理方式类似的方式来处理这些类型。 对于 <xref:System.DateTime>，这种处理涉及调用 <xref:System.DateTime.Parse%2A>。  
  
<a name="Implementing_a_Type_Converter"></a>   
## 实现类型转换器  
 以下各节讨论 <xref:System.ComponentModel.TypeConverter> 类的 API。  
  
### TypeConverter  
 在 .NET Framework XAML 服务下，用于 XAML 用途的所有类型转换器都是从基类 <xref:System.ComponentModel.TypeConverter> 派生的类。<xref:System.ComponentModel.TypeConverter> 类在 XAML 出现之前便存在于 .NET Framework 各版本中；原始 <xref:System.ComponentModel.TypeConverter> 方案之一是在可视化设计器中为属性编辑器提供字符串转换。  
  
 对于 XAML，<xref:System.ComponentModel.TypeConverter> 的角色已进行了扩展。 对于 XAML 用途，<xref:System.ComponentModel.TypeConverter> 是用于为某些变为字符串和源自字符串转换提供支持的基类。 通过源自字符串转换可从 XAML 分析字符串特性值。 通过变为字符串转换可处理特定对象属性的运行时值以恢复为 XAML 中的特性，从而实现序列化。  
  
 <xref:System.ComponentModel.TypeConverter> 定义了四个成员，它们对于针对 XAML 处理用途的转换为字符串和从字符串转换是相关的：  
  
-   <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A>  
  
-   <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A>  
  
-   <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>  
  
-   <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>  
  
 在这些成员中，最重要的方法是 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>，它将输入字符串转换为所需的对象类型。 可以实现 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 方法以将更广泛的类型转换为转换器的预期目标类型。 因此，它可以实现扩展到 XAML 外部的用途，如支持运行时转换。 但是，对于 XAML 使用，只有可以处理 <xref:System.String> 输入的代码路径才十分重要。  
  
 第二重要的方法是 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>。 如果应用程序转换为标记表示形式（例如，如果将它作为文件保存到 XAML），则在生成标记表示形式的 XAML 文本编写器的较大方案中会涉及到 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>。 在这种情况下，XAML 的重要代码路径是调用方何时传递 <xref:System.String> 的 `destinationType`。  
  
 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 和 <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> 是在服务查询 <xref:System.ComponentModel.TypeConverter> 实现的功能时使用的支持方法。 必须实现这些方法以便为转换器的等效转换方法支持的特定于类型的情况返回 `true`。 对于 XAML 用途，这通常意味着 <xref:System.String> 类型。  
  
### XAML 的区域性信息和类型转换器  
 每个 <xref:System.ComponentModel.TypeConverter> 实现都可以唯一地解释对于转换是有效字符串的内容，它还可以使用或忽略作为参数传递的类型说明。 区域性和 XAML 类型转换的一个重要注意事项如下所示：尽管 XAML 支持使用可本地化的字符串作为特性值，但是不能使用这些可本地化的字符串作为具有特定区域性要求的类型转换器输入。 存在此限制是因为 XAML 特性值的类型转换器涉及使用 `en-US` 区域性的必定固定的语言 XAML 处理行为。 有关此限制的设计原因的详细信息，请参阅 XAML 语言规范 \([\[MS\-XAML\]](http://go.microsoft.com/fwlink/?LinkId=114525)\) 或 [WPF 全球化和本地化概述](../../../ocs/framework/wpf/advanced/wpf-globalization-and-localization-overview.md)。  
  
 区域性可能会产生问题的一个示例是，某些区域性使用逗号而不是句点作为字符串形式的数字的小数点分隔符。 这种用法与许多现有类型转换器所具有的行为（即使用逗号作为分隔符）冲突。 在周围的 XAML 中通过 `xml:lang` 传递区域性无法解决此问题。  
  
### 实现 ConvertFrom  
 若要能够用作支持 XAML 的 <xref:System.ComponentModel.TypeConverter> 实现，该转换器的 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 方法必须接受字符串作为 `value` 参数。 如果字符串采用有效格式，并且可以由 <xref:System.ComponentModel.TypeConverter> 实现进行转换，则返回对象必须支持强制转换为属性预期的类型。 否则，<xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 实现必须返回 `null`。  
  
 每个 <xref:System.ComponentModel.TypeConverter> 实现都可以唯一地解释对于转换构成效字符串的内容，它还可以使用或忽略作为参数传递的类型说明或区域性上下文。 但是，WPF XAML 处理可能不会在所有情况下都将值传递给类型说明上下文，还可能不会基于 `xml:lang` 传递区域性。  
  
> [!NOTE]
>  请勿使用大括号 \({}\)（尤其是左大括号 \({\)）作为字符串格式的元素。 这些字符保留作为标记扩展序列的入口和出口。  
  
 当类型转换器必须可以从 .NET Framework XAML 服务对象编写器访问 XAML 服务，但是针对上下文进行的 <xref:System.IServiceProvider.GetService%2A> 调用未返回该服务时，适合引发异常。  
  
### 实现 ConvertTo  
 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 可能用于序列化支持。 通过 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 为自定义类型及其类型转换器实现的序列化支持不是绝对要求。 但是，如果要实现控件，或使用序列化作为类的功能或设计的一部分，则应实现 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>。  
  
 若要能够用作支持 XAML 的 <xref:System.ComponentModel.TypeConverter> 实现，该转换器的 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 方法必须接受支持的类型（或值）的实例作为 `value` 参数。 当 `destinationType` 参数属于 <xref:System.String> 类型时，返回对象必须能够强制转换为 <xref:System.String>。 返回字符串必须表示 `value` 的序列化值。 理想情况下，选择的序列化格式应能够生成相同的值，就像该字符串传递给相同转换器的 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 实现一样，不会丢失大量信息。  
  
 如果值无法进行序列化，或转换器不支持序列化，则 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 实现必须返回 `null`，可能会引发异常。 但是，如果确实引发了异常，则应报告无法使用该转换作为 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 实现的一部分，以便支持首先使用 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 进行检查以避免异常这一最佳做法。  
  
 如果 `destinationType` 参数不属于 <xref:System.String> 类型，则你可以选择自己的转换器处理。 通常你会恢复为基实现处理，这会在基 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 中引发特定异常。  
  
 当类型转换器必须可以从 .NET Framework XAML 服务对象编写器访问 XAML 服务，但是针对上下文进行的 <xref:System.IServiceProvider.GetService%2A> 调用未返回该服务时，适合引发异常。  
  
### 实现 CanConvertFrom  
 对于 <xref:System.String> 类型的 `sourceType`，<xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> 实现应返回 `true`，否则遵从基实现。 不会从 <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> 引发异常。  
  
### 实现 CanConvertTo  
 对于 <xref:System.String> 类型的 `destinationType`，<xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 实现应返回 `true`，否则遵从基实现。 不会从 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 引发异常。  
  
<a name="Applying_the_TypeConverterAttribute"></a>   
## 应用 TypeConverterAttribute  
 对于要由 .NET Framework XAML 服务用作自定义类的操作类型转换器的自定义类型转换器，必须将 [!INCLUDE[TLA#tla_netframewkattr](../../../includes/tlasharptla-netframewkattr-md.md)] <xref:System.ComponentModel.TypeConverterAttribute> 应用于类定义。 通过特性指定的 <xref:System.ComponentModel.TypeConverterAttribute.ConverterTypeName%2A> 必须是自定义类型转换器的类型名。 如果应用此特性，则当 XAML 处理器处理属性类型使用自定义类类型的值时，它可以输入字符串并返回对象实例。  
  
 还可以基于每个属性提供类型转换器。 应将 [!INCLUDE[TLA#tla_netframewkattr](../../../includes/tlasharptla-netframewkattr-md.md)] <xref:System.ComponentModel.TypeConverterAttribute> 应用于属性定义（主定义，不是它包含的 `get`\/`set` 的实现），而不是将它应用于类定义。 属性的类型必须与自定义类型转换器处理的类型匹配。 应用此特性时，当 XAML 处理器处理该属性的值时，它可以处理输入字符串并返回对象实例。 如果选择使用来自 [!INCLUDE[TLA#tla_netframewk](../../../includes/tlasharptla-netframewk-md.md)] 或某种其他库（在其中无法控制类定义并且无法应用 <xref:System.ComponentModel.TypeConverterAttribute>）的属性类型，则每属性类型转换器方法特别有用。  
  
 若要为自定义附加成员提供类型转换行为，请将 <xref:System.ComponentModel.TypeConverterAttribute> 应用于附加成员的实现模式的 `Get` 访问器方法。  
  
<a name="accessing_service_provider_context_from_a_markup_extension_implementation"></a>   
## 从标记扩展实现访问服务提供程序上下文  
 可用服务对于任何值转换器都是相同的。 不同之处在于每个值转换器接收服务上下文的方式。 访问服务以及可用服务在主题 [Type Converters and Markup Extensions for XAML](../../../docs/framework/xaml-services/type-converters-and-markup-extensions-for-xaml.md) 中进行了说明。  
  
<a name="type_converters_in_the_xaml_node_stream"></a>   
## XAML 节点流中的类型转换器  
 如果使用 XAML 节点流，则尚未执行类型转换器的操作或最终结果。 在加载路径中，最终需要进行类型转换以便加载的特性字符串会在起始成员和结束成员中保留为文本值。 此操作最终需要的类型转换器可以使用 <xref:System.Xaml.XamlMember.TypeConverter%2A?displayProperty=fullName> 属性来确定。 但是，从 <xref:System.Xaml.XamlMember.TypeConverter%2A?displayProperty=fullName> 获取有效值依赖于具有 XAML 架构上下文，这可以通过基础成员（或成员使用的对象值的类型）访问此类信息。 调用类型转换行为也需要 XAML 架构上下文，因为这需要类型映射和创建转换器实例。  
  
## 请参阅  
 <xref:System.ComponentModel.TypeConverterAttribute>   
 [Type Converters and Markup Extensions for XAML](../../../docs/framework/xaml-services/type-converters-and-markup-extensions-for-xaml.md)   
 [XAML 概述 \(WPF\)](../../../ocs/framework/wpf/advanced/xaml-overview-wpf.md)