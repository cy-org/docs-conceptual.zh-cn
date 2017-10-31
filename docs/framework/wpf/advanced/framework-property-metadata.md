---
title: "框架属性元数据 | Microsoft Docs"
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
  - "框架属性元数据"
  - "元数据, 框架属性"
ms.assetid: 9962f380-b885-4b61-a62e-457397083fea
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 框架属性元数据
框架属性元数据选项是针对被视为位于 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 体系结构中的 [WPF 框架级](GTMT)的对象元素的属性报告的。  通常情况下，[WPF 框架级](GTMT)指示要求诸如呈现、数据绑定和属性系统优化之类的功能由 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 演示 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 和可执行文件处理。  这些系统对框架属性元数据进行查询，以便为特定的元素属性确定特定于功能的特性。  
  
   
  
<a name="prerequisites"></a>   
## 必备组件  
 本主题假定您从 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 类的现有依赖项属性的使用者角度了解[依赖项属性](GTMT)，并且已阅读[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)。  另外，您应当已阅读[依赖项属性元数据](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)。  
  
<a name="What_Is_Communicated_by_Framework_Property"></a>   
## 框架属性元数据传达的信息  
 框架属性元数据分为以下类别：  
  
-   报告影响某个元素的布局属性（<xref:System.Windows.FrameworkPropertyMetadata.AffectsArrange%2A>、<xref:System.Windows.FrameworkPropertyMetadata.AffectsMeasure%2A> 和 <xref:System.Windows.FrameworkPropertyMetadata.AffectsRender%2A>）。  如果属性对这些相应的方面有影响，则可以在元数据中设置相应的标志，还可以在类中实现 <xref:System.Windows.FrameworkElement.MeasureOverride%2A> \/ <xref:System.Windows.FrameworkElement.ArrangeOverride%2A> 方法以便向布局系统提供特定的呈现行为和信息。  通常情况下，如果在属性元数据中任何这些布局属性为 true，则此实现会在依赖项属性中检查属性是否无效，并且只有那些无效的属性才必须请求新的布局处理过程。  
  
-   报告影响元素的父元素的布局属性（<xref:System.Windows.FrameworkPropertyMetadata.AffectsParentArrange%2A> 和 <xref:System.Windows.FrameworkPropertyMetadata.AffectsParentMeasure%2A>）。  默认情况下设置了这些标志的一些示例有 <xref:System.Windows.Documents.FixedPage.Left%2A?displayProperty=fullName> 和 <xref:System.Windows.Documents.Paragraph.KeepWithNext%2A?displayProperty=fullName>。  
  
-   <xref:System.Windows.FrameworkPropertyMetadata.Inherits%2A>.  默认情况下，依赖项属性不会继承值。  <xref:System.Windows.FrameworkPropertyMetadata.OverridesInheritanceBehavior%2A> 允许继承的路径进入可视化树中，这对于某些控件合成方案是必需的。  
  
    > [!NOTE]
    >  属性值上下文中的术语“继承”指特定于依赖项属性的情况；它意味着由于存在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统的 [WPF 框架级](GTMT)功能，子元素可以从父元素继承实际的依赖项属性值。  它与通过派生类型的托管代码类型和成员继承没有直接关系。  有关详细信息，请参见[属性值继承](../../../../docs/framework/wpf/advanced/property-value-inheritance.md)。  
  
-   报告数据绑定特性（<xref:System.Windows.FrameworkPropertyMetadata.IsNotDataBindable%2A> 和 <xref:System.Windows.FrameworkPropertyMetadata.BindsTwoWayByDefault%2A>）。  默认情况下，框架中的依赖项属性支持具有单向绑定行为的数据绑定。  如果数据绑定没有适用的场合，则可禁用数据绑定（因为这些属性应该是灵活且可扩展的，所以在默认的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 中没有太多的此类属性的示例）。  您可以针对以下两种情况将绑定设置为具有双向属性默认值：需要将控件在其组件元素中的各种行为绑定在一起（例如 <xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A>）；或者双向绑定对于用户来说是最常见、最想要的方案（例如 <xref:System.Windows.Controls.TextBox.Text%2A>）。  更改与数据绑定相关的元数据只会影响默认值；始终可以根据各个绑定更改此默认值。  有关常规的绑定模式和绑定的详细信息，请参见[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。  
  
-   报告支持日记功能的应用程序或服务是否应当对属性进行日记记录 \(<xref:System.Windows.FrameworkPropertyMetadata.Journal%2A>\)。  对于一般的元素，默认情况下不会启用日记功能，但可以针对特定的用户输入控件有选择性地启用它。  此属性旨在由 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 日记实现等日记服务读取，并且通常针对用户控件（例如应在导航步骤中保持的列表中的用户选择）设置此属性。  有关日记的信息，请参见[导航概述](../../../../docs/framework/wpf/app-development/navigation-overview.md)。  
  
<a name="Reading_FrameworkPropertyMetadata"></a>   
## 读取 FrameworkPropertyMetadata  
 前面链接中的各个属性都是 <xref:System.Windows.FrameworkPropertyMetadata> 向其直接基类 <xref:System.Windows.UIPropertyMetadata> 中添加的特定属性。  默认情况下，这些属性都为 `false`。  在必须了解这些属性值的情况下，对某个属性的元数据请求应尝试将返回的元数据强制转换为 <xref:System.Windows.FrameworkPropertyMetadata>，然后根据需要检查各个属性的值。  
  
<a name="Specifying_Metadata"></a>   
## 指定元数据  
 如果您出于将元数据应用到新的依赖项属性注册而创建新的元数据实例，则可选择要使用的元数据类：基 <xref:System.Windows.PropertyMetadata> 还是一些派生类（如 <xref:System.Windows.FrameworkPropertyMetadata>）。  通常情况下，您应使用 <xref:System.Windows.FrameworkPropertyMetadata>，尤其是在您的属性与属性系统和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 功能（例如布局和数据绑定）存在任何交互的情况下。  如果是针对更为复杂的方案，则还可以从 <xref:System.Windows.FrameworkPropertyMetadata> 派生以创建您自己的元数据报告类，使其成员承载额外的信息。  或者，您也可以使用 <xref:System.Windows.PropertyMetadata> 或 <xref:System.Windows.UIPropertyMetadata> 来传达对实现的功能的支持程度。  
  
 对于现有的属性（<xref:System.Windows.DependencyProperty.AddOwner%2A> 或 <xref:System.Windows.DependencyProperty.OverrideMetadata%2A> 调用），您应总是使用原始注册所用的元数据类型进行重写。  
  
 当您正在创建 <xref:System.Windows.FrameworkPropertyMetadata> 实例时，可通过以下两种方式使用传达框架属性特性的特定属性的值填充该元数据：  
  
1.  使用允许 `flags` 参数的 <xref:System.Windows.FrameworkPropertyMetadata> 构造函数签名。  此参数应使用 <xref:System.Windows.FrameworkPropertyMetadataOptions> 枚举标志的所有所需的合并值来填充。  
  
2.  使用无 `flags` 参数的签名之一，然后针对每个所需的特性更改将 <xref:System.Windows.FrameworkPropertyMetadata> 的每个报告布尔属性设置为 `true`。  为此，必须在构造具有此依赖项属性的任何元素之前对这些属性进行设置；布尔属性是读写的，以允许这一避免 `flags` 参数的行为，同时仍然可以填充元数据，但元数据必须在属性使用之前进行有效地密封。  因此，尝试在请求元数据之后设置属性将是无效的操作。  
  
<a name="Framework_Property_Metadata_Merge_Behavior"></a>   
## 框架属性元数据合并行为  
 重写框架属性元数据时，会合并或替换不同的元数据特性。  
  
-   将合并 <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>。  如果您添加一个新的 <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>，则该回调将存储在元数据中。  如果您没有在重写中指定 <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>，则 <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> 的值会从在元数据中指定它的最近上级提升为一个引用。  
  
-   <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A> 的实际属性系统行为是层次结构中的所有元数据所有者的实现都将保留并添加到表中，属性系统的执行顺序是最先调用派生程度最高的类的回调。  继承的回调仅运行一次，计数由将这些回调放置在元数据中的类所有。  
  
-   将替换 <xref:System.Windows.PropertyMetadata.DefaultValue%2A>。  如果您没有在重写中指定 <xref:System.Windows.PropertyMetadata.PropertyChangedCallback%2A>，则 <xref:System.Windows.PropertyMetadata.DefaultValue%2A> 的值从在元数据中指定它的最近上级获取。  
  
-   将替换 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> 实现。  如果您添加一个新的 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>，则该回调将存储在元数据中。  如果您没有在重写中指定 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>，则 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> 的值会从在元数据中指定它的最近上级提升为一个引用。  
  
-   属性系统的行为是仅调用直接元数据中的 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>，  而不保留对层次结构中所实现的其他 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> 的引用。  
  
-   <xref:System.Windows.FrameworkPropertyMetadataOptions> 枚举的标志组合为按位“或”运算。  如果指定 <xref:System.Windows.FrameworkPropertyMetadataOptions>，则不会覆盖原始选项。  若要更改某个选项，请在 <xref:System.Windows.FrameworkPropertyMetadata> 上设置对应的属性。  例如，如果原始 <xref:System.Windows.FrameworkPropertyMetadata> 对象设置 <xref:System.Windows.FrameworkPropertyMetadataOptions?displayProperty=fullName> 标志，则您可以通过将 <xref:System.Windows.FrameworkPropertyMetadata.IsNotDataBindable%2A?displayProperty=fullName> 设置为 `false` 来更改该对象。  
  
 此行为由 <xref:System.Windows.FrameworkPropertyMetadata.Merge%2A> 实现，并且可在派生的元数据类中重写。  
  
## 请参阅  
 <xref:System.Windows.DependencyProperty.GetMetadata%2A>   
 [依赖项属性元数据](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)   
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)