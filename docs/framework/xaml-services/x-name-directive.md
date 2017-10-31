---
title: "x:Name Directive | Microsoft Docs"
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
  - "x:Name"
  - "xName"
  - "Name"
helpviewer_keywords: 
  - "x:Name attribute [XAML Services]"
  - "XAML [XAML Services], x:Name attribute"
  - "Name attribute in XAML [XAML Services]"
ms.assetid: b7e61222-e8cf-48d2-acd0-6df3b7685d48
caps.latest.revision: 27
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 27
---
# x:Name Directive
唯一标识 XAML 名称范围中的 XAML 定义元素。  XAML 名称范围及其唯一性模型可应用于实例化的对象，当框架提供 API 或实现在运行时访问 XAML 创建的对象图的行为。  
  
## XAML 属性用法  
  
```  
<object x:Name="XAMLNameValue".../>  
```  
  
## XAML 值  
  
|||  
|-|-|  
|`XAMLNameValue`|遵守 [XamlName 语法](../../../docs/framework/xaml-services/xamlname-grammar.md)限制的字符串。|  
  
## 备注  
 一旦将 `x:Name` 应用于框架的支持编程模型，该名称就会与由构造函数返回的用于保存对象引用或实例的变量等效。  
  
 `x:Name` 指令用法的值必须在 XAML 名称范围内唯一。  默认情况下，在 .NET Framework XAML Services API 使用主 XAML 名称范围时，会在单个 XAML 生产的 XAML 根元素中定义它，并包括该 XAML 生产中包含的元素。  框架可定义单个 XAML 生产中可能发生的其他离散 XAML 名称范围以解决特定方案。  例如，在 WPF 中，由任意模板定义和创建的新 XAML 名称范围也在该 XAML 生产上定义。  有关 XAML 名称范围（针对 WPF 编写，但与 XAML 名称范围概念相关）的更多信息，请参见 [WPF XAML 名称范围](../../../ocs/framework/wpf/advanced/wpf-xaml-namescopes.md)。  
  
 通常情况下 `x:Name` 不应该应用于也使用 `x:Key` 的情况。  特定现有框架的 XAML 实现引入了 `x:Key` 和 `x:Name` 之间的替换概念，但这不是建议的做法。  处理名称\/键的信息时，.NET Framework XAML 服务不支持此类替换概念，如 <xref:System.Windows.Markup.INameScope> 或 <xref:System.Windows.Markup.DictionaryKeyPropertyAttribute>。  
  
 `x:Name` 许可和名称强制唯一性的规则可能由特定实现框架定义。  但是，要能与 .NET Framework XAML 服务一起使用，XAML 命名空间惟一性应和该文档中的 <xref:System.Windows.Markup.INameScope> 定义信息一致，并且信息使用位置应遵循相同规则。  例如，[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] 实现将各种标记元素分成单独的 <xref:System.Windows.NameScope> 范围，如资源字典、由页级别 XAML 创建的逻辑树、模板及其他延迟内容，然后强制其中每个 XAML 名称范围内的 XAML 名称的唯一性。  
  
 对于使用 .NET Framework XAML 服务 XAML 对象编写器的自定义类型，可以建立或更改映射到类型中 `x:Name` 的属性。  通过引用属性名称来映射类型定义代码中的 <xref:System.Windows.Markup.RuntimeNamePropertyAttribute> 定义此行为。  <xref:System.Windows.Markup.RuntimeNamePropertyAttribute> 是一个类级属性。  
  
 使用 .NET Framework XAML 服务，用于 XAML 名称范围支持的后备逻辑可以通过 <xref:System.Windows.Markup.INameScope> 接口，以对框架中立的方式定义。  
  
## WPF 用法说明  
 在使用 XAML、分部类和代码隐藏的 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 应用程序项目的标准生成配置下，指定的 `x:Name` 成为标记编译生成任务处理 [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 时在基础代码中创建的字段的名称，并且该字段保留对对象的引用。默认情况下，创建的字段为内部字段。  您可以通过指定 [x:FieldModifier 特性](../../../docs/framework/xaml-services/x-fieldmodifier-directive.md)来更改字段访问。  在 WPF 和 Silverlight 中，序列为标记编译定义和命名特定类中字段的顺序，但初始值为空。  然后，生成名为 `InitializeComponent` 的方法将从类构造函数进行调用。  `InitializeComponent` 包括使用每个 `x:Name` 值的 `FindName` 调用，这些值存在于 XAML 定义为输入字符串的部分局部类中。  然后将返回值分配给类似名称的字段引用，用 XAML 分析中创建的对象来填补字段。  执行 `InitializeComponent` 使通过 `x:Name` \/字段名称直接而非必须显式地调用`FindName` 在任何需要引用 XAML 定义对象的时候可以引用运行时对象图。  
  
 对于使用  [!INCLUDE[TLA#tla_visualb](../../../includes/tlasharptla-visualb-md.md)] 目标并包括带 `Page` XAML 文件生成操作的 WPF 文件的应用程序，会在编译期间创建一个单独的引用属性，该属性将  `WithEvents` 关键字添加到所有具有 `x:Name` 的元素，以支持事件处理程序委托的 `Handles` 语法。  该属性始终是公共的。  有关更多信息，请参见 [Visual Basic 和 WPF 事件处理](../../../ocs/framework/wpf/advanced/visual-basic-and-wpf-event-handling.md)。  
  
 `x:Name` 由 WPF XAML 处理器用于在加载时将名称注册到 XAML 名称范围，即使在生成操作为对页面进行标记编译的情况下（例如，资源字典的宽松 XAML）也是如此。  此行为的一个原因是因为 <xref:System.Windows.Data.Binding.ElementName%2A> 绑定可能需要 `x:Name`。  有关详细信息，请参见[数据绑定概述](../../../ocs/framework/wpf/data/data-binding-overview.md)。  
  
 如前所述，`x:Name`（或 `Name`）不应用于使用 `x:Key` 的情况。  [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.ResourceDictionary> 具有特别行为，即将其自身定义为 XAML 名称范围，但对 <xref:System.Windows.Markup.INameScope> API 返回“未实现”或 null 值来作为一种强制执行该行为的方法。  如果 WPF XAML 分析程序遇到 XAML 定义的 <xref:System.Windows.ResourceDictionary> 中的 `Name` 或 `x:Name`，则不会将名称添加到任何 XAML 命名空间中。  尝试从任何 XAML 名称范围和 `FindName` 方法中查找该名称将不会返回有效结果。  
  
### x:Name 和 Name  
 许多 WPF 应用程序方案都可以完全避免使用 `x:Name` 特性，因为在默认 XAML 命名空间内为几个重要基类（如 <xref:System.Windows.FrameworkElement> 和 <xref:System.Windows.FrameworkContentElement>）指定的 `Name` 依赖项属性也具有此用途。  当代码在框架级访问具有非 `Name` 属性的元素时，仍存在一些常见的 XAML 和 WPF 方案。  例如，某些动画和演示图板支持类不支持 `Name` 属性，但为了控制动画经常需要引用代码。  应当在时间线以及在 XAML 中创建的变换上将 `x:Name` 指定为属性，前提是您计划以后在代码中引用它们。  
  
 如果 <xref:System.Windows.FrameworkElement.Name%2A> 可用作类的一个属性，则 <xref:System.Windows.FrameworkElement.Name%2A> 和 `x:Name` 可作为特性互换使用，但如果在同一元素上同时指定了这两者，则将分析异常。  如果对 XAML 进行标记编译，则将在标记编译时发生异常，否则将在加载时发生异常。  
  
 <xref:System.Windows.FrameworkElement.Name%2A> 可以使用 XAML 特性语法设置，而且在代码中使用 <xref:System.Windows.DependencyObject.SetValue%2A> 也可以设置；请注意无论在代码中如何设置 <xref:System.Windows.FrameworkElement.Name%2A> 属性，也不会在 XAML 已载入的大多数情况下在 XAML 名称范围内创建代表性字段引用。  不要尝试在代码中设置 <xref:System.Windows.FrameworkElement.Name%2A>，而应从代码中根据相应的名称范围来使用 <xref:System.Windows.NameScope> 方法。  
  
 使用带有内部文本的属性元素语法也可以设置 <xref:System.Windows.FrameworkElement.Name%2A>，但这不常见。  相反，`x:Name` 不能在 XAML 属性元素语法中设置，也不能在代码中使用 <xref:System.Windows.DependencyObject.SetValue%2A> 来设置；它只能使用特性语法在对象上设置，因为它是一条指令。  
  
## Silverlight Usage 备注。  
 单独说明了 `x:Name` for Silverlight。  更多信息，请参见 [XAML Namespace \(x:\) Language Features \(Silverlight\)](http://go.microsoft.com/fwlink/?LinkId=199081) 。  
  
## 请参阅  
 <xref:System.Windows.FrameworkElement.Name%2A?displayProperty=fullName>   
 <xref:System.Windows.FrameworkContentElement.Name%2A?displayProperty=fullName>   
 [WPF 中的树](../../../ocs/framework/wpf/advanced/trees-in-wpf.md)