---
title: "控件创作概述 | Microsoft Docs"
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
  - "有关控件的创作概述"
  - "控件, 创作概述"
ms.assetid: 3d864748-cff0-4e63-9b23-d8e5a635b28f
caps.latest.revision: 32
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 29
---
# 控件创作概述
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 控件模型的扩展性极大减少了创建新控件的需要。  但在某些情况下，仍可能需要创建自定义控件。  本主题讨论可最大限度减少在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中创建自定义控件以及其他控件创作模型的需要的功能。  本主题还演示如何创建新控件。  
  
   
  
<a name="when_to_write_a_new_control"></a>   
## 编写新控件的替代方法  
 以前，如果要通过现有控件获取自定义体验，您只能更改控件的标准属性，例如背景色、边框宽度和字号。  如果希望在这些预定义参数的基础之上扩展控件的外观或行为，则需要创建新的控件，通常的方法是继承现有控件并重写负责绘制该控件的方法。  虽然这仍是一种可选方法，但也可以利用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 丰富内容模型、样式、模板和触发器来自定义现有的控件。  下面的列表提供了一些示例，演示如何在不创建新控件的情况下使用这些功能来实现统一的自定义体验。  
  
-   **丰富内容。**很多标准 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件都支持丰富内容。  例如，<xref:System.Windows.Controls.Button> 的内容属性为 <xref:System.Object> 类型，因此从理论上讲，任何内容都可以显示在 <xref:System.Windows.Controls.Button> 上。  若要让按钮显示图像和文本，可以将图像和 <xref:System.Windows.Controls.TextBlock> 添加到 <xref:System.Windows.Controls.StackPanel> 中，然后将 <xref:System.Windows.Controls.StackPanel> 分配给 <xref:System.Windows.Controls.ContentControl.Content%2A> 属性。  由于这些控件可以显示 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 可视化元素和任意数据，因此，减少了创建新控件或修改现有控件来支持复杂可视化效果的需要。  有关 <xref:System.Windows.Controls.Button> 的内容模型和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的其他内容模型的更多信息，请参见 [WPF 内容模型](../../../../docs/framework/wpf/controls/wpf-content-model.md)。  
  
-   **样式。** <xref:System.Windows.Style> 是表示控件属性的值的集合。  使用样式可创建所需控件外观和行为的可重用表示形式，而无需编写新控件。  例如，假设您希望所有 <xref:System.Windows.Controls.TextBlock> 控件的字体都为红色 Arial 字体，字号为 14。  您可以创建一个样式，将其作为资源，并相应设置适当的属性。  这样，添加到应用程序中的每个 <xref:System.Windows.Controls.TextBlock> 都将具有相同的外观。  
  
-   **数据模板。** <xref:System.Windows.DataTemplate> 可用于自定义数据在控件上的显示方式。  例如，<xref:System.Windows.DataTemplate> 可用于指定数据在 <xref:System.Windows.Controls.ListBox> 中的显示方式。  有关这种情况的示例，请参见[数据模板化概述](../../../../docs/framework/wpf/data/data-templating-overview.md)。  除了自定义数据外观之外，<xref:System.Windows.DataTemplate> 还可以包含 UI 元素，这样大大增加了自定义 UI 的灵活性。  例如，使用 <xref:System.Windows.DataTemplate> 可以创建一个 <xref:System.Windows.Controls.ComboBox>，其中每一项都包含一个复选框。  
  
-   **控件模板。** [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的很多控件都使用 <xref:System.Windows.Controls.ControlTemplate> 来定义控件的结构和外观，这样可将控件外观和控件功能分离开。通过重新定义控件的 <xref:System.Windows.Controls.ControlTemplate>，可以彻底更改控件的外观。  例如，假设您希望控件看起来像一个交通信号灯。  此控件具有简单的用户界面和功能。  该控件有三个圆形，一次只能点亮其中一个。  经过考虑之后，您可能意识到 <xref:System.Windows.Controls.RadioButton> 提供了一次只选中一项的功能，但是 <xref:System.Windows.Controls.RadioButton> 的默认外观完全不像交通信号灯上的灯。  由于 <xref:System.Windows.Controls.RadioButton> 使用控件模板来定义其外观，因此很容易重新定义 <xref:System.Windows.Controls.ControlTemplate> 以符合该控件的要求，从而使用单选按钮来制作交通信号灯。  
  
    > [!NOTE]
    >  尽管 <xref:System.Windows.Controls.RadioButton> 可以使用 <xref:System.Windows.DataTemplate>，但在本例中，只使用 <xref:System.Windows.DataTemplate> 还不够。  <xref:System.Windows.DataTemplate> 定义控件内容的外观。  对于 <xref:System.Windows.Controls.RadioButton>，指示 <xref:System.Windows.Controls.RadioButton> 是否选中的那个圆形右侧显示出来的全部都是该控件的内容。  在交通信号灯的示例中，单选按钮只需要成为可“点亮”的圆形。由于交通信号灯的外观要求与 <xref:System.Windows.Controls.RadioButton> 的默认外观存在很大差异，因此，有必要重新定义 <xref:System.Windows.Controls.ControlTemplate>。  一般而言，<xref:System.Windows.DataTemplate> 用于定义控件的内容（或数据），<xref:System.Windows.Controls.ControlTemplate> 用于定义控件的构成方式。  
  
-   **触发器。** <xref:System.Windows.Trigger> 用于在不创建新控件的情况下动态更改控件的外观和行为。  例如，假设应用程序中有多个 <xref:System.Windows.Controls.ListBox> 控件，而您希望每个 <xref:System.Windows.Controls.ListBox> 中的项在选中时都显示为红色粗体。  您首先想到的可能是创建一个从 <xref:System.Windows.Controls.ListBox> 继承的类，然后重写 <xref:System.Windows.Controls.Primitives.Selector.OnSelectionChanged%2A> 方法，以更改选中项的外观，不过，更好的方法是向 <xref:System.Windows.Controls.ListBoxItem> 的样式添加一个更改选中项外观的触发器。  触发器用于更改属性值或根据属性值执行操作。  <xref:System.Windows.EventTrigger> 用于在发生事件时执行操作。  
  
 有关样式、模板和触发器的更多信息，请参见[样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)。  
  
 一般而言，如果控件完全复制现有控件的功能，但您希望该控件具有不同的外观，则应先考虑是否可以使用本节中讨论的某些方法来更改现有控件的外观。  
  
<a name="models_for_control_authoring"></a>   
## 控件创作模型  
 通过丰富内容模型、样式、模板和触发器，最大程度地减少了创建新控件的需要。  但是，如果确实需要创建新控件，那么理解 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的不同控件创作模型就显得非常重要。[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供三个用于创建控件的一般模型，每个模型都提供不同的功能集和灵活度。  这三个模型的基类分别为 <xref:System.Windows.Controls.UserControl>、<xref:System.Windows.Controls.Control> 和 <xref:System.Windows.FrameworkElement>。  
  
### 从 UserControl 派生  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中创建控件的最简单方法是从 <xref:System.Windows.Controls.UserControl> 派生。  如果生成继承自 <xref:System.Windows.Controls.UserControl> 的控件，需要将现有组件添加到 <xref:System.Windows.Controls.UserControl>，命名这些组件，然后在 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中引用事件处理程序。  执行这些操作之后，即可在代码中引用这些命名元素和定义事件处理程序。  此开发模型与用于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序开发的模型非常相似。  
  
 如果生成正确，<xref:System.Windows.Controls.UserControl> 可以利用丰富内容、样式和触发器的优点。  但是，如果控件继承自 <xref:System.Windows.Controls.UserControl>，则使用该控件的用户将无法使用 <xref:System.Windows.DataTemplate> 或 <xref:System.Windows.Controls.ControlTemplate> 来自定义其外观。  因此，有必要从 <xref:System.Windows.Controls.Control> 类或其派生类（<xref:System.Windows.Controls.UserControl> 除外）进行派生，以便创建支持模板的自定义控件。  
  
#### 从 UserControl 派生的优点  
 如果符合以下所有情况，请考虑从 <xref:System.Windows.Controls.UserControl> 派生：  
  
-   希望以类似于生成应用程序的方式生成控件。  
  
-   控件仅由现有组件组成。  
  
-   不需要支持复杂自定义项。  
  
### 从 Control 派生  
 从 <xref:System.Windows.Controls.Control> 类派生是大多数现有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件使用的模型。  在创建继承自 <xref:System.Windows.Controls.Control> 类的控件时，可使用模板定义其外观。  通过这种方式，可以将运算逻辑从可视化表示形式中分离出来。  通过使用命令和绑定（而不是事件）并尽可能避免引用 <xref:System.Windows.Controls.ControlTemplate> 中的元素，也可确保分离 UI 和逻辑。如果控件的 UI 和逻辑正确分离，该控件的用户即可重新定义其 <xref:System.Windows.Controls.ControlTemplate>，从而自定义其外观。尽管生成自定义 <xref:System.Windows.Controls.Control> 不像生成 <xref:System.Windows.Controls.UserControl> 那样简单，自定义 <xref:System.Windows.Controls.Control> 还是提供了最大的灵活性。  
  
#### 从 Control 派生的优点  
 如果符合以下任一情况，请考虑从 <xref:System.Windows.Controls.Control> 派生，而不要使用 <xref:System.Windows.Controls.UserControl> 类：  
  
-   希望控件外观能通过 <xref:System.Windows.Controls.ControlTemplate> 进行自定义。  
  
-   希望控件支持不同的主题。  
  
### 从 FrameworkElement 派生  
 从 <xref:System.Windows.Controls.UserControl> 或 <xref:System.Windows.Controls.Control> 派生的控件依赖于组合现有元素。  很多情况下，这是一种可接受的解决方案，因为从 <xref:System.Windows.FrameworkElement> 继承的任何对象都可以位于 <xref:System.Windows.Controls.ControlTemplate> 中。  但是，某些时候，简单的元素组合不能满足控件的外观需要。  对于这些情况，使组件基于 <xref:System.Windows.FrameworkElement> 才是正确的选择。  
  
 生成基于 <xref:System.Windows.FrameworkElement> 的组件有两种标准方法：直接呈现和自定义元素组合。  直接呈现涉及的操作包括：重写 <xref:System.Windows.FrameworkElement> 的 <xref:System.Windows.UIElement.OnRender%2A> 方法，并提供显式定义组件视觉效果的 <xref:System.Windows.Media.DrawingContext> 操作。  此方法由 <xref:System.Windows.Controls.Image> 和 <xref:System.Windows.Controls.Border> 使用。  自定义元素组合涉及的操作包括使用 <xref:System.Windows.Media.Visual> 类型的对象组合组件的外观。  有关示例，请参见[使用 DrawingVisual 对象](../../../../docs/framework/wpf/graphics-multimedia/using-drawingvisual-objects.md)。  <xref:System.Windows.Controls.Primitives.Track> 是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中使用自定义元素组合的控件示例。  在同一控件中，也可以混合使用直接呈现和自定义元素组合。  
  
#### 从 FrameworkElement 派生的优点  
 如果符合以下任一情况，请考虑从 <xref:System.Windows.FrameworkElement> 派生：  
  
-   希望对控件的外观进行精确控制，而不仅仅是简单的元素组合提供的效果。  
  
-   想要通过定义自己的呈现逻辑来定义控件的外观。  
  
-   想要以一种 <xref:System.Windows.Controls.UserControl> 和 <xref:System.Windows.Controls.Control> 之外的新颖方式组合现有元素。  
  
<a name="control_authoring_basics"></a>   
## 控件创作基础知识  
 如前所述，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的最强大功能之一在于，它能够在不需要创建自定义控件的情况下，不只是通过设置控件的基本属性来更改其外观和行为。样式、数据绑定和触发器功能是通过 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 事件系统实现的。以下各部分介绍您应遵循的一些做法（与创建自定义控件时所有的模型无关），以便自定义控件的用户可以像使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 附带的控件一样使用这些功能。  
  
### 使用依赖项属性  
 当属性为依赖项属性时，可以进行下面的操作：  
  
-   在样式中设置该属性。  
  
-   将该属性绑定到数据源。  
  
-   使用动态资源作为该属性的值。  
  
-   动画处理该属性。  
  
 如果希望控件的属性支持以上任一功能，则应将该属性实现为依赖项属性。  下面的示例通过执行以下操作定义一个名为 `Value` 的依赖项属性：  
  
-   将一个名为 `ValueProperty` 的 <xref:System.Windows.DependencyProperty> 标识符定义为 `public` `static` `readonly` 字段。  
  
-   通过调用 <xref:System.Windows.DependencyProperty.Register%2A?displayProperty=fullName> 向属性系统注册该属性名，以指定以下内容：  
  
    -   属性的名称。  
  
    -   属性的类型。  
  
    -   拥有该属性的类型。  
  
    -   属性的元数据。  元数据包含该属性的默认值、<xref:System.Windows.CoerceValueCallback> 和 <xref:System.Windows.PropertyChangedCallback>。  
  
-   通过实现该属性的 `get` 和 `set` 访问器定义一个名为 `Value`（即用来注册该依赖项属性的名称）的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 包装属性。  请注意，`get` 和 `set` 访问器只是分别调用 <xref:System.Windows.DependencyObject.GetValue%2A> 和 <xref:System.Windows.DependencyObject.SetValue%2A>。  建议依赖项属性的访问器不要包含其他逻辑，因为客户端和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 可绕过这两个访问器直接调用 <xref:System.Windows.DependencyObject.GetValue%2A> 和 <xref:System.Windows.DependencyObject.SetValue%2A>。  例如，如果属性绑定到数据源，则不会调用该属性的 `set` 访问器。  不要向 get 和 set 访问器添加其他逻辑，而应使用 <xref:System.Windows.ValidateValueCallback>、<xref:System.Windows.CoerceValueCallback> 和 <xref:System.Windows.PropertyChangedCallback> 委托在值更改时进行响应或检查该值。  有关这些回调的更多信息，请参见[依赖项属性回调和验证](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md)。  
  
-   为 <xref:System.Windows.CoerceValueCallback> 定义一个名为 `CoerceValue` 的方法。  `CoerceValue` 确保 `Value` 大于或等于 `MinValue` 且小于或等于 `MaxValue`。  
  
-   为 <xref:System.Windows.PropertyChangedCallback> 定义一个名为 `OnValueChanged` 的方法。  `OnValueChanged` 创建一个 <xref:System.Windows.RoutedPropertyChangedEventArgs%601> 对象，并准备引发 `ValueChanged` 路由事件。  路由事件在下一节中讨论。  
  
 [!code-csharp[UserControlNumericUpDown#DependencyProperty](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml.cs#dependencyproperty)]
 [!code-vb[UserControlNumericUpDown#DependencyProperty](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDown/visualbasic/numericupdown.xaml.vb#dependencyproperty)]  
  
 有关更多信息，请参见[自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)。  
  
### 使用路由事件  
 就像[依赖项属性](GTMT)以附加功能扩展 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 属性的用途一样，[路由事件](GTMT)扩展了标准 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件的用途。  在创建新的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件时，将事件实现为路由事件也是一种好方法，因为路由事件支持以下行为：  
  
-   事件可以在多个控件的父级上进行处理。  如果事件是冒泡事件，则元素树中的单个父级可预订该事件。  然后，应用程序作者可以使用一个处理程序来响应多个控件的该事件。  例如，如果控件属于 <xref:System.Windows.Controls.ListBox> 中的每个项（因为它包含在 <xref:System.Windows.DataTemplate> 中），则应用程序开发人员可以为该控件的 <xref:System.Windows.Controls.ListBox> 事件定义相应的事件处理程序。  每当这些控件中的任何控件发生该事件时，都会调用该事件处理程序。  
  
-   路由事件可在 <xref:System.Windows.EventSetter> 中使用，应用程序开发人员通过 EventSetter 可以在样式内指定事件的处理程序。  
  
-   路由事件可在 <xref:System.Windows.EventTrigger> 中使用，这对于使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 对属性进行动画处理很有用。  有关更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
 下面的示例通过执行以下操作定义了一个路由事件：  
  
-   将一个名为 `ValueChangedEvent` 的 <xref:System.Windows.RoutedEvent> 标识符定义为 `public` `static` `readonly` 字段。  
  
-   通过调用 <xref:System.Windows.EventManager.RegisterRoutedEvent%2A?displayProperty=fullName> 方法注册该路由事件。  该示例在调用 <xref:System.Windows.EventManager.RegisterRoutedEvent%2A> 时指定以下信息：  
  
    -   事件的名称为 `ValueChanged`。  
  
    -   路由策略为 <xref:System.Windows.RoutingStrategy>，这意味着首先调用源（引发事件的对象）上的事件处理程序，然后从最近的父元素上的事件处理程序开始，相继调用源的各个父元素上的事件处理程序。  
  
    -   该事件处理程序的类型为 <xref:System.Windows.RoutedPropertyChangedEventHandler%601>，是用 <xref:System.Decimal> 类型构造的。  
  
    -   该事件的所属类型为 `NumericUpDown`。  
  
-   声明一个名为 `ValueChanged` 的公共事件，并包含事件访问器声明。  该示例调用 `add` 访问器声明中的 <xref:System.Windows.UIElement.AddHandler%2A> 和 `remove` 访问器声明中的 <xref:System.Windows.UIElement.RemoveHandler%2A> 来使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 事件服务。  
  
-   创建一个名为 `OnValueChanged` 的受保护的虚方法，该方法引发 `ValueChanged` 事件。  
  
 [!code-csharp[UserControlNumericUpDown#RoutedEvent](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml.cs#routedevent)]
 [!code-vb[UserControlNumericUpDown#RoutedEvent](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDown/visualbasic/numericupdown.xaml.vb#routedevent)]  
  
 有关更多信息，请参见[路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)和[创建自定义路由事件](../../../../docs/framework/wpf/advanced/how-to-create-a-custom-routed-event.md)。  
  
### 使用绑定  
 若要将控件 UI 与其逻辑分离，请考虑使用数据绑定。  如果是使用 <xref:System.Windows.Controls.ControlTemplate> 定义控件的外观，这一点尤其重要。  使用数据绑定时，或许可以避免在代码中引用 UI 的特定部分。  最好避免引用 <xref:System.Windows.Controls.ControlTemplate> 中的元素，原因是当代码引用 <xref:System.Windows.Controls.ControlTemplate> 中的元素并且 <xref:System.Windows.Controls.ControlTemplate> 发生更改时，需要将被引用的元素包含在新的 <xref:System.Windows.Controls.ControlTemplate> 中。  
  
 下面的示例更新 `NumericUpDown` 控件的 <xref:System.Windows.Controls.TextBlock>，向它分配一个名称，然后在代码中按名称引用该文本框。  
  
 [!code-xml[UserControlNumericUpDownSimple#UIRefMarkup](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDownSimple/CSharp/NumericUpDown.xaml#uirefmarkup)]  
  
 [!code-csharp[UserControlNumericUpDownSimple#UIRefCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDownSimple/CSharp/NumericUpDown.xaml.cs#uirefcode)]
 [!code-vb[UserControlNumericUpDownSimple#UIRefCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDownSimple/VisualBasic/NumericUpDown.xaml.vb#uirefcode)]  
  
 下面的示例使用绑定来达到相同的目的。  
  
 [!code-xml[UserControlNumericUpDown#Binding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml#binding)]  
  
 有关数据绑定的更多信息，请参见 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。  
  
### 设计器的设计  
 若要在 [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)]中获得对自定义 WPF 控件的支持（例如，使用“属性”窗口编辑属性），请遵循以下准则。  有关针对 [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]开发的更多信息，请参见 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)。  
  
#### 依赖项属性  
 确保实现 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] `get` 访问器和 `set` 访问器，如前面“使用依赖项属性”中所述。设计器可以使用包装来检测某个依赖项属性是否存在，但与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和控件客户端一样，在获取或设置属性时不需要使用设计器来调用访问器。  
  
#### 附加属性  
 应按照以下原则在自定义控件上实现附加属性：  
  
-   具有一个使用 <xref:System.Windows.DependencyProperty.RegisterAttached%2A> 方法创建的 `public` `static` `readonly` <xref:System.Windows.DependencyProperty>，其形式为“*属性名称*`Property`”。  传递到 <xref:System.Windows.DependencyProperty.RegisterAttached%2A> 的属性名称必须与*属性名称* 匹配。  
  
-   实现一对名为 `Set`*属性名称* 和 `Get`*属性名称* 的 `public` `static` CLR 方法。  这两种方法都应接受从 <xref:System.Windows.DependencyProperty> 派生的类作为其第一个参数。  `Set`*属性名称* 方法还接受其类型与属性的注册数据类型匹配的参数。  `Get`*属性名称* 方法应返回相同类型的值。  如果缺少 `Set`*属性名称* 方法，则该属性标记为只读。  
  
-   `Set` *属性名称* 和 `Get`*属性名称* 必须分别直接路由到目标依赖项对象的 <xref:System.Windows.DependencyObject.GetValue%2A> 和 <xref:System.Windows.DependencyObject.SetValue%2A> 方法。  通过调用方法包装或直接调用目标依赖项对象，设计器可以访问附加属性。  
  
 有关附加属性的更多信息，请参见[附加属性概述](../../../../docs/framework/wpf/advanced/attached-properties-overview.md)。  
  
### 定义和使用共享资源  
 可以将控件包含在应用程序所在的程序集中，也可以将控件打包到可在多个应用程序中使用的单独程序集中。  大多数情况下，不管您使用什么方法，本主题中讨论的信息都适用。  但有一处差异值得注意。  将控件放入应用程序所在的程序集中时，可以随意向 App.xaml 文件添加全局资源。  但只包含控件的程序集没有与之关联的 <xref:System.Windows.Application> 对象，因此 App.xaml 文件不可用。  
  
 当应用程序查找资源时，它会按以下顺序在三个级别进行查找：  
  
1.  元素级别。  
  
     系统从引用该资源的元素开始搜索，接着搜索逻辑父级的资源，依此类推，直至到达根元素。  
  
2.  应用程序级别。  
  
     由 <xref:System.Windows.Application> 对象定义的资源。  
  
3.  主题级别。  
  
     主题级别的字典存储在名为“Themes”的子文件夹中。  Themes 文件夹中的文件与主题对应。  例如，其中可能会有 Aero.NormalColor.xaml、Luna.NormalColor.xaml、Royale.NormalColor.xaml，等等。  可能还有一个名为 generic.xaml 的文件。  当系统在主题级查找资源时，它会先在特定于主题的文件中查找相应资源，然后在 generic.xaml 中进行查找。  
  
 当控件位于独立于应用程序的程序集中时，必须将全局资源放在元素级或主题级。  这两种方法都各有其优点。  
  
#### 在元素级定义资源  
 可以通过创建自定义资源词典并将其与控件的资源词典合并，在元素级定义共享资源。  采用此方法时，可以为资源文件指定任意名称，并且资源文件可以与控件位于同一文件夹中。  元素级资源还可以使用简单字符串作为键。  下面的示例创建一个名为 Dictionary1.xaml 的 <xref:System.Windows.Media.LinearGradientBrush> 资源文件。  
  
 [!code-xml[SharedResources#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/Dictionary1.xaml#1)]  
  
 定义词典后，需要将其与控件的资源词典合并。  可以使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 或代码进行合并。  
  
 下面的示例通过使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 来合并资源词典。  
  
 [!code-xml[SharedResources#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/ShapeResizer.xaml#2)]  
  
 这种方法的缺点是每次引用它时都会创建一个 <xref:System.Windows.ResourceDictionary> 对象。  例如，如果库中有 10 个自定义控件，并且您通过使用 XAML 来合并每个控件的共享资源词典，则会创建 10 个完全相同的 <xref:System.Windows.ResourceDictionary> 对象。  可以通过创建一个在代码中合并资源并返回所产生的 <xref:System.Windows.ResourceDictionary> 的静态类，来避免出现这种情况。  
  
 下面的示例创建了一个返回共享的 <xref:System.Windows.ResourceDictionary> 的类。  
  
 [!code-csharp[SharedResources#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/SharedDictionaryManager.cs#3)]  
  
 下面的示例先在一个自定义控件的构造函数中将共享资源与该控件的资源合并，然后再调用 `InitilizeComponent`。  由于 `SharedDictionaryManager.SharedDictionary` 为静态属性，因此 <xref:System.Windows.ResourceDictionary> 仅创建一次。  因为资源词典是在调用 `InitializeComponent` 前合并的，所以控件可以在其 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件中使用资源。  
  
 [!code-csharp[SharedResources#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/ShapeResizer.xaml.cs#4)]  
  
#### 在主题级定义资源  
 通过 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 可以为不同的 Windows 主题创建资源。  作为控件作者，您可以为特定主题定义资源，以根据所使用的主题更改控件的外观。  例如，Windows 经典主题（Windows 2000 的默认主题）中 <xref:System.Windows.Controls.Button> 的外观不同于 Windows Luna 主题（Windows XP 的默认主题）中 <xref:System.Windows.Controls.Button> 的外观，原因是 <xref:System.Windows.Controls.Button> 针对每种主题使用的 <xref:System.Windows.Controls.ControlTemplate> 不同。  
  
 特定于主题的资源以特定文件名保留在资源词典中。  这些文件必须位于一个名为 `Themes` 的文件夹中，此文件夹是包含相应控件的文件夹的子文件夹。  下表列出了资源词典文件以及与每个文件关联的主题：  
  
|资源词典文件名|Windows 主题|  
|-------------|----------------|  
|`Classic.xaml`|Windows XP 中的经典 Windows 9x\/2000 外观|  
|`Luna.NormalColor.xaml`|Windows XP 上的默认蓝色主题|  
|`Luna.Homestead.xaml`|Windows XP 上的橄榄色主题|  
|`Luna.Metallic.xaml`|Windows XP 上的银色主题|  
|`Royale.NormalColor.xaml`|Windows XP Media Center Edition 上的默认主题|  
|`Aero.NormalColor.xaml`|Windows Vista 上的默认主题|  
  
 您无需为每一种主题都定义资源。  如果没有为特定主题定义资源，则控件会在 `Classic.xaml` 中检查资源。  如果在与当前主题对应的文件或 `Classic.xaml` 中没有定义资源，则控件会使用常规资源，该资源位于名为 `generic.xaml` 的资源词典文件中。  `generic.xaml` 文件与特定于主题的资源词典文件位于同一文件夹中。  尽管 `generic.xaml` 不与特定的 Windows 主题对应，但它仍是一个主题级词典。  
  
 [NumericUpDown Custom Control with Theme and UI Automation Support Sample](http://go.microsoft.com/fwlink/?LinkID=160025)（带有主题和 UI 自动化支持的 NumericUpDown 自定义控件示例）中包含两个用于 `NumericUpDown` 控件的资源词典：一个在 generic.xaml 中，另一个在 Luna.NormalColor.xaml 中。  您可以运行应用程序并在 Windows XP 中的银色主题和另一主题之间切换，以查看这两个控件模板之间的差别。  （如果您运行的是 Windows Vista，则可以将 Luna.NormalColor.xaml 重命名为 Aero.NormalColor.xaml，然后在两个主题之间切换，例如在 Windows 经典主题和 Windows Vista 的默认主题之间切换。）  
  
 将 <xref:System.Windows.Controls.ControlTemplate> 放入任何特定于主题的资源词典文件中时，都必须为控件创建静态构造函数，并对 <xref:System.Windows.FrameworkElement.DefaultStyleKey%2A> 调用 <xref:System.Windows.DependencyProperty.OverrideMetadata%28System.Type%2CSystem.Windows.PropertyMetadata%29> 方法，如下例所示。  
  
 [!code-csharp[CustomControlNumericUpDownOneProject#StaticConstructor](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDownOneProject/CSharp/NumericUpDown.cs#staticconstructor)]
 [!code-vb[CustomControlNumericUpDownOneProject#StaticConstructor](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDownOneProject/visualbasic/numericupdown.vb#staticconstructor)]  
  
##### 定义和引用主题资源的键  
 在元素级定义资源时，可以指定一个字符串作为其键，然后通过该字符串访问该资源。  在主题级定义资源时，必须使用 <xref:System.Windows.ComponentResourceKey> 作为键。  下面的示例在 generic.xaml 中定义了一项资源。  
  
  
  
 下面的示例通过指定 <xref:System.Windows.ComponentResourceKey> 作为键来引用该资源。  
  
  
  
##### 指定主题资源的位置  
 若要找到控件的资源，承载应用程序需要知道相应程序集包含特定于控件的资源。  可以通过向包含此控件的程序集添加 <xref:System.Windows.ThemeInfoAttribute> 来达到此目的。  <xref:System.Windows.ThemeInfoAttribute> 具有一个 <xref:System.Windows.ThemeInfoAttribute.GenericDictionaryLocation%2A> 属性和一个 <xref:System.Windows.ThemeInfoAttribute.ThemeDictionaryLocation%2A> 属性，前者指定常规资源的位置，后者指定特定于主题的资源的位置。  
  
 下面的示例将 <xref:System.Windows.ThemeInfoAttribute.GenericDictionaryLocation%2A> 和 <xref:System.Windows.ThemeInfoAttribute.ThemeDictionaryLocation%2A> 属性设置为 <xref:System.Windows.ResourceDictionaryLocation>，以指定常规资源和特定于主题的资源与控件位于同一程序集中。  
  
 [!code-csharp[CustomControlNumericUpDown#ThemesSection](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/Properties/AssemblyInfo.cs#themessection)]
 [!code-vb[CustomControlNumericUpDown#ThemesSection](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/my project/assemblyinfo.vb#themessection)]  
  
## 请参阅  
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)   
 [WPF 中的 Pack URI](../../../../docs/framework/wpf/app-development/pack-uris-in-wpf.md)   
 [控件自定义](../../../../docs/framework/wpf/controls/control-customization.md)