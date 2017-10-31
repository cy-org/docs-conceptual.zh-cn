---
title: "自定义依赖项属性 | Microsoft Docs"
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
  - "自定义依赖项属性"
  - "依赖项属性, 自定义"
  - "实现, 包装"
  - "元数据, 属性"
  - "属性, 元数据"
  - "属性, 注册"
  - "注册属性"
  - "包装, 实现"
ms.assetid: e6bfcfac-b10d-4f58-9f77-a864c2a2938f
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# 自定义依赖项属性
本主题介绍 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序开发人员和组件作者可能希望创建自定义的[依赖项属性](GTMT)的原因，以及介绍可以提高该属性的性能、可用性或通用性的实现步骤和某些实现选项。  
  
   
  
<a name="prerequisites"></a>   
## 必备组件  
 本主题假定您从 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 类的现有依赖项属性的使用者角度了解依赖项属性，并且已阅读[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)主题。  若要采用本主题中的示例，还应当了解[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 并知道如何编写 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序。  
  
<a name="whatis"></a>   
## 什么是依赖项属性？  
 您可以启用本应为[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 属性的属性来支持样式设置、数据绑定、继承、动画和默认值，方法是将其作为[依赖项属性](GTMT)进行实现。  依赖项属性是通过调用 <xref:System.Windows.DependencyProperty.Register%2A> 方法（或 <xref:System.Windows.DependencyProperty.RegisterReadOnly%2A>）在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统中注册，并通过 <xref:System.Windows.DependencyProperty> 标识符字段备份的属性。  依赖项属性只能由 <xref:System.Windows.DependencyObject> 类型使用，但 <xref:System.Windows.DependencyObject> 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 类层次结构中的级别很高，因此，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的大多数可用类都支持依赖项属性。  有关依赖项属性和此 [!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)] 中用于描述依赖项属性的某些术语和约定的更多信息，请参见[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)。  
  
<a name="example_dp"></a>   
## 依赖项属性示例  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 类上实现的依赖项属性示例包括 <xref:System.Windows.Controls.Control.Background%2A> 属性、<xref:System.Windows.FrameworkElement.Width%2A> 属性和 <xref:System.Windows.Controls.TextBox.Text%2A> 属性等。  类公开的每个依赖项属性都有一个对应的、在同一个类上公开的 <xref:System.Windows.DependencyProperty> 类型的公共静态字段。这是依赖项属性的标识符。  该标识符的命名约定为：在[依赖项属性](GTMT)的名称后面追加字符串 `Property`。  例如，与 <xref:System.Windows.Controls.Control.Background%2A> 属性对应的 <xref:System.Windows.DependencyProperty> 标识符字段为 <xref:System.Windows.Controls.Control.BackgroundProperty>。  该标识符用于在注册[依赖项属性](GTMT)时存储其相关信息，并且在随后可用于与[依赖项属性](GTMT)有关的其他操作，如调用 <xref:System.Windows.DependencyObject.SetValue%2A>。  
  
 如[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)中所述，由于“包装”实现，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的所有依赖项属性（大多数[附加属性](GTMT)除外）也是 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 属性。  因此，可以从代码中获取或设置依赖项属性，方法是按照与使用其他 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 属性相同的方式来调用定义包装的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 访问器。  作为确立的依赖项属性的使用者，您通常不会使用 <xref:System.Windows.DependencyObject> 方法 <xref:System.Windows.DependencyObject.GetValue%2A> 和 <xref:System.Windows.DependencyObject.SetValue%2A>，这两种方法是基础属性系统的连接点。  相反，[!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 属性的现有实现会已使用相应的标识符字段在该属性的 `get` 和 `set` 包装实现内调用 <xref:System.Windows.DependencyObject.GetValue%2A> 和 <xref:System.Windows.DependencyObject.SetValue%2A>。  如果要亲自实现自定义的依赖项属性，则需要用类似的方法定义包装。  
  
<a name="backing_with_dp"></a>   
## 何时应实现依赖项属性？  
 在类上实现属性时，只要类派生自 <xref:System.Windows.DependencyObject>，便可以选择使用 <xref:System.Windows.DependencyProperty> 标识符来备份属性，从而将其设置为依赖项属性。  将属性设置为依赖项属性并不总是必要或适当，具体取决于方案需要。  有时，使用私有字段备份属性的典型方法便能满足要求。  但是，只要您希望属性支持以下一种或多种 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 功能，就应将属性作为[依赖项属性](GTMT)来实现：  
  
-   希望可在样式中设置属性。  有关更多信息，请参见[样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)。  
  
-   希望属性支持数据绑定。  有关数据绑定依赖项属性的更多信息，请参见[绑定两个控件的属性](../../../../docs/framework/wpf/data/how-to-bind-the-properties-of-two-controls.md)。  
  
-   希望可使用动态资源引用设置属性。  有关更多信息，请参见[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
-   希望从元素树中的父元素自动继承属性值。  在这种情况下，即使还为 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 访问创建了属性包装，也应使用 <xref:System.Windows.DependencyProperty.RegisterAttached%2A> 方法进行注册。  有关更多信息，请参见[属性值继承](../../../../docs/framework/wpf/advanced/property-value-inheritance.md)。  
  
-   希望属性可进行动画处理。  有关更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
-   希望属性系统在属性系统、环境或用户执行的操作或者读取并使用样式更改了属性以前的值时报告。  通过使用属性元数据，属性可以指定将在每次属性系统确定属性值已被明确更改时调用的回调方法。  相关概念是属性值强制。  有关更多信息，请参见[依赖项属性回调和验证](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md)。  
  
-   希望使用已建立的、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 进程也使用的元数据约定，例如报告更改属性值时是否要求布局系统重新编写元素的可视化对象。  或者，希望能够使用元数据重写，以便派生类可更改基于元数据的特性（如默认值）。  
  
-   希望自定义控件的属性接收 [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)] [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]支持，如**“属性”**窗口编辑。  有关更多信息，请参见[控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)。  
  
 检查这些方案时，还应考虑是否可以通过重写现有[依赖项属性](GTMT)的元数据，而不是实现一个全新属性来实现方案。  元数据重写可行与否取决于方案以及方案与现有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 依赖项属性和类的实现的相似情况。  有关重写现有属性的元数据的更多信息，请参见[依赖项属性元数据](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)。  
  
<a name="checklist"></a>   
## 定义依赖项属性的检查表  
 定义依赖项属性包括四个不同的概念。  这些概念并不一定是严格的过程步骤，因为其中某些概念最后在实现中被组合为单行代码：  
  
-   （可选）为依赖项属性创建属性元数据。  
  
-   在属性系统中注册属性名称，并指定所有者类型和属性值的类型。  如果使用了属性元数据，则也应同时指定。  
  
-   在所有者类型上将 <xref:System.Windows.DependencyProperty> 标识符定义为 `public` `static` `readonly` 字段。  
  
-   定义其名称与依赖项属性的名称匹配的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]“包装”属性。  实现 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]“包装”属性的 `get` 和 `set` 访问器，以便与支持此属性的依赖项属性进行连接。  
  
<a name="registering"></a>   
### 在属性系统中注册属性  
 为将属性设置为[依赖项属性](GTMT)，必须在属性系统维护的表中注册该属性，并为其指定一个唯一的标识符，以用作属性系统后续操作的限定符。  这些操作可能是内部操作，也可能是您自己的代码调用属性系统 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]。  若要注册属性，请在类体中调用 <xref:System.Windows.DependencyProperty.Register%2A> 方法（在类的内部，但在任何成员定义的外部）。  <xref:System.Windows.DependencyProperty.Register%2A> 方法调用还提供了标识符字段以作为返回值。  在其他成员定义外部执行 <xref:System.Windows.DependencyProperty.Register%2A> 调用的原因是：使用此返回值可以分配和创建一个类型为 <xref:System.Windows.DependencyProperty> 的 `public` `static` `readonly` 字段，以作为类的一部分。  此字段将成为依赖项属性的标识符。  
  
 [!code-csharp[WPFAquariumSln#RegisterAG](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#registerag)]
 [!code-vb[WPFAquariumSln#RegisterAG](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#registerag)]  
  
<a name="nameconventions"></a>   
### 依赖项属性名称约定  
 您必须完全遵循为依赖项属性建立的有关命名约定，但例外情况除外。  
  
 如此例中所示，依赖项属性本身将具有一个基本名称“AquariumGraphic”，该名称是作为 <xref:System.Windows.DependencyProperty.Register%2A> 的第一个参数提供的。  该名称在每个注册类型中必须唯一。  通过基类型继承的依赖项属性将被视为已是注册类型的一部分；无法再次注册已继承属性的名称。  但是，即使不继承该依赖项属性，也可以使用一种方法来添加作为依赖项属性所有者的类；有关详细信息，请参见[依赖项属性元数据](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)。  
  
 创建标识符字段时，请将此字段命名为所注册的属性名称，并加上后缀 `Property`。  此字段是依赖项属性的标识符，随后将用作包装中进行的 <xref:System.Windows.DependencyObject.SetValue%2A> 和 <xref:System.Windows.DependencyObject.GetValue%2A> 调用的输入，供任何其他代码通过您自己的代码、允许的任何外部代码访问、属性系统以及可能通过 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器来访问属性。  
  
> [!NOTE]
>  在类体中定义依赖项属性是典型的实现，但是也可以在类静态构造函数中定义依赖项属性。  如果您需要多行代码来初始化依赖项属性，则此方法可能会很有意义。  
  
<a name="wrapper1"></a>   
### 实现“包装”  
 包装实现应调用 `get` 实现中的 <xref:System.Windows.DependencyObject.GetValue%2A> 和 `set` 实现中的 <xref:System.Windows.DependencyObject.SetValue%2A>。（为清楚起见，此处还显示了原始注册调用和字段。）  
  
 除例外情况以外，包装实现在其他情况中应只分别执行 <xref:System.Windows.DependencyObject.GetValue%2A> 和 <xref:System.Windows.DependencyObject.SetValue%2A> 操作。  [XAML 加载和依赖项属性](../../../../docs/framework/wpf/advanced/xaml-loading-and-dependency-properties.md)主题中对其原因进行了讨论。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 类中提供的所有现有公共依赖项属性都使用这一简单的包装实现模型；依赖项属性如何工作的大部分复杂性或者在本质上是一种属性系统行为，或者是通过其他概念（如通过属性元数据进行强制回调或属性更改回调）实现的。  
  
 [!code-csharp[WPFAquariumSln#AGWithWrapper](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#agwithwrapper)]
 [!code-vb[WPFAquariumSln#AGWithWrapper](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#agwithwrapper)]  
  
 此外，按照约定，包装属性的名称必须与所选择并指定为注册该属性的 <xref:System.Windows.DependencyProperty.Register%2A> 调用的第一个参数的名称相同。  如果属性不遵循该约定，尽管不一定要禁用所有可能的用法，但您将会遇到几个突出的问题：  
  
-   某些方面的样式和模板将不起作用。  
  
-   许多工具和设计器必须依赖于命名约定，才能正确序列化 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，或按每个属性级别提供设计器环境帮助。  
  
-   [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 加载程序的当前实现会完全跳过包装，并且在处理特性值时依赖于命名约定。  有关更多信息，请参见[XAML 加载和依赖项属性](../../../../docs/framework/wpf/advanced/xaml-loading-and-dependency-properties.md)。  
  
<a name="metadata"></a>   
### 新依赖项属性的属性元数据  
 注册依赖项属性时，通过属性系统进行的注册将会创建元数据对象以存储属性特性。  如果属性是使用 <xref:System.Windows.DependencyProperty.Register%2A> 的简单签名注册的，则会设置其中许多特性的默认值。  通过 <xref:System.Windows.DependencyProperty.Register%2A> 的其他签名，可以在注册属性时指定所需的元数据。  为依赖项属性提供的最常见元数据是为它们提供一个默认值，该默认值适用于使用该属性的新实例。  
  
 如果要创建在 <xref:System.Windows.FrameworkElement> 的派生类上存在的依赖项属性，则可以使用更专用的元数据类 <xref:System.Windows.FrameworkPropertyMetadata>，而不是 <xref:System.Windows.PropertyMetadata> 基类。  <xref:System.Windows.FrameworkPropertyMetadata> 类的构造函数具有几种签名，您可以在其中组合指定多个元数据特性。  如果要仅指定默认值，请使用接受类型为 <xref:System.Object> 的单个参数的签名，  并将该对象参数作为属性特定于类型的默认值进行传递。（提供的默认值必须是 <xref:System.Windows.DependencyProperty.Register%2A> 调用中作为 `propertyType` 参数提供的类型。）  
  
 对于 <xref:System.Windows.FrameworkPropertyMetadata>，还可以为属性指定元数据选项标志。  在注册之后，这些标志将转换为属性元数据中的不同属性，用于将某些条件传送给其他进程（如布局引擎）。  
  
#### 设置相应的元数据标志  
  
-   如果属性（或属性值更改）影响[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]，尤其是影响布局系统在页面中调整元素大小或呈现元素的方式，请设置以下一个或多个标志：<xref:System.Windows.FrameworkPropertyMetadataOptions>、<xref:System.Windows.FrameworkPropertyMetadataOptions> 和 <xref:System.Windows.FrameworkPropertyMetadataOptions>。  
  
    -   <xref:System.Windows.FrameworkPropertyMetadataOptions> 指示在对此属性进行更改时，需要更改包含对象在父对象中可能需要更多或较少空间的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 呈现。  例如，“Width”属性应设置此标志。  
  
    -   <xref:System.Windows.FrameworkPropertyMetadataOptions> 指示在对此属性进行更改时，需要更改通常无须更改专用空间、但又指示该空间中的位置已发生了更改的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 呈现。  例如，“Alignment”属性应设置此标志。  
  
    -   <xref:System.Windows.FrameworkPropertyMetadataOptions> 指示已发生了某些不会影响布局和度量，但确实需要其他呈现的其他更改。  更改现有元素的颜色的属性便是一个示例，如“Background”。  
  
    -   这些标志在元数据中通常用作协议，以便您自己重写实现属性系统或布局回调。  例如，如果实例的任何属性报告值发生更改，并且在其元数据中将 <xref:System.Windows.FrameworkPropertyMetadata.AffectsArrange%2A> 设置为 `true`，则您可能具有将调用 <xref:System.Windows.UIElement.InvalidateArrange%2A> 的 <xref:System.Windows.DependencyObject.OnPropertyChanged%2A> 回调。  
  
-   某些属性可能会影响包含父元素的呈现特性，采取的方法是超出上面提到的所需大小的更改。  例如，流文档模型中使用的 <xref:System.Windows.Documents.Paragraph.MinOrphanLines%2A> 属性，其中，对该属性进行的更改可能会改变包含段落的流文档的整体呈现。  使用 <xref:System.Windows.FrameworkPropertyMetadataOptions> 或 <xref:System.Windows.FrameworkPropertyMetadataOptions> 可以确定您自己的属性中的类似情况。  
  
-   默认情况下，依赖项属性支持数据绑定。  对于没有实际的数据绑定方案，或大型对象的数据绑定性能被识别为问题等情况，可以特意禁用数据绑定。  
  
-   默认情况下，依赖项属性的数据绑定 <xref:System.Windows.Data.Binding.Mode%2A> 默认为 <xref:System.Windows.Data.BindingMode>。  您可以根据绑定实例，将绑定始终更改为 <xref:System.Windows.Data.BindingMode>；有关详细信息，请参见[指定绑定的方向](../../../../docs/framework/wpf/data/how-to-specify-the-direction-of-the-binding.md)。  但是，作为依赖项属性作者，您可以选择将该属性设置为默认使用 <xref:System.Windows.Data.BindingMode> 绑定模式。  现有依赖项属性的一个示例是 <xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A?displayProperty=fullName>；该属性的方案为 <xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A> 设置逻辑和 <xref:System.Windows.Controls.MenuItem> 合成与默认的主题样式进行交互。  <xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A> 属性逻辑以本机方式使用数据绑定来根据其他状态属性和方法调用维护属性状态。  另一个默认情况下绑定 <xref:System.Windows.Data.BindingMode> 的示例属性是 <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=fullName>。  
  
-   此外，还可以通过设置 <xref:System.Windows.FrameworkPropertyMetadataOptions> 标志，在自定义的依赖项属性中启用属性继承。  对于父元素和子元素具有相同属性的情况，属性继承是很有用的，它使得子元素可将该特定属性的值设置为与父元素所设相同的值。  可继承的属性的一个示例是 <xref:System.Windows.FrameworkElement.DataContext%2A>，该属性用于绑定操作，以便为数据表示启用重要的主\-从方案。  通过将 <xref:System.Windows.FrameworkElement.DataContext%2A> 设置为可继承，任何子元素也会继承该数据上下文。  由于属性值继承，您可以在页面或应用程序根目录中指定数据上下文，从而不需要为所有可能的子元素的绑定重新指定数据上下文。  <xref:System.Windows.FrameworkElement.DataContext%2A> 也是一个用于阐释继承重写默认值的很好的示例，但是，始终可在任何特定子元素上对其进行本地设置；有关详细信息，请参见[对分层数据使用主\-从模式](../../../../docs/framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-data.md)。  属性值继承可能会具有一定的性能开销，因此应谨慎使用；有关详细信息，请参见[属性值继承](../../../../docs/framework/wpf/advanced/property-value-inheritance.md)。  
  
-   设置 <xref:System.Windows.FrameworkPropertyMetadataOptions> 标志可指示导航日记服务是否应检测或使用依赖项属性。  <xref:System.Windows.Controls.Primitives.Selector.SelectedIndex%2A> 属性就是一个示例；导航日记历史记录时，在选择控件中选择的任何项都应保持不变。  
  
<a name="RODP"></a>   
## 只读依赖项属性  
 可以定义只读的依赖项属性。  但是，为何可将属性定义为只读的情况略有不同，在该过程中，将在属性系统中注册属性并公开标识符。  有关更多信息，请参见[只读依赖项属性](../../../../docs/framework/wpf/advanced/read-only-dependency-properties.md)。  
  
<a name="CTDP"></a>   
## 集合类型依赖项属性  
 集合类型依赖项属性具有一些需要考虑的其他实现问题。  有关详细信息，请参见[集合类型依赖项属性](../../../../docs/framework/wpf/advanced/collection-type-dependency-properties.md)。  
  
<a name="SecurityC"></a>   
## 依赖项属性安全注意事项  
 依赖项属性应声明为公共属性。  依赖项属性标识符字段应声明为公共静态字段。  即使您尝试声明其他访问级别（如“受保护”），也始终可通过标识符并结合属性系统 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 来访问依赖项属性。  由于元数据报告或值确定 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 属于属性系统，因此甚至可以访问受保护的标识符字段，例如 <xref:System.Windows.LocalValueEnumerator>。  有关更多信息，请参见[依赖项属性的安全性](../../../../docs/framework/wpf/advanced/dependency-property-security.md)。  
  
<a name="DPCtor"></a>   
## 依赖项属性和类构造函数  
 托管代码编程（通常通过 FxCop 等代码分析工具来强制执行）的一般原则是：类构造函数不应调用虚方法。  这是因为构造函数可作为派生的类构造函数的基本初始化来调用，并且可能会在所构造的对象实例的不完全初始化状态下通过构造函数输入虚方法。  从已派生自 <xref:System.Windows.DependencyObject> 的任何类派生时，应注意属性系统本身会在内部调用和公开虚方法。  这些虚方法属于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统服务。  通过重写这些方法，派生类可以参与值确定。  为了避免运行时初始化出现潜在问题，不应在类的构造函数中设置依赖项属性值，除非您遵循非常具体的构造函数模式。  有关详细信息，请参见[DependencyObject 的安全构造函数模式](../../../../docs/framework/wpf/advanced/safe-constructor-patterns-for-dependencyobjects.md)。  
  
## 请参阅  
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [依赖项属性元数据](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)   
 [控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)   
 [集合类型依赖项属性](../../../../docs/framework/wpf/advanced/collection-type-dependency-properties.md)   
 [依赖项属性的安全性](../../../../docs/framework/wpf/advanced/dependency-property-security.md)   
 [XAML 加载和依赖项属性](../../../../docs/framework/wpf/advanced/xaml-loading-and-dependency-properties.md)   
 [DependencyObject 的安全构造函数模式](../../../../docs/framework/wpf/advanced/safe-constructor-patterns-for-dependencyobjects.md)