---
title: "附加属性概述 | Microsoft Docs"
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
  - "附加属性 [WPF 设计器]"
ms.assetid: 75928354-dc01-47e8-a018-8409aec1f32d
caps.latest.revision: 28
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 27
---
# 附加属性概述
“附加属性”是由 XAML 定义的概念。  附加属性旨在用作可在任何对象上设置的一类全局属性。  在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]，附加属性通常定义为依赖项属性的专用形式没有常规属性 “包装”。  
  
   
  
<a name="prerequisites"></a>   
## 必备组件  
 本主题假设您从 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 类的现有依赖项属性的使用者角度了解依赖项属性，并且已阅读[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)。  若要采用本主题中的示例，如何还应当了解并知道 XAML 编写 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序。  
  
<a name="attached_properties_usage"></a>   
## 为何使用附加属性  
 附加属性的一个用途是允许不同的子元素为实际在父元素中定义的属性指定唯一值。  此方案的一个具体应用是让子元素通知父元素它们将如何在[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 中呈现。  一个示例是 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> 属性。  <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> 属性创建为一个附加属性，因为它设计为在 <xref:System.Windows.Controls.DockPanel> 中包含的元素上设置，而不是在 <xref:System.Windows.Controls.DockPanel> 本身上设置。  <xref:System.Windows.Controls.DockPanel> 类定义名为 <xref:System.Windows.Controls.DockPanel.DockProperty> 的静态 <xref:System.Windows.DependencyProperty> 字段，然后将 <xref:System.Windows.Controls.DockPanel.GetDock%2A> 和 <xref:System.Windows.Controls.DockPanel.SetDock%2A> 方法作为该[附加属性](GTMT)的公共访问器提供。  
  
<a name="attached_properties_xaml"></a>   
## XAML 中的附加属性  
 在 XAML 中，通过使用语法 *AttachedPropertyProvider*.*PropertyName* 来设置附加属性。  
  
 下面是有关如何在 XAML 中设置 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> 的一个示例：  
  
 [!code-xml[PropertiesOvwSupport#APBasicUsage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml#apbasicusage)]  
  
 请注意，上述用法与静态属性有些类似，即总是引用拥有并注册[附加属性](GTMT)的类型 <xref:System.Windows.Controls.DockPanel>，而不是引用通过名称指定的任何实例。  
  
 此外，，因为 XAML 中的附加属性是您在标记中设置，因此，只有 set 运算具有相关性。  您无法直接在 XAML 的属性访问，因此，虽然具有值进行比较的一些间接机制，例如样式中的触发器 \(有关详细信息，请参见 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)\)。  
  
### WPF 中的附加属性实现  
 在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]，在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 类型存在与 UI 表示相关的大多数附加属性实现为依赖项属性。  附加属性是 XAML 概念，该组件，而依赖项属性是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 概念。  由于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 附加属性是依赖项属性，所以它们支持依赖项属性概念 \(如属性元数据以及这些属性元数据中的默认值。  
  
<a name="howused"></a>   
## 所属类型如何使用附加属性  
 尽管可以在任何对象上设置附加属性，但这并不自动意味着设置该属性会产生实际的结果，或者该值将会被其他对象使用。  通常，附加属性是为了使来自各种可能的类层次结构或逻辑关系的对象都可以向用于定义附加属性的类型报告公用信息。  定义附加属性的类型通常采用以下模型之一：  
  
-   设计定义附加属性的类型，以便它可以是将为附加属性设置值的元素的父元素。  之后，该类型将在内部逻辑中对照某些对象树结构循环访问其子对象，获取值，并以某种方式作用于这些值。  
  
-   定义附加属性的类型将用作各种可能的父元素和内容模型的子元素。  
  
-   定义附加属性的类型表示一个服务。  其他类型为该附加属性设置值。  之后，当在服务的上下文中计算设置该属性的元素时，将通过服务类的内部逻辑获取附加属性的值。  
  
### 父级定义的附加属性示例  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 定义附加属性的最典型方案是：父元素支持子元素集合，并实现分别为每个子元素报告行为细节的行为。  
  
 <xref:System.Windows.Controls.DockPanel> 定义 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> 附加属性，并且 <xref:System.Windows.Controls.DockPanel> 具有作为呈现逻辑一部分的类级代码（具体的说，是 <xref:System.Windows.Controls.DockPanel.MeasureOverride%2A> 和 <xref:System.Windows.Controls.DockPanel.ArrangeOverride%2A>）。  一个 <xref:System.Windows.Controls.DockPanel> 实例将始终查看它的任何直接子元素是否已为 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> 设置了值。  如果是，这些值将变为应用于该特定子元素的呈现逻辑的输入。  每个嵌套的 <xref:System.Windows.Controls.DockPanel> 实例都处理自己的直接子元素集合，但对于 <xref:System.Windows.Controls.DockPanel> 如何处理 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> 值，该行为是特定于实现的。  在理论上可以有影响直接父级之外的元素的附加属性。  如果在没有 <xref:System.Windows.Controls.DockPanel> 父元素作用的元素上设置 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> 附加属性，则不会引发错误或异常。  这仅仅意味着设置了全局属性值，但它没有可以使用这一信息的当前 <xref:System.Windows.Controls.DockPanel> 父级。  
  
<a name="attached_properties_code"></a>   
## 代码中的附加属性  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的附加属性没有用于简化 get\/set 访问的典型 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)]“包装”方法。  这是因为附加属性不是必须属于设置它的实例的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 命名空间的一部分。  但是，在中，分析 XAML 时， XAML 处理器必须能够设置这些值。  若要支持有效附加属性用法，该附加属性的所有者类型必须实现专用访问器方法在窗体*PropertyName* `Get`和 `Set`*PropertyName*。  这些专用的访问器方法也有助于在代码中获取或设置附加属性。  从代码的角度而言，附加属性类似于具有方法访问器（而不是属性访问器）的支持字段，并且该支持字段可以存在于任何对象上，而不需要专门定义。  
  
 下面的示例演示如何在代码中设置附加属性。  在本示例中，`myCheckBox` 是 <xref:System.Windows.Controls.CheckBox> 类的一个实例。  
  
 [!code-csharp[PropertiesOvwSupport#APCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#apcode)]
 [!code-vb[PropertiesOvwSupport#APCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#apcode)]  
  
 类似于 XAML 大小写，则为; `myCheckBox` 尚未添加为 `myDockPanel` 的子元素由代码的第三行代码，第四行不会引发异常，但是，属性值都与 <xref:System.Windows.Controls.DockPanel> 父不会进行交互并不会因此执行。  只有当既在子元素上设置了 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName> 值，又存在 <xref:System.Windows.Controls.DockPanel> 父元素时，才会在所呈现的应用程序中产生有效的行为。  （在本例中，应设置附加属性，然后附加到树。  或者可以附加到树，然后再设置附加属性。  任何一种操作顺序得到的结果都相同。）  
  
<a name="attached_properties_metadata"></a>   
## 附加属性元数据  
 当注册属性时，会设置 <xref:System.Windows.FrameworkPropertyMetadata> 以指定属性的特征，例如，属性是否影响呈现、度量等等。  [附加属性](GTMT)的元数据通常与[依赖项属性](GTMT)的元数据没有不同。  如果您在附加属性元数据的重写中指定默认值，则该值将成为重写类的实例的隐含附加属性的默认值。  具体而言，如果某个进程通过附加属性的 `Get` 方法访问器查询该属性的值，并指定您在其中指定元数据的类的实例，将会报告默认值，而不会设置该附加属性的值。  
  
 如果您希望对属性启用属性值继承，则应使用附加属性，而不是非附加的依赖项属性。  有关详细信息，请参见[属性值继承](../../../../docs/framework/wpf/advanced/property-value-inheritance.md)。  
  
<a name="custom"></a>   
## 自定义的附加属性  
  
<a name="create_attached_properties"></a>   
### 何时创建附加属性  
 当确实需要有一个可用于定义类之外的其他类的属性设置机制时，您可能会创建[附加属性](GTMT)。  这种情况的最常见方案是布局。  现有布局属性的示例有 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=fullName>、<xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=fullName> 和 <xref:System.Windows.Controls.Canvas.Top%2A?displayProperty=fullName>。  这里启用的方案是作为布局控制元素的子元素存在的元素能够分别向其布局父元素表达布局要求，其中每个元素都设置一个被父级定义为附加属性的属性值。  
  
 使用附加属性的另一种情况是您的类表示一个服务，并且您希望类能够更加透明地集成此服务。  
  
 另一种情况是接收 [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)] [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]支持，如**“属性”**窗口编辑。  有关更多信息，请参见[控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)。  
  
 前面已提到，如果您希望使用属性值继承，应注册为一个附加属性。  
  
<a name="how_do_i_create_attached_properties"></a>   
### 如何创建附加属性  
 如果您的类将[附加属性](GTMT)严格定义为用于其他类型，那么该类不必从 <xref:System.Windows.DependencyObject> 派生。  但是，如果您遵循总体 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 模型具有该附加属性也是依赖项属性，但是，需要从 <xref:System.Windows.DependencyObject> 派生。  
  
 通过声明一个 <xref:System.Windows.DependencyProperty> 类型的 `public` `static` `readonly` 字段可以将附加属性定义为依赖项属性。  通过使用 <xref:System.Windows.DependencyProperty.RegisterAttached%2A> 方法的返回值来定义此字段。  为了遵循命名标识字段及其所表示的属性的已建立 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 模式，字段名必须与附加属性名一致，并附加字符串 `Property`。  附加属性提供程序还必须提供静态 `Get`*PropertyName* 和 `Set`*PropertyName* 方法作为访问器为附加属性;否则会导致属性系统无法使用附加属性。  
  
> [!NOTE]
>  如果省略附加属性的 get 访问器，则该属性上的数据绑定在设计工具（例如 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 和 Expression Blend）中将无法工作。  
  
#### Get 访问器  
 *PropertyName* 访问器的 `Get`签名必须是:  
  
 `public static object Get` *PropertyName* `(object`  `target` `)`  
  
-   在实现中可以将 `target` 对象指定为更具体的类型。  例如，<xref:System.Windows.Controls.DockPanel.GetDock%2A?displayProperty=fullName> 方法将参数类型定义为 <xref:System.Windows.UIElement>，因为附加属性只能在 <xref:System.Windows.UIElement> 实例上设置。  
  
-   可以在实现中将返回值指定为更具体的类型。  例如，<xref:System.Windows.Controls.DockPanel.GetDock%2A> 方法将它的类型指定为 <xref:System.Windows.Controls.Dock>，因为该值只能设置为此枚举。  
  
#### Set 访问器  
 *PropertyName* 访问器的 `Set`签名必须是:  
  
 `public static void Set` *PropertyName* `(object`  `target` `, object`  `value` `)`  
  
-   在实现中可以将 `target` 对象指定为更具体的类型。  例如，<xref:System.Windows.Controls.DockPanel.SetDock%2A> 方法将它的类型定义为 <xref:System.Windows.UIElement>，因为附加属性只能在 <xref:System.Windows.UIElement> 实例上设置。  
  
-   在实现中可以将 `value` 对象指定为更具体的类型。  例如，<xref:System.Windows.Controls.DockPanel.SetDock%2A> 方法将它的类型指定为 <xref:System.Windows.Controls.Dock>，因为该值只能设置为此枚举。  确保此方法的值是来自 XAML 加载程序的输入，在遇到在一个附加属性用法的附加属性在标记。  输入是作为 XAML 特性值的值在标记。  因此，必须存在可用于您所使用的类型的类型转换、值序列化程序或标记扩展支持，以便可以从特性值（最终仅仅是一个字符串）创建相应的类型。  
  
 下面的示例演示注册依赖项属性 \(使用 <xref:System.Windows.DependencyProperty.RegisterAttached%2A> 方法\)，以及 `Get`*PropertyName* 和 `Set`*PropertyName* 访问器。  在本示例中，附加属性名是 `IsBubbleSource`。  因此，访问器的名称必须为 `GetIsBubbleSource` 和 `SetIsBubbleSource`。  
  
 [!code-csharp[WPFAquariumSln#RegisterAttachedBubbler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#registerattachedbubbler)]
 [!code-vb[WPFAquariumSln#RegisterAttachedBubbler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#registerattachedbubbler)]  
  
#### 附加属性特性  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 定义了几个 [!INCLUDE[TLA2#tla_netframewkattr#plural](../../../../includes/tla2sharptla-netframewkattrsharpplural-md.md)]，这些属性旨在向反射进程以及反射的典型用户和诸如设计器这样的属性信息提供有关附加属性的信息。  因为附加属性具有无限制的范围的类型，设计器需要一种方式来避免为全局的压倒大多数用户在某个特定技术实现中定义使用 XAML 的所有附加属性。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 为附加属性定义的 [!INCLUDE[TLA2#tla_netframewkattr#plural](../../../../includes/tla2sharptla-netframewkattrsharpplural-md.md)] 可以用于规定应当在属性窗口中显示给定的附加属性的情形。  您可能会考虑也对自己的自定义附加属性应用这些特性.  相应的参考页中介绍了 [!INCLUDE[TLA2#tla_netframewkattr#plural](../../../../includes/tla2sharptla-netframewkattrsharpplural-md.md)]的用途和语法：  
  
-   <xref:System.Windows.AttachedPropertyBrowsableAttribute>  
  
-   <xref:System.Windows.AttachedPropertyBrowsableForChildrenAttribute>  
  
-   <xref:System.Windows.AttachedPropertyBrowsableForTypeAttribute>  
  
-   <xref:System.Windows.AttachedPropertyBrowsableWhenAttributePresentAttribute>  
  
<a name="more"></a>   
## 了解有关附加属性的更多信息  
  
-   有关创建附加属性的更多信息，请参见 [注册附加属性](../../../../docs/framework/wpf/advanced/how-to-register-an-attached-property.md)。  
  
-   有关依赖项属性和附加属性的更高级使用方案，请参见[自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)。  
  
-   您还可以将属性注册为附加属性和依赖项属性，但之后仍然需要公开“包装”实现。  在这种情况下，属性设置为该元素，也可以在任何元素通过 XAML 附加特性语法。  具有同时适用于标准用法和附加用法的方案的属性示例是 <xref:System.Windows.FrameworkElement.FlowDirection%2A?displayProperty=fullName>。  
  
## 请参阅  
 <xref:System.Windows.DependencyProperty>   
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)   
 [注册附加属性](../../../../docs/framework/wpf/advanced/how-to-register-an-attached-property.md)