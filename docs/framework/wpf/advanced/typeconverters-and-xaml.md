---
title: "TypeConverters 和 XAML | Microsoft Docs"
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
  - "类, TypeConverter"
  - "TypeConverter 类"
  - "XAML, TypeConverter 类"
ms.assetid: f6313e4d-e89d-497d-ac87-b43511a1ae4b
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# TypeConverters 和 XAML
本主题介绍从字符串进行类型转换这项常规 XAML 语言功能的用途。  在 .NET Framework 中，<xref:System.ComponentModel.TypeConverter> 类是在 XAML 特性用法中可用作属性值的托管自定义类的实现的一部分，具有特定的用途。  如果编写自定义类，并希望该类的实例可用作 XAML 可设置特性值，则可能需要向该类应用 <xref:System.ComponentModel.TypeConverterAttribute> 和\/或编写自定义 <xref:System.ComponentModel.TypeConverter> 类。  
  
   
  
## 类型转换概念  
  
### XAML 和字符串值  
 在 XAML 文件中设置特性值时，该值的初始类型为纯文本形式的字符串。  甚至 <xref:System.Double> 等其他基元最初对于 XAML 处理器而言也是文本字符串。  
  
 XAML 处理器需要两条信息才能处理特性值。  第一条信息是要设置的属性的值类型。  用于定义特性值并且在 XAML 中进行处理的任何字符串最终都必须转换或解析为该类型的值。  如果该值为 XAML 分析器能够识别的基元（如数字值），则将尝试直接转换该字符串。  如果该值为枚举，则使用字符串检查是否有名称与该枚举中的命名常量匹配。  如果该值既不是分析器所能识别的基元，也不是枚举，则所涉及的类型必须能够根据转换的字符串提供该类型的实例（即值）。  通过指示类型转换器类达到此目的。  类型转换器实际上是一个帮助程序类，用于为 XAML 方案，可能还要为 .NET 代码中的代码调用提供另一个类的值。  
  
### 在 XAML 中使用现有的类型转换行为  
 根据您对于基础 XAML 概念的熟悉程度，您可能已经在基础应用程序 XAML 中使用了类型转换行为，只是您还不知道。  例如，WPF 确实定义了成百上千个采用 <xref:System.Windows.Point> 类型的值的属性。  <xref:System.Windows.Point> 是一个用于描述二维坐标空间中某个坐标的值，它实际上就有两个重要的属性：<xref:System.Windows.Point.X%2A> 和 <xref:System.Windows.Point.Y%2A>。  在 XAML 中指定一个点时，可将其指定为一个字符串，其中在所提供的 <xref:System.Windows.Point.X%2A> 和 <xref:System.Windows.Point.Y%2A> 值之间有分隔符（通常为英文逗号）。  例如：`<LinearGradientBrush StartPoint="0,0" EndPoint="1,1">`。  
  
 即使是 <xref:System.Windows.Point> 这种简单类型及其在 XAML 中的简单用法，其中也涉及到类型转换器。  在这种情况下，类型转换器是类 <xref:System.Windows.PointConverter>。  
  
 在类级别定义的 <xref:System.Windows.Point> 的类型转换器简化了所有采用 <xref:System.Windows.Point> 的属性的标记用法。  如果此处没有类型转换器，那么对于前面显示的同一示例，将需要以下冗长得多的标记：  
  
 `<LinearGradientBrush>`  
  
 `<LinearGradientBrush.StartPoint>`  
  
 `<Point X="0" Y="0"/>`  
  
 `</LinearGradientBrush.StartPoint>`  
  
 `<LinearGradientBrush.EndPoint>`  
  
 `<Point X="1" Y="1"/>`  
  
 `</LinearGradientBrush.EndPoint>`  
  
 `<LinearGradientBrush>`  
  
 一般来说，使用类型转换字符串还是更复杂的等效语法是对编码风格的选择。  您的 XAML 工具工作流可能也会影响值的设置方式。  某些 XAML 工具可能会生成最复制的标记形式，因为这可使往返于设计器视图或其自身的序列化机制更加容易。  
  
 通过检查确认类（或属性）中是否存在已应用的 <xref:System.ComponentModel.TypeConverterAttribute>，一般可以在 WPF 和 .NET Framework 类型中发现现有的类型转换器。  此特性出于 XAML 目的，可能还出于其他目的，将命名一个类，作为该类型的值的支持类型转换器。  
  
### 类型转换器和标记扩展  
 标记扩展和类型转换器根据 XAML 处理器行为以及这些行为所适用的方案来实现正交角色。  尽管上下文可用于标记扩展，但在标记扩展实现中通常不检查标记扩展为其提供值的属性的类型转换行为。  换句话说，即使标记扩展返回一个文本字符串作为其 `ProvideValue` 输出，也不会对该字符串调用应用于特定属性或属性值类型的类型转换行为。通常，标记扩展的用途是处理字符串并返回一个对象，而不涉及任何类型转换器。  
  
 一种常见的情况是需要标记扩展（而非类型转换器）来对已经存在的对象进行引用。  在最佳情况下，无状态类型转换器只能生成一个新实例，但该实例可能并不是所需的实例。  有关标记扩展的更多信息，请参见[标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)。  
  
### 本机类型转换器  
 在 XAML 分析器的 WPF 和 .NET Framework 实现中，有一些类型具有本机类型转换处理功能，但在传统上可能不会将这些类型视为基元。  <xref:System.DateTime> 就是这样的一个类型。  这种情况的原因在于 .NET Framework 体系结构的工作方式：<xref:System.DateTime> 类型在 mscorlib 中进行定义，这是 .NET 中最基础的库。  不允许用来自引入依赖关系的另一个程序集中的特性（<xref:System.ComponentModel.TypeConverterAttribute> 来自 System）将 <xref:System.DateTime> 特性化，因此不能支持根据特性化进行的常规类型转换器发现机制。  而是，XAML 分析器具有需要此类本机处理的类型的列表，并用类似于处理真实基元的方式处理这些类型。  （在 <xref:System.DateTime> 的情况下，这种方法中要调用 <xref:System.DateTime.Parse%2A>。  
  
<a name="Implementing_a_Type_Converter"></a>   
## 实现类型转换器  
  
### TypeConverter  
 在前面给出的 <xref:System.Windows.Point> 示例中，提到了 <xref:System.Windows.PointConverter> 类。  对于 XAML 的 .NET 实现，用于 XAML 目的的所有类型转换器都是从 <xref:System.ComponentModel.TypeConverter> 基类派生的类。  <xref:System.ComponentModel.TypeConverter> 类存在于 XAML 出现之前的 .NET Framework 版本中；其原始用法之一是为可视设计器中的属性对话框提供字符串转换功能。  对于 XAML，<xref:System.ComponentModel.TypeConverter> 的作用已变大，其中包括作为用于分析字符串特性值的 to\-string 和 from\-string 转换的基类，可能还包括处理特定对象属性的运行时值，使其恢复为特性形式的序列化字符串。  
  
 <xref:System.ComponentModel.TypeConverter> 出于 XAML 处理目的，定义了四个与来回转换字符串相关的成员：  
  
-   <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A>  
  
-   <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A>  
  
-   <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>  
  
-   <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>  
  
 其中，最重要的方法是 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>。  此方法将输入的字符串转换为必需的对象类型。  严格来说，可以将 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 方法实现为将更广泛的类型转换为转换器的预期目标类型，并因此实现超越 XAML 的目的（如支持运行时转换），但出于 XAML 目的，该方法仅仅作为可以处理重要的 <xref:System.String> 输入的代码路径。  
  
 下一个最重要的方法是 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>。  如果将应用程序转换为标记表示形式（例如，如果它保存为文件形式的 XAML），则 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 负责生成标记表示形式。  在这种情况下，对 XAML 重要的代码路径是传递 <xref:System.String> 的 `destinationType` 的时间。  
  
 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 和 <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> 是当服务查询 <xref:System.ComponentModel.TypeConverter> 实现的功能时使用的支持方法。  必须实现这些方法才能为转换器的等效转换方法所支持的类型特定情况返回 `true`。  出于 XAML 目的，这一般表示 <xref:System.String> 类型。  
  
### 区域性信息与 XAML 的类型转换器  
 每个 <xref:System.ComponentModel.TypeConverter> 实现对于什么内容构成对转换有效的字符串都可以有其自己的解释，还可以使用或忽略作为参数传递的类型描述。  对于区域性和 XAML 类型转换，有一个重要的注意事项。  XAML 完全支持使用可本地化的字符串作为特性值。  但不支持在使用该可本地化的字符串作为类型转换器输入时具有特定的区域性要求，因为 XAML 特性值的类型转换器包含一个必要的固定语言分析行为，其中使用 `en-US` 区域性。  有关此限制的设计原因的更多信息，应查阅 XAML 语言规范 \([\[MS\-XAML\]](http://go.microsoft.com/fwlink/?LinkId=114525)\)。  
  
 区域性可能造成问题的一个示例是，某些区域性使用英文逗号作为其数字的小数点分隔符。  这将与许多 WPF XAML 类型转换器所具有的使用英文逗号作为分隔符的行为发生冲突（根据常用的 X,Y 形式等过去的先例，或英文逗号分隔的列表）。  即使在周围的 XAML 中传递区域性（将 `Language` 或 `xml:lang` 设置为 `sl-SI` 区域性，以此方式使用英文逗号作为小数点的区域性的一个示例）也不能解决此问题。  
  
### 实现 ConvertFrom  
 若要使该转换器的 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 方法可用作支持 XAML 的 <xref:System.ComponentModel.TypeConverter> 实现，该方法必须接受字符串作为 `value` 参数。  如果该字符串的格式有效，而且可以由 <xref:System.ComponentModel.TypeConverter> 实现进行转换，则返回的对象必须支持强制转换为该属性所预期的类型。  否则，<xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 实现必须返回 `null`。  
  
 每个 <xref:System.ComponentModel.TypeConverter> 实现都可以有其自己对组成有效转换字符串的内容的解释，还可以使用或忽略作为参数传递的类型描述或区域性上下文。  但是，WPF XAML 处理可能不会在所有情况下都向类型描述上下文传递值，也有可能不根据 `xml:lang` 传递区域性。  
  
> [!NOTE]
>  请勿使用大括号字符，尤其是 {，其原因是它有可能作为您字符串格式的一个元素。  这些字符保留为标记扩展序列的入口和出口。  
  
### 实现 ConvertTo  
 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 可潜在用于序列化支持。  通过 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 支持对自定义类型及其类型转换器进行序列化不是绝对必需的。  但是，如果您正实现一个控件，或正使用作为类的功能和设计一部分的序列化，则应实现 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>。  
  
 若要使该转换器的 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 方法可用作支持 XAML 的 <xref:System.ComponentModel.TypeConverter> 实现，该方法必须接受要支持的类型的实例（即值）作为 `value` 参数。  如果 `destinationType` 参数为 <xref:System.String> 类型，则返回的对象必须可强制转换为 <xref:System.String>。  返回的字符串必须表示 `value` 的序列化值。  理想情况下，如果将该字符串传递到同一转换器的 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 实现，则选择的序列化格式应能够生成相同的值，同时不会丢失大量信息。  
  
 如果值无法进行序列化，或者转换器不支持序列化，则 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 实现必须返回 `null`，并允许在此情况下引发异常。  但如果引发了异常，则应报告无法使用该转换作为 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 实现的一部分，以便支持首先检查 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 以避免异常的最佳实践。  
  
 如果 `destinationType` 参数不为类型 <xref:System.String>，则可以选择自己的转换器处理。  通常，您要恢复使用基本的实现处理方法，该方法在最基本的 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> 中会引发特定的异常。  
  
### 实现 CanConvertTo  
 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 实现应为类型为 <xref:System.String> 的 `destinationType` 返回 `true`，否则遵从基实现。  
  
### 实现 CanConvertFrom  
 您的 <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> 实现应为类型 <xref:System.String> 的 `sourceType` 返回 `true`，否则遵从基实现。  
  
<a name="Applying_the_TypeConverterAttribute"></a>   
## 应用 TypeConverterAttribute  
 为使 XAML 处理器使用自定义类型转换器作为自定义类的当前类型转换器，必须向类定义应用 [!INCLUDE[TLA#tla_netframewkattr](../../../../includes/tlasharptla-netframewkattr-md.md)] <xref:System.ComponentModel.TypeConverterAttribute>。  通过特性指定的 <xref:System.ComponentModel.TypeConverterAttribute.ConverterTypeName%2A> 必须是自定义类型转换器的类型名称。  应用此特性后，当 XAML 处理器在属性类型使用自定义类类型的情况下处理值时，它可以输入字符串并返回对象实例。  
  
 您还可以基于每个属性提供类型转换器。  不应将 [!INCLUDE[TLA#tla_netframewkattr](../../../../includes/tlasharptla-netframewkattr-md.md)] <xref:System.ComponentModel.TypeConverterAttribute> 应用到类定义，而是将其应用到属性定义（是主定义，而不是其中的 `get`\/`set` 实现）。  属性类型必须与自定义转换器处理的类型匹配。  应用此特性后，当 XAML 处理器处理该属性的值时，它可以处理输入字符串并返回对象实例。  如果选择使用 [!INCLUDE[TLA#tla_netframewk](../../../../includes/tlasharptla-netframewk-md.md)] 或某些其他库（其中无法控制类定义并无法应用 <xref:System.ComponentModel.TypeConverterAttribute>）中的属性类型，则每个属性类型转换器方法尤其有用。  
  
## 请参阅  
 <xref:System.ComponentModel.TypeConverter>   
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [标记扩展和 WPF XAML](../../../../docs/framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)   
 [XAML 语法详述](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)