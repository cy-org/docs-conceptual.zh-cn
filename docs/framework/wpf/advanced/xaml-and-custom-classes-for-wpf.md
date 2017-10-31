---
title: "XAML 及 WPF 的自定义类 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "类, XAML 中的自定义类"
  - "XAML 中的自定义类"
  - "XAML, 自定义类"
ms.assetid: e7313137-581e-4a64-8453-d44e15a6164a
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# XAML 及 WPF 的自定义类
使用 XAML 标记， XAML 为已实现在 [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] framework 支持能够定义自定义类或结构的所有 [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 语言，然后访问该类。  您可以在同一标记文件中混合使用 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 定义的类型和您的自定义类型，通常是通过将自定义类型映射到 XAML 命名空间前缀。  本主题讨论自定义类必须满足可用作 XAML 元素的要求。  
  
   
  
<a name="Custom_Classes_in_Applications_vs__in_Assemblies"></a>   
## 应用程序或程序集中的自定义类  
 在 XAML 的自定义类中定义使用两种不同的方法:在代码隐藏或生成主 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序的其他代码中，或者在单独的程序集中的类后，例如为类库或使用 DLL 的可执行文件。  这些方法中的每一种都有特定的优点和缺点。  
  
-   创建类库的优点是，任何这样的自定义类都可以在许多可能不同的应用程序中共享。  单独的库也使应用程序的版本问题更易控件，并简化创建预期的类的用法的类，在 XAML 页的根元素。  
  
-   在应用程序中定义自定义类的优点是，此方法是相对轻型的方法，可最大限度减少当引入主应用程序可执行文件之外的单独程序集时遇到的部署和测试问题。  
  
-   定义在相同或不同的程序集，自定义类是否需要映射到 CLR 命名空间和 XML 命名空间之间才能用于 XAML 作为元素。  请参见 [WPF XAML 的 XAML 命名空间和命名空间映射](../../../../docs/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)。  
  
<a name="Requirements_for_a_Custom_Class_as_a_XAML_Element"></a>   
## 自定义类作为 XAML 元素的要求  
 类要能够实例化为对象元素，必须满足以下要求：  
  
-   自定义类必须是公共的且支持默认（无参数）公共构造函数。  （有关结构的说明，请参见以下各节。）  
  
-   您的自定义类不得是嵌套类。  采用常规 CLR 使用语法的嵌套类和“点”会干扰其他 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和\/或 XAML 功能（如附加属性）。  
  
 除了启用对象元素语法外，对象定义还为将该对象用作值类型的任何其他公共属性启用属性元素语法。  这是因为，对象现在可以实例化为对象元素，而且可以填充此类属性的属性元素值。  
  
### 结构  
 您定义的结构，因为自定义类型始终可以构造在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的 XAML。这是因为， [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 编译器隐式创建所有属性值初始化为其默认值的结构的默认构造函数。  在某些情况下，不需要结构的默认构造行为和\/或对象元素用法。  这可能是因为该结构在概念上同时用于填充值和函数，其中所含的值可能有互斥的解释，因此其属性都是不可设置的。  这种结构的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 示例有 <xref:System.Windows.GridLength>。  一般情况下，这种结构应该实现类型转换器，以便可以使用为结构值创建不同解释或模式的字符串约定以特性形式表示值。  该结构还应通过非默认构造函数为代码构造公开类似的行为。  
  
<a name="Requirements_for_Properties_of_a_Custom_Class_as_XAML"></a>   
## 自定义类的属性作为 XAML 特性的要求  
 属性必须引用按值类型（如基元），或者为具有默认构造函数或 XAML 处理器可以访问的专用类型转换器的类型使用类。  在 CLR XAML 实现中，XAML 处理器可通过对语言基元的本机支持或通过将 <xref:System.ComponentModel.TypeConverterAttribute> 应用到后备类型定义中的类型或成员来查找此类转换器。  
  
 或者，属性可以引用抽象类类型或接口。  对于抽象类或接口，XAML 分析的期望是，必须使用实现该接口的实际类实例或从该抽象类派生的类型实例填充属性值。  
  
 可在抽象类上声明属性，但只能在从抽象类派生的实际类上设置属性。  这是因为，无论如何，为类创建对象元素都需要类上的公共默认构造函数。  
  
### 启用了 TypeConverter 的特性语法  
 如果在类级别提供专用的特性化类型转换器，则应用的类型转换将为任何需要实例化该类型的属性启用特性语法。  类型转换器不启用该类型的对象元素用法；只有当存在该类型的默认构造函数时才会启用对象元素用法。  所以，启用了类型转换器的属性一般而言在属性语法中不可用，除非该类型本身也支持对象元素语法。  这一点的一个例外是，可以指定属性元素语法，但允许该属性元素包含一个字符串。  该用法实质上相当于特性语法用法，这样的用法不常见，除非需要对特性值进行更可靠的空白处理。  例如，以下用法是接受字符串的属性元素用法和等效的特性用法：  
  
 [!code-xml[XamlOvwSupport#GoofyTCPE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#goofytcpe)]  
  
 [!code-xml[XamlOvwSupport#GoofyTCPE2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#goofytcpe2)]  
  
 允许使用特性语法，但包含对象元素的属性元素语法的示例通过 XAML 禁止是采用 <xref:System.Windows.Input.Cursor> 类型的各个属性。  <xref:System.Windows.Input.Cursor> 类有专用类型转换器 <xref:System.Windows.Input.CursorConverter>，但未公开默认构造函数，因此 <xref:System.Windows.FrameworkElement.Cursor%2A> 属性只能通过特性语法进行设置，即使实际 <xref:System.Windows.Input.Cursor> 类型为引用类型。  
  
### 每个属性类型转换器  
 此外，属性本身也可以在属性级别声明类型转换器。  对于基于适当类型的 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 操作，通过将特性的传入字符串值作为输入进行处理，这将启用“mini language”，它将实例化内联属性类型的对象。  通常这样做是为了提供方便的访问器，而不是作为的唯一手段在 XAML 中设置一个属性。  但是，对于想要使用现有 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 类型（不提供默认构造函数或特性化类型转换器）的特性，也可以使用类型转换器。  从 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] API 的示例是采用 <xref:System.Globalization.CultureInfo> 类型的某些属性。  在这种情况下， [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用现有 [!INCLUDE[TLA#tla_winfx](../../../../includes/tlasharptla-winfx-md.md)] <xref:System.Globalization.CultureInfo> 类型改进地址用于早期版本框架的兼容性和迁移方案，但是， <xref:System.Globalization.CultureInfo> 类型不支持必需的构造函数或类型级别的类型转换可用，因为 XAML 属性值直接。  
  
 公开具有 XAML 用法的属性时，特别当您是控件作者时，尤其应考虑使用依赖项属性支持该属性。  这是尤其如此，如果使用 XAML 处理器的现有 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 实现，使用 <xref:System.Windows.DependencyProperty> ，将返回，因为可以提高性能。  对于用户期望的 XAML 可访问属性，依赖项属性将公开该属性的属性系统功能。  这些功能包括动画、数据绑定和样式支持。  有关更多信息，请参见[自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)和 [XAML 加载和依赖项属性](../../../../docs/framework/wpf/advanced/xaml-loading-and-dependency-properties.md)。  
  
### 编写和属性化类型转换器  
 有时需要编写自定义 <xref:System.ComponentModel.TypeConverter> 派生类，以便为属性类型提供类型转换。  有关如何从类型转换器派生和创建支持 XAML 用法的类型转换器，以及如何应用 <xref:System.ComponentModel.TypeConverterAttribute> 的说明，请参见 [TypeConverters 和 XAML](../../../../docs/framework/wpf/advanced/typeconverters-and-xaml.md)。  
  
<a name="Requirements_for_Events_of_a_Custom_Class_as_XAML"></a>   
## 有关自定义类事件的 XAML 事件处理程序特性语法的要求  
 若要将事件用作 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件，必须在支持默认构造函数的类上或可以在派生类中访问事件的抽象类上，将该事件公开为公共事件。  为了可方便地用作[路由事件](GTMT)，[!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件应实现显式 `add` 和 `remove` 方法，这两种方法分别添加和移除 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件签名的处理程序，并将这些处理程序转发到 <xref:System.Windows.UIElement.AddHandler%2A> 和 <xref:System.Windows.UIElement.RemoveHandler%2A> 方法。  这些方法在事件所附加到的实例的路由事件处理程序存储区中添加或删除处理程序。  
  
> [!NOTE]
>  可以使用 <xref:System.Windows.UIElement.AddHandler%2A> 直接注册路由事件的处理程序，而不用特意定义用于公开[路由事件](GTMT)的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件。  通常建议不要这样做，因为该事件不会使 XAML 特性语法来附加处理程序，并且，生成的类将为该类型的功能提供一个不太透明 XAML 视图。  
  
<a name="Collection_Properties"></a>   
## 编写集合属性  
 接受集合类型的属性具有的 XAML 语法允许您指定要添加到集合的对象。  此语法有两种显著功能。  
  
-   不需要在对象元素语法中指定属于集合对象的对象。  如果在 XAML 中指定接受集合类型的属性，则隐式存在该集合类型。  
  
-   标记中该集合属性的子元素将被处理为集合的成员。  通常，代码对集合成员的访问通过列表\/字典方法（如 `Add`）或索引器执行。  但是， XAML 语法不支持方法或索引器 \(例外情况:XAML 2009 可以支持方法，但是，使用 XAML 2009 中限制可能的 WPF 用法;请参见 [XAML 2009 语言功能](../../../../docs/framework/xaml-services/xaml-2009-language-features.md)\)。  对于生成元素树的操作，集合明显是很常见的要求，您需要在声明性 XAML 中通过某种方法填充这些集合。  因此，处理集合属性的子元素的方法是将这些子元素添加到将作为集合属性类型值的集合中。  
  
 .NET framework XAML 服务实现和 WPF XAML 处理器 WPF XAML 使用以下定义构成集合属性。  属性的属性类型必须实现以下内容之一：  
  
-   实现 <xref:System.Collections.IList>。  
  
-   实现 <xref:System.Collections.IDictionary> 或等效泛型 \(<xref:System.Collections.Generic.IDictionary%602>\)。  
  
-   从 <xref:System.Array> 派生 \(有关 XAML 中数组的更多信息，请参见 [x:Array 标记扩展](../../../../docs/framework/xaml-services/x-array-markup-extension.md)。\)  
  
-   实现 <xref:System.Windows.Markup.IAddChild>（[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 定义的接口）。  
  
 每个键入 CLR 具有 `Add` 方法， XAML 处理器使用将项添加到基础集合，在创建对象图时。  
  
> [!NOTE]
>  泛型 `List` 和 `Dictionary` 接口 \(<xref:System.Collections.Generic.IList%601> 和 <xref:System.Collections.Generic.IDictionary%602>\) 集合检测功能不支持由 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] XAML 处理器。  但是，可以将 <xref:System.Collections.Generic.List%601> 类用作基类（因为它直接实现 <xref:System.Collections.IList>），或者将 <xref:System.Collections.Generic.Dictionary%602> 用作基类（因为它直接实现 <xref:System.Collections.IDictionary>）。  
  
 声明接受集合的属性时，务必注意在该类型的新实例中初始化属性值的方式。  如果未将属性实现为依赖项属性，则使属性使用可调用集合类型构造函数的支持字段是合适的。  如果属性是依赖项属性，则可能需要将集合属性初始化为默认类型构造函数的一部分。  这是因为，依赖项属性从元数据中获取其默认值，并且您通常不希望集合属性的初始值为静态的共享集合。  对于每个包含类型实例，都应有一个集合实例。  有关更多信息，请参见[自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)。  
  
 您可以为集合属性实现自定义集合类型。  由于集合属性隐式进行处理，因此自定义集合类型不需要提供默认构造函数就可以在 XAML 中隐式使用。  但是，也可以选择为集合类型提供默认构造函数。  这是一种值得推行的做法。  除非提供默认构造函数，否则无法显式地将集合声明为对象元素。  一些标记作者可能喜欢将显式集合视作一种标记样式。  另外，在创建将集合类型用作属性值的新对象时，默认构造函数可以简化初始化要求。  
  
<a name="XAMLCONtent"></a>   
## 声明 XAML 内容属性  
 XAML 语言定义 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 内容属性的概念。  对象语法中可用的每个类恰好有一个 XAML 内容属性。  若要将属性声明为类的 XAML 内容属性，请将 <xref:System.Windows.Markup.ContentPropertyAttribute> 作为类定义的一部分进行应用。  在属性中将要使用的 XAML 内容属性的名称指定为 <xref:System.Windows.Markup.ContentPropertyAttribute.Name%2A>。  属性按名称指定为字符串，不是反射构造 \(如<xref:System.Reflection.PropertyInfo>。  
  
 您可以将集合属性指定为 XAML 内容属性。  这将导致使用该属性，由此对象元素可以有一个或多个子元素，而没有任何插入集合对象元素或属性元素标记。  这些元素然后被作为 XAML 内容属性的值进行处理，并添加到支持集合实例中。  
  
 有些现有 XAML 内容属性使用的属性类型 `Object`。  这将使 XAML 内容属性可接受基元值（如 <xref:System.String>），并可接受单个引用对象值。  如果遵从此模型，则您的类型将负责类型确定和可能类型的处理。  使用 <xref:System.Object> 内容类型的一般原因有两种，一种是支持将对象内容添加为字符串的简单方式（接受默认呈现处理），另一种是支持添加对象内容（指定非默认呈现或其他数据）的高级方式。  
  
<a name="Serializing"></a>   
## 序列化 XAML  
 对于某些情况，例如，如果您是控件作者，您可能还需要确保在 XAML 可实例化的任何对象表示形式也可以序列化到等效的 XAML 标记。  本主题中不介绍序列化要求。  请参见[控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)和[元素树和序列化](../../../../docs/framework/wpf/advanced/element-tree-and-serialization.md)。  
  
## 请参阅  
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)   
 [基元素概述](../../../../docs/framework/wpf/advanced/base-elements-overview.md)   
 [XAML 加载和依赖项属性](../../../../docs/framework/wpf/advanced/xaml-loading-and-dependency-properties.md)