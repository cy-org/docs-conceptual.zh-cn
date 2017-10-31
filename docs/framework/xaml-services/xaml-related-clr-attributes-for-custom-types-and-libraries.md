---
title: "XAML-Related CLR Attributes for Custom Types and Libraries | Microsoft Docs"
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
  - "CLR attributes for custom types [XAML Services]"
ms.assetid: 5dfb299a-b6e2-41b8-8694-e6ac987547f1
caps.latest.revision: 8
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 8
---
# XAML-Related CLR Attributes for Custom Types and Libraries
本主题介绍由 .NET Framework XAML 服务定义的公共语言运行时 \(CLR\) 特性。  本主题还介绍在 .NET Framework 中定义的具有 XAML 相关方案的其他 CLR 特性，以便应用于程序集或类型。  使用这些 CLR 特性将程序集、类型或成员特性化可提供与类型有关的 XAML 类型系统信息。  将信息提供给使用 .NET Framework XAML 服务的任何 XAML 使用方，以便直接处理或通过专用 XAML 读取器和 XAML 编写器处理 XAML 节点流。  
  
## 自定义类型和自定义成员 XAML 相关 CLR 特性  
 使用 CLR 特性要求您使用全部 CLR 来定义类型，否则此类特性将不可用。  如果使用 CLR 来定义类型支持，则 .NET Framework XAML 服务 XAML 编写器使用的默认 XAML 架构上下文可以通过针对支持程序集的反射来读取 CLR 特性。  
  
 以下各节介绍可应用于自定义类型或自定义成员的 XAML 相关特性。  每个 CLR 特性都传达与 XAML 类型系统有关的信息。  在加载路径中，特性化的信息可帮助 XAML 读取器形成有效的 XAML 节点流，或帮助 XAML 编写器生成有效的对象图。  在保存路径中，特性化的信息可帮助 XAML 读取器形成重建 XAML 类型系统信息的有效 XAML 节点流，或者为 XAML 编写器或其他 XAML 使用者声明序列化提示或要求。  
  
### AmbientAttribute  
 **参考文档：** <xref:System.Windows.Markup.AmbientAttribute>  
  
 **适用对象：**类、属性或支持可附加属性的 `get` 访问器成员。  
  
 **参数：**无  
  
 <xref:System.Windows.Markup.AmbientAttribute> 指示采用该特性化类型的单个属性或所有属性在 XAML 中都应基于环境属性概念进行解释。  环境概念与 XAML 处理器确定成员的类型所有者的方式相关。  环境属性是这样一种属性，该属性的值在创建对象图时应在分析器上下文中可用，但其常用类型成员查找由于正在创建直接 XAML 节点集而挂起。  
  
 环境概念可以应用于可附加的成员，这些成员未按照 CLR 特性定义 <xref:System.AttributeTargets> 的方式表示为属性。  应该仅对支持 XAML 的可附加用法的 `get` 访问器应用方法特性用法。  
  
### ConstructorArgumentAttribute  
 **参考文档：** <xref:System.Windows.Markup.ConstructorArgumentAttribute>  
  
 **适用对象：**类  
  
 **参数：**一个字符串，该字符串指定与单个构造函数参数匹配的属性的名称。  
  
 <xref:System.Windows.Markup.ConstructorArgumentAttribute> 指定可以使用非默认构造函数语法初始化对象，并且指定具有指定名称的属性提供构造信息。  此信息主要用于 XAML 序列化。  有关更多信息，请参见 <xref:System.Windows.Markup.ConstructorArgumentAttribute>。  
  
### ContentPropertyAttribute  
 **参考文档：** <xref:System.Windows.Markup.ContentPropertyAttribute>  
  
 **适用对象：**类  
  
 **参数：**一个字符串，该字符串指定特性化类型的成员的名称。  
  
 <xref:System.Windows.Markup.ContentPropertyAttribute> 指示由参数命名的属性应该作为该类型的 XAML 内容属性。  XAML 内容属性定义继承到可赋值给定义类型的所有派生类型。  可以通过对特定派生类型应用 <xref:System.Windows.Markup.ContentPropertyAttribute> 而重写特定派生类型的定义。  
  
 对于作为 XAML 内容属性的属性，在 XAML 用法中可以忽略该属性的属性元素标记。  通常，要指定为内容和包容模型提升简化的 XAML 标记的 XAML 内容属性。  由于只能将一个成员指定为 XAML 内容属性，因此有时在设计中要选择应该将某一类型的若干容器属性中的哪个属性指定为 XAML 内容属性。  其他容器属性必须与显式属性元素一起使用。  
  
 在 XAML 节点流中，XAML 内容属性仍然使用 <xref:System.Xaml.XamlMember> 的属性的名称生成 `StartMember` 和 `EndMember` 节点。  为了确定某个成员是否是 XAML 内容属性，请检查 `StartObject` 位置的 <xref:System.Xaml.XamlType> 值并获取 <xref:System.Xaml.XamlType.ContentProperty%2A> 的值。  
  
### ContentWrapperAttribute  
 **参考文档：** <xref:System.Windows.Markup.ContentWrapperAttribute>  
  
 **适用对象：**类、（特别是）集合类型。  
  
 **参数：**一个 <xref:System.Type>，它指定要用作外部内容的内容包装类型的类型。  
  
 <xref:System.Windows.Markup.ContentWrapperAttribute> 指定在关联的集合类型上将用来包装外部内容的一种或多种类型。  外部内容是指一些情况，在这些情况下，内容属性类型上的类型系统约束不捕获所属类型的 XAML 用法将支持的所有可能的内容情况。  例如，对特定类型的内容的 XAML 支持可能支持强类型的泛型 <xref:System.Collections.ObjectModel.Collection%601> 中的字符串。  内容包装对于将预先存在的标记约定迁移到用于集合的可赋值的值的 XAML 概念中（如迁移与文本相关的内容模型）非常有用。  
  
 若要指定多个内容包装类型，请多次应用该特性。  
  
### DependsOnAttribute  
 **参考文档：** <xref:System.Windows.Markup.DependsOnAttribute>  
  
 **适用对象：**属性  
  
 **参数：**一个字符串，该字符串指定特性化类型的另一个成员的名称。  
  
 <xref:System.Windows.Markup.DependsOnAttribute> 指示特性化属性依赖于另一个属性的值。  将此特性应用于属性定义可确保在 XAML 对象编写时首先处理依赖属性。  使用 <xref:System.Windows.Markup.DependsOnAttribute> 可指定类型的属性的例外情况，在这些情况下，必须按照特定的分析顺序才能进行有效的对象创建。  
  
 可以将多个 <xref:System.Windows.Markup.DependsOnAttribute> 情况应用于一个属性定义。  
  
### MarkupExtensionReturnTypeAttribute  
 **参考文档：** <xref:System.Windows.Markup.MarkupExtensionReturnTypeAttribute>  
  
 **适用对象：**应为 <xref:System.Windows.Markup.MarkupExtension> 派生类型的类。  
  
 **参数：**一个 <xref:System.Type>，它指定预期作为特性化 <xref:System.Windows.Markup.MarkupExtension> 的 `ProvideValue` 结果的最精确类型。  
  
 有关更多信息，请参见 [Markup Extensions for XAML Overview](../../../docs/framework/xaml-services/markup-extensions-for-xaml-overview.md)。  
  
### NameScopePropertyAttribute  
 **参考文档：** <xref:System.Windows.Markup.NameScopePropertyAttribute>  
  
 **适用对象：**类  
  
 **参数：**支持两种形式的特性：  
  
-   一个字符串，该字符串指定特性化类型的某个属性的名称。  
  
-   一个字符串，该字符串指定某个属性的名称以及一个定义该命名属性的类型的 <xref:System.Type>。  这种形式用于将可附加成员指定为 XAML 名称范围属性。  
  
 <xref:System.Windows.Markup.NameScopePropertyAttribute> 指定为特性化的类提供 XAML 名称范围值的属性。  XAML 名称范围属性应当引用实现 <xref:System.Windows.Markup.INameScope> 并保存实际 XAML 名称范围、其存储区及其行为的对象。  
  
### RuntimeNamePropertyAttribute  
 **参考文档：** <xref:System.Windows.Markup.RuntimeNamePropertyAttribute>  
  
 **适用对象：**类  
  
 **参数：**一个字符串，该字符串指定特性化类型的运行时名称属性的名称。  
  
 <xref:System.Windows.Markup.RuntimeNamePropertyAttribute> 报告映射到 XAML [x:Name Directive](../../../docs/framework/xaml-services/x-name-directive.md) 的特性化类型的属性。  该属性的类型必须为 <xref:System.String> 并且必须是读\/写属性。  
  
 该定义继承到可赋值给定义类型的所有派生类型。  可以通过对特定派生类型应用 <xref:System.Windows.Markup.RuntimeNamePropertyAttribute> 而重写特定派生类型的定义。  
  
### TrimSurroundingWhitespaceAttribute  
 **参考文档：** <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute>  
  
 **适用对象：**类型  
  
 **参数：**无。  
  
 <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute> 适用于特定类型，这些类型可能作为空白有意义的内容（由含有 <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute> 的集合包含的内容）中的子元素出现。  <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute> 主要与保存路径有关，但可以通过检查 <xref:System.Xaml.XamlType.TrimSurroundingWhitespace%2A?displayProperty=fullName> 用在加载路径的 XAML 类型系统中。  有关更多信息，请参见 [Whitespace Processing in XAML](../../../docs/framework/xaml-services/whitespace-processing-in-xaml.md)。  
  
### TypeConverterAttribute  
 **参考文档：** <xref:System.ComponentModel.TypeConverterAttribute>  
  
 **适用对象：**类、属性、方法（唯一有效的 XAML 方法是支持可附加成员的 `get` 访问器）。  
  
 **参数：** <xref:System.ComponentModel.TypeConverter> 的 <xref:System.Type>。  
  
 XAML 上下文中的 <xref:System.ComponentModel.TypeConverterAttribute> 引用一个自定义 <xref:System.ComponentModel.TypeConverter>。  此 <xref:System.ComponentModel.TypeConverter> 为自定义类型或该类型的成员提供类型转换行为。  
  
 可将 <xref:System.ComponentModel.TypeConverterAttribute> 特性应用于您的类型，从而引用您的类型转换器实现。  可以对类、结构或接口定义 XAML 的类型转换器。  不需要为枚举提供类型转换，该转换是自然启用的。  
  
 类型转换器应能够将用于标记中的特性或初始化文本的字符串转换为所需的目标类型。  有关更多信息，请参见 [TypeConverters 和 XAML](../../../ocs/framework/wpf/advanced/typeconverters-and-xaml.md)。  
  
 可以针对特定属性确立 XAML 的类型转换器行为，而不是应用于某个类型的所有值。  在这种情况下，将 <xref:System.ComponentModel.TypeConverterAttribute> 应用于属性定义（外部定义，而不是特定的 `get` 和 `set` 定义）。  
  
 通过将 <xref:System.ComponentModel.TypeConverterAttribute> 应用于支持 XAML 用法的 `get` 方法访问器，可以为自定义可附加成员的 XAML 用法指定类型转换器行为。  
  
 与 <xref:System.ComponentModel.TypeConverter> 一样，在 XAML 存在之前，<xref:System.ComponentModel.TypeConverterAttribute> 就已经存在于 .NET Framework 中了，并且类型转换器模型还用作其他用途。  为了引用和使用 <xref:System.ComponentModel.TypeConverterAttribute>，必须对其完全限定或为 <xref:System.ComponentModel> 提供 `using` 语句。  还必须将系统程序集包含在项目中。  
  
### UidPropertyAttribute  
 **参考文档：** <xref:System.Windows.Markup.UidPropertyAttribute>  
  
 **适用对象：**类  
  
 **参数：**一个字符串，该字符串按名称引用相关属性。  
  
 指示用作 [x:Uid Directive](../../../docs/framework/xaml-services/x-uid-directive.md) 别名的类的 CLR 属性。  
  
### UsableDuringInitializationAttribute  
 **参考文档：** <xref:System.Windows.Markup.UsableDuringInitializationAttribute>  
  
 **适用对象：**类  
  
 **参数：**一个布尔值。  如果用于特性的预期目的，则应该始终将它指定为 `true`。  
  
 指示在 XAML 对象图创建期间是否自上而下生成此类型。  这是一个高级概念，这个概念可能与编程模型的定义紧密相关。  有关更多信息，请参见 <xref:System.Windows.Markup.UsableDuringInitializationAttribute>。  
  
### ValueSerializerAttribute  
 **参考文档：** <xref:System.Windows.Markup.ValueSerializerAttribute>  
  
 **适用对象：**类、属性、方法（唯一有效的 XAML 方法是支持可附加成员的 `get` 访问器）。  
  
 **参数：**一个 <xref:System.Type>，它指定要在对特性化类型的所有属性或特定的特性化属性进行序列化时使用的值序列化程序支持类。  
  
 <xref:System.Windows.Markup.ValueSerializer> 指定一个值序列化类，该类比 <xref:System.ComponentModel.TypeConverter> 需要更多的状态和上下文。  通过对可附加成员的 `get` 访问器方法应用 <xref:System.Windows.Markup.ValueSerializerAttribute> 特性，可将 <xref:System.Windows.Markup.ValueSerializer> 与该可附加成员关联。  值序列化也适用于枚举、接口和结构，但不适用于委托。  
  
### WhitespaceSignificantCollectionAttribute  
 **参考文档：** <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>  
  
 **适用对象：**类、（特别是）集合类型，这些结合类型预期承载混合内容，其中对象元素周围的空白对于 UI 表示形式可能有意义。  
  
 **参数：**无。  
  
 <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute> 指示 XAML 处理器应该将集合类型处理为空白有意义，这会影响集合中 XAML 节点流的值节点的构造。  有关更多信息，请参见 [Whitespace Processing in XAML](../../../docs/framework/xaml-services/whitespace-processing-in-xaml.md)。  
  
### XamlDeferLoadAttribute  
 **参考文档：** <xref:System.Windows.Markup.XamlDeferLoadAttribute>  
  
 **适用对象：**类、属性。  
  
 **参数：**支持两个特性类型：作为字符串的类型或作为 <xref:System.Type> 的类型。  请参见 <xref:System.Windows.Markup.XamlDeferLoadAttribute>。  
  
 指示类或属性具有 XAML 的延迟加载用途（如模板行为），并报告启用延迟行为及其目标\/内容类型的类。  
  
### XamlSetMarkupExtensionAttribute  
 **参考文档：** <xref:System.Windows.Markup.XamlSetMarkupExtensionAttribute>  
  
 **适用对象：**类  
  
 **参数：**为回调命名。  
  
 指示某个类可以使用标记扩展为它的一个或多个属性提供值，并且在对该类的任何属性执行标记扩展 set 操作之前，引用 XAML 编写器应调用的处理程序。  
  
### XamlSetTypeConverterAttribute  
 **参考文档：** <xref:System.Windows.Markup.XamlSetTypeConverterAttribute>  
  
 **适用对象：**类  
  
 **参数：**为回调命名。  
  
 指示某个类可以使用类型转换器为它的一个或多个属性提供值，并且在对该类的任何属性执行类型转换器 set 操作之前，引用 XAML 编写器应调用的处理程序。  
  
### XmlLangPropertyAttribute  
 **参考文档：** <xref:System.Windows.Markup.XmlLangPropertyAttribute>  
  
 **适用对象：**类  
  
 **参数：**一个字符串，该字符串指定特性化类型的用作 `xml:lang` 别名的属性名称。  
  
 <xref:System.Windows.Markup.XmlLangPropertyAttribute> 报告映射到 XML `lang` 指令的特性化类型的属性。  该属性的类型可以不是 <xref:System.String>，但必须可从字符串赋值（这可以通过将类型转换器与该属性的类型或特定的属性相关联来实现）。  该属性必须是读\/写属性。  
  
 这是用于映射 `xml:lang` 的方案，以便运行时对象模型可以访问 XML 指定的语言信息，而无需使用 XMLDOM 专门进行处理。  
  
 该定义继承到可赋值给定义类型的所有派生类型。  可以通过对特定派生类型应用 <xref:System.Windows.Markup.XmlLangPropertyAttribute> 而重写特定派生类型的定义，但这种情况不常见。  
  
## 程序集级别的 XAML 相关 CLR 特性  
 以下各节介绍不适用于类型或成员定义但适用于程序集的 XAML 相关特性。  这些特性都与定义包含要在 XAML 中使用的自定义类型的库的总体目标有关。  某些特性不一定会直接影响 XAML 节点流，但会在节点流中传递以供其他使用方使用。  该信息的使用方包括需要 XAML 命名空间信息以及关联的前缀信息的设计环境或序列化进程。  XAML 架构上下文（包括 .NET Framework XAML 服务默认值）也使用此信息。  
  
### XmlnsCompatibleWithAttribute  
 **参考文档：** <xref:System.Windows.Markup.XmlnsCompatibleWithAttribute>  
  
 **参数：**  
  
-   一个字符串，该字符串指定要归入的 XAML 命名空间的标识符。  
  
-   一个字符串，该字符串指定可以将来自上一参数的 XAML 命名空间归入的 XAML 命名空间的标识符。  
  
 <xref:System.Windows.Markup.XmlnsCompatibleWithAttribute> 指定一个 XAML 命名空间可以归入另一个 XAML 命名空间。  通常，进行归入的 XAML 命名空间在以前定义的 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 中指示。  此方法可用于对某个库中的 XAML 词汇进行版本控制，从而使它与之前针对以前版本的词汇定义的标记兼容。  
  
### XmlnsDefinitionAttribute  
 **参考文档：** <xref:System.Windows.Markup.XmlnsDefinitionAttribute>  
  
 **参数：**  
  
-   一个字符串，该字符串指定要定义的 XAML 命名空间的标识符。  
  
-   一个字符串，该字符串命名 CLR 命名空间。  CLR 命名空间应该在您的程序集中定义公共类型，并且该 CLR 命名空间类型中的至少一个类型应该用于 XAML 用法。  
  
 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 基于每个程序集指定 XAML 命名空间与 CLR 命名空间之间的映射，然后将该映射用于由 XAML 对象编写器或 XAML 架构上下文进行的类型解析。  
  
 可以对一个程序集应用多个 <xref:System.Windows.Markup.XmlnsDefinitionAttribute>。  可以出于下列原因的任意组合而这样做：  
  
-   库设计包含多个 CLR 命名空间以用于运行时 API 访问的逻辑组织；但是，您需要引用相同的 XAML 命名空间来使这些命名空间中的所有类型都是 XAML 可用的。  在这种情况下，可使用相同的 <xref:System.Windows.Markup.XmlnsDefinitionAttribute.XmlNamespace%2A> 值但不同的 <xref:System.Windows.Markup.XmlnsDefinitionAttribute.ClrNamespace%2A> 值来应用多个 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 特性。  如果为框架或应用程序要在常见用法中成为默认 XAML 命名空间的 XAML 命名空间定义映射，则此特性尤其有用。  
  
-   库设计包含多个 CLR 命名空间，并且您希望在这些 CLR 命名空间中类型的使用不同时有意分离 XAML 命名空间。  
  
-   在该程序集中定义一个 CLR 命名空间，并且希望该命名空间能够通过多个 XAML 命名空间访问。  在您支持具有相同基本代码的多个词汇表时，会出现这种情况。  
  
-   在一个或多个 CLR 命名空间中定义 XAML 语言支持。  对于这些命名空间，<xref:System.Windows.Markup.XmlnsDefinitionAttribute.XmlNamespace%2A> 值都应为 `http://schemas.microsoft.com/winfx/2006/xaml`。  
  
### XmlnsPrefixAttribute  
 **参考文档：** <xref:System.Windows.Markup.XmlnsPrefixAttribute>  
  
 **参数：**  
  
-   一个字符串，该字符串指定 XAML 命名空间的标识符。  
  
-   一个字符串，该字符串指定建议的前缀。  
  
 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 指定用于 XAML 命名空间的建议前缀。  在 XAML 文件中编写元素和特性时（该文件由 .NET Framework XAML 服务 <xref:System.Xaml.XamlXmlWriter> 进行序列化），或在 XAML 实现库与具有 XAML 编辑功能的设计环境进行交互时，此前缀十分有用。  
  
 可以对一个程序集应用多个 <xref:System.Windows.Markup.XmlnsPrefixAttribute>。  可以出于下列原因的任意组合而这样做：  
  
-   您的程序集为多个 XAML 命名空间定义类型。  在这种情况下，应为每个 XAML 命名空间定义不同的前缀值。  
  
-   您支持多个词汇表并且对每个词汇表和 XAML 命名空间使用不同的前缀。  
  
-   在该程序集中定义 XAML 语言支持并且有 `http://schemas.microsoft.com/winfx/2006/xaml` 对应的 <xref:System.Windows.Markup.XmlnsDefinitionAttribute>。  在这种情况下，通常应该提升前缀 `x`。  
  
> [!NOTE]
>  .NET Framework XAML 服务还定义与 XAML 相关的特性 <xref:System.Windows.Markup.RootNamespaceAttribute>。  此特性是用于项目系统支持的程序集级特性，它与 XAML 自定义类型无关。  
  
## 请参阅  
 <xref:System.Attribute>   
 [Defining Custom Types for Use with .NET Framework XAML Services](../../../docs/framework/xaml-services/defining-custom-types-for-use-with-net-framework-xaml-services.md)