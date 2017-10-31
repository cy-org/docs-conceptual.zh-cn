---
title: "Service Contexts Available to Type Converters and Markup Extensions | Microsoft Docs"
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
  - "XAML [XAML Services], type converter services how-to"
ms.assetid: b4dad00f-03da-4579-a4e9-d8d72d2ccbce
caps.latest.revision: 13
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 13
---
# Service Contexts Available to Type Converters and Markup Extensions
支持类型转换器和标记扩展用法的类型的作者通常必须拥有用法在标记或周围对象图结构中的所在位置的相关上下文信息。 为了能正确实例化所提供的对象或者对对象图中的现有对象进行对象引用，可能需要此信息。 使用.NET Framework XAML 服务时，可能需要的上下文将作为一系列服务接口公开。 类型转换器或标记扩展支持代码可使用从 <xref:System.Xaml.XamlObjectWriter> 或相关类型传递且可用的服务提供程序上下文来查询服务。 可通过一个这样的服务来直接获取 XAML 架构上下文。 本主题介绍如何从值转换器实现访问服务上下文，并且列出了通常可用的服务及其角色。  
  
<a name="obtaining_services"></a>   
## 获取服务  
 作为值转换器的实现者，你经常需要访问在其中应用了值转换器的某些类型的上下文。 此上下文可能包括诸如活动的 XAML 架构上下文、对 XAML 架构上下文和 XAML 对象编写器提供的类型映射系统的访问权限等信息。 可用于标记扩展或类型转换器实现的服务通过属于每种虚方法签名的一部分的上下文参数来传递。 在每种情况下，你都在上下文中实现了 <xref:System.IServiceProvider>，并且可以调用 <xref:System.IServiceProvider.GetService%2A?displayProperty=fullName> 来请求服务。  
  
<a name="services_for_a_markup_extension"></a>   
## 用于标记扩展的服务  
 <xref:System.Windows.Markup.MarkupExtension> 只有一个虚方法 <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>。 输入 `serviceProvider` 参数是 XAML 处理器调用标记扩展时服务与实现的通信方式。 下面的伪代码演示了标记扩展实现可如何在其 <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A> 中查询服务：  
  
```  
public override object ProvideValue(IServiceProvider serviceProvider) { ... // Get the IXamlTypeResolver from the service provider if (serviceProvider == null) { throw new ArgumentNullException("serviceProvider"); } IXamlTypeResolver xamlTypeResolver = serviceProvider.GetService(typeof(IXamlTypeResolver)) as IXamlTypeResolver; if (xamlTypeResolver == null) { throw new ArgumentException("IXamlTypeResolver")); } ... }  
```  
  
<a name="services_for_a_type_converter"></a>   
## 用于类型转换器的服务  
 <xref:System.ComponentModel.TypeConverter> 有四个虚方法，它们使用一个服务上下文并且都支持 XAML 用法。 每个方法都传递一个输入 `context` 参数。 此参数的类型为 <xref:System.ComponentModel.ITypeDescriptorContext>，但该接口继承 <xref:System.IServiceProvider>，因此具有一个可用于类型转换器实现的 <xref:System.IServiceProvider.GetService%2A> 方法。  
  
 下面的伪代码演示了 XAML 用法的类型转换器实现可如何在它的一个替代（在本示例中为 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>）中查询服务：  
  
```  
public override object ConvertFrom(ITypeDescriptorContext typeDescriptorContext, CultureInfo cultureInfo, object source) { IRootObjectProvider rootProvider = typeDescriptorContext.GetService(typeof(IRootObjectProvider)) as IRootObjectProvider; if (rootProvider != null && source is String) { //return something, else ... } throw GetConvertFromException(source); }  
```  
  
<a name="services_for_a_value_serializer"></a>   
## 用于值序列化程序的服务  
 对于值序列化程序上下文，使用特定于 <xref:System.Windows.Markup.ValueSerializer> 类 <xref:System.Windows.Markup.IValueSerializerContext> 的服务提供程序类型。 该上下文传递给四个 <xref:System.Windows.Markup.ValueSerializer> 虚方法的替代。 从上下文调用 <xref:System.IServiceProvider.GetService%2A> 以获取服务。  
  
<a name="using_the_xaml_service_provider_contexts"></a>   
## 使用 XAML 服务提供程序上下文  
 可供 <xref:System.IServiceProvider.GetService%2A> 访问可用于标记扩展或类型转换器的 XAML 服务的服务提供程序作为内部类实现，并且仅通过接口以及将其传递到相关上下文中的方式公开。 只要加载路径或保存路径的默认 .NET Framework XAML 服务实现中的 XAML 处理操作调用需要服务上下文的相关标记扩展或类型转换器方法，就会传递此内部对象。 根据具体情况，系统服务上下文提供 `MarkupExtensionContext` 或 `TextSyntaxContext`，但这两个特定类都是内部类。 你与这些类的交互仅限于通过 <xref:System.IServiceProvider.GetService%2A> 从中请求服务。  
  
<a name="available_systemxaml_services"></a>   
## .NET Framework XAML 服务上下文中可用的服务  
 .NET Framework XAML 服务为标记扩展、类型转换器、值序列化程序以及可能的其他用法定义服务。 以下各节介绍每种服务，并提供有关可如何在实现中使用服务的指导。  
  
### IServiceProvider  
 **参考文档**：<xref:System.IServiceProvider>  
  
 **相关内容：**.NET Framework 中基于服务的基础结构的基本操作，以便你可以调用 <xref:System.IServiceProvider.GetService%2A?displayProperty=fullName>。  
  
### ITypeDescriptorContext  
 **参考文档**：<xref:System.ComponentModel.ITypeDescriptorContext>  
  
 派生自 <xref:System.IServiceProvider>。 此类表示标准 <xref:System.ComponentModel.TypeConverter> 签名中的上下文；<xref:System.ComponentModel.TypeConverter> 是自 .NET Framework 1.0 起就已存在的类。 它早于用于字符串到值类型转换的 XAML 和 XAML <xref:System.ComponentModel.TypeConverter> 方案。 在 .NET Framework XAML 服务上下文中，<xref:System.ComponentModel.TypeConverter> 的方法是显式实现的。 显式实现的行为向调用方指示 <xref:System.ComponentModel.ITypeDescriptorContext> API 与 XAML 类型系统无关，或者与 XAML 中的读取或写入对象无关。<xref:System.ComponentModel.ITypeDescriptorContext.Container%2A>、<xref:System.ComponentModel.ITypeDescriptorContext.Instance%2A> 和 <xref:System.ComponentModel.ITypeDescriptorContext.PropertyDescriptor%2A> 通常从 .NET Framework XAML 服务上下文返回 `null`。  
  
### IValueSerializerContext  
 **参考文档**：<xref:System.Windows.Markup.IValueSerializerContext>  
  
 派生自 <xref:System.ComponentModel.ITypeDescriptorContext>，并且还依赖于显式实现以抑制有关 XAML 类型系统的错误含义。 支持 <xref:System.Windows.Markup.ValueSerializer> 上的静态查找帮助器方法。  
  
### IXamlTypeResolver  
 **参考文档**：<xref:System.Windows.Markup.IXamlTypeResolver>  
  
 **由以下内容定义：** <xref:System.Windows.Markup> 命名空间、System.Xaml 程序集  
  
 **相关内容：**加载路径方案以及与 XAML 架构上下文的交互  
  
 **服务 API:**  <xref:System.Windows.Markup.IXamlTypeResolver.Resolve%2A>  
  
 可能会影响 XAML 到 CLR 类型映射，当 XAML 编写器在对象图中构造 CLR 对象时，此映射是必需的。<xref:System.Windows.Markup.IXamlTypeResolver.Resolve%2A> 处理对应于 XAML 类型名称 \(<xref:System.Xaml.XamlType.Name%2A?displayProperty=fullName>\) 的可能由前缀限定的字符串，并返回一个 CLR <xref:System.Type>。 解析类型通常很大程度上取决于 XAML 架构上下文。 只有 XAML 架构上下文了解注意事项，如加载哪些程序集以及可以或应访问其中哪些程序集以进行类型解析。  
  
### IUriContext  
 **参考文档**：<xref:System.Windows.Markup.IUriContext>  
  
 **由以下内容定义：** <xref:System.Windows.Markup> 命名空间、System.Xaml 程序集  
  
 **相关内容：**是 URI 或 `x:Uri` 值的成员值的加载路径和保存路径处理。  
  
 **服务 API:**  <xref:System.Windows.Markup.IUriContext.BaseUri%2A>  
  
 此服务报告一个全局可用的 URI 根（如果有）。 可使用此 URI 根将相对 URI 解析为绝对 URI，反之亦然。 此方案主要与由特定框架或框架中常用根元素类的功能公开的应用程序服务相关。 可以采用 XAML 读取器设置的形式建立基 URI，然后传递给 XAML 对象编写器并由此服务进行报告。  
  
### IAmbientProvider  
 **参考文档**：<xref:System.Xaml.IAmbientProvider>  
  
 **由以下内容定义：** <xref:System.Xaml> 命名空间、System.Xaml 程序集  
  
 **相关内容：**加载路径处理以及类型查找延迟或优化。  
  
 **服务 API：** <xref:System.Xaml.IAmbientProvider.GetAllAmbientValues%2A>、3 个其他 API。  
  
 XAML 中的环境概念是一种将类型的特定成员标记为环境的方法。 或者，某种类型也可以是环境，以便保留该类型实例的所有属性值都应视为环境属性。 沿 XAML 节点流前进或作为对象图中的后代的标记扩展或类型转换器可以在加载时访问环境属性或类型实例；也可以在保存时使用环境结构的知识。 这可能会影响其他服务（例如，<xref:System.Windows.Markup.IXamlTypeResolver> 或 `x:Type`）的类型解析所需的限定程度。 另请参阅<xref:System.Xaml.AmbientPropertyValue>。  
  
### IXamlSchemaContextProvider  
 **参考文档**：<xref:System.Xaml.IXamlSchemaContextProvider>  
  
 **由以下内容定义：** <xref:System.Xaml> 命名空间、System.Xaml 程序集  
  
 **相关内容：**加载路径以及必须将 XAML 类型解析为后备类型的任何操作。  
  
 **服务 API:**  <xref:System.Xaml.IXamlSchemaContextProvider.SchemaContext%2A>  
  
 对于任何推迟加载操作，XAML 架构上下文都是必需的，因为同一架构上下文必须作用于推迟的区域才能集成推迟的内容。 有关 XAML 架构上下文的角色的详细信息，请参阅 [XAML Services](../../../docs/framework/xaml-services/index.md)。  
  
### IRootObjectProvider  
 **参考文档**：<xref:System.Xaml.IRootObjectProvider>  
  
 **由以下内容定义：** <xref:System.Xaml> 命名空间、System.Xaml 程序集  
  
 **相关内容：**加载路径。  
  
 **服务 API:**  <xref:System.Xaml.IRootObjectProvider.RootObject%2A>  
  
 该服务与由特定框架或框架中常用根元素类的功能公开的应用程序服务相关。 一种获取根对象的情况是连接代码隐藏和事件连结。 例如，`x:Class` 的 WPF 实现用于 XAML 标记中任何其他位置处的任何事件处理程序特性的标记编译和连结。 标记与为标记编译定义分部类的代码隐藏的连接点在根元素处。  
  
### IXamlNamespaceResolver  
 **参考文档**：<xref:System.Xaml.IXamlNamespaceResolver>  
  
 **由以下内容定义：** <xref:System.Xaml> 命名空间、System.Xaml 程序集  
  
 **相关内容：**加载路径、保存路径。  
  
 **服务 API：** <xref:System.Xaml.IXamlNamespaceResolver.GetNamespace%2A>（用于加载路径）、<xref:System.Xaml.IXamlNamespaceResolver.GetNamespacePrefixes%2A>（用于保存路径）。  
  
 <xref:System.Xaml.IXamlNamespaceResolver> 是一项服务，该服务可按照原始 XAML 标记中映射的方式基于 XAML 命名空间的前缀返回 XAML 命名空间标识符\/URI。  
  
### IProvideValueTarget  
 **参考文档**：<xref:System.Windows.Markup.IProvideValueTarget>  
  
 **由以下内容定义：** <xref:System.Windows.Markup> 命名空间、System.Xaml 程序集  
  
 **相关内容：**加载路径和保存路径。  
  
 **服务 API：** <xref:System.Windows.Markup.IProvideValueTarget.TargetObject%2A>、<xref:System.Windows.Markup.IProvideValueTarget.TargetProperty%2A>。  
  
 <xref:System.Windows.Markup.IProvideValueTarget> 可使类型转换器或标记扩展能够获取有关加载时作用位置的上下文。 实现可能使用此上下文来使某个用法失效。 例如，WPF 在其某些标记扩展（例如 <xref:System.Windows.DynamicResourceExtension>）中具有逻辑。 该逻辑检查 <xref:System.Windows.Markup.IProvideValueTarget.TargetProperty%2A> 以确保该扩展仅用于设置依赖项属性（或其他非依赖项属性的简短列表）。  
  
### IXamlNameResolver  
 **参考文档**：<xref:System.Xaml.IXamlNameResolver>  
  
 **由以下内容定义：** <xref:System.Xaml> 命名空间、System.Xaml 程序集  
  
 **相关：**加载路径对象关系图定义，解析由 `x:Name`、`x:Reference` 或特定于框架的技术标识的对象。  
  
 **服务 API：** <xref:System.Xaml.IXamlNameResolver.Resolve%2A>；用于更高级方案（如处理前向引用）的其他 API。  
  
 `x:Reference` 处理的 .NET Framework XAML 服务实现依赖于此服务。 特定框架或支持框架的工具使用此服务进行 `x:Name` 处理或等效的（<xref:System.Windows.Markup.RuntimeNamePropertyAttribute> 特性化）属性处理。  
  
### IDestinationTypeProvider  
 **参考文档**：<xref:System.Xaml.IDestinationTypeProvider>  
  
 **由以下内容定义：** <xref:System.Xaml> 命名空间、System.Xaml 程序集  
  
 **相关内容：**间接 CLR 类型信息的加载路径解析。  
  
 **服务 API：** <xref:System.Xaml.IDestinationTypeProvider.GetDestinationType%2A>  
  
 有关更多信息，请参见<xref:System.Xaml.IDestinationTypeProvider>。  
  
## 请参阅  
 <xref:System.Windows.Markup.MarkupExtension>   
 <xref:System.Xaml.XamlObjectWriter>   
 [Markup Extensions for XAML Overview](../../../docs/framework/xaml-services/markup-extensions-for-xaml-overview.md)   
 [Type Converters for XAML Overview](../../../docs/framework/xaml-services/type-converters-for-xaml-overview.md)