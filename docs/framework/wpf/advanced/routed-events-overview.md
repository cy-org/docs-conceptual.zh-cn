---
title: "路由事件概述 | Microsoft Docs"
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
  - "附加事件"
  - "Bubbling — 冒泡"
  - "按钮集, 分组"
  - "事件, 附加的"
  - "事件, 路由"
  - "分组按钮集"
  - "路由事件"
  - "事件的路由策略"
  - "Tunneling — 隧道"
ms.assetid: 1a2189ae-13b4-45b0-b12c-8de2e49c29d2
caps.latest.revision: 29
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 28
---
# 路由事件概述
本主题描述 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中路由事件的概念。  本主题定义路由事件术语，描述路由事件如何通过元素树来路由，概述如何处理路由事件，并介绍如何创建您自己的自定义路由事件。  
  
   
  
<a name="prerequisites"></a>   
## 必备组件  
 本主题假设您对如下内容有基本的了解：[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)]、面向对象的编程以及如何用树的概念来说明 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素之间的关系。  为了按照本主题中的示例操作，您还应当了解[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 并知道如何编写非常基本的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序或页。  有关更多信息，请参见 [演练：开始使用 WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)和 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)。  
  
<a name="routing"></a>   
## 什么是路由事件？  
 可以从功能或实现的角度来考虑路由事件。  此处对这两种定义均进行了说明，因为用户当中有的认为前者更有用，而有的则认为后者更有用。  
  
 功能定义：路由事件是一种可以针对元素树中的多个侦听器（而不是仅针对引发该事件的对象）调用处理程序的事件。  
  
 实现定义：[路由事件](GTMT)是一个 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件，可以由 <xref:System.Windows.RoutedEvent> 类的实例提供支持并由 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 事件系统来处理。  
  
 典型的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中包含许多元素。  无论这些元素是在代码中创建的还是在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中声明的，它们构成了一个彼此关联的元素树。  根据事件的定义，事件路由可以按两种方向之一传播，但是通常会在元素树中从源元素向上“冒泡”，直到它到达元素树的根（通常是页面或窗口）。  如果您以前用过 DHTML 对象模型，则可能会熟悉这个冒泡概念。  
  
 请考虑下面的简单元素树：  
  
 [!code-xml[EventOvwSupport#GroupButton](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml#groupbutton)]  
  
 此元素树生成类似如下的内容：  
  
 ![“是”、“否”和“取消”按钮](../../../../docs/framework/wpf/advanced/media/routedevent-ovw-1.png "RoutedEvent\_ovw\_1")  
  
 在这个简化的元素树中，<xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件的源是某个 <xref:System.Windows.Controls.Button> 元素，而所单击的 <xref:System.Windows.Controls.Button> 是有机会处理该事件的第一个元素。  但是，如果附加到 <xref:System.Windows.Controls.Button> 的任何处理程序均未作用于该事件，则该事件将向上冒泡到元素树中的 <xref:System.Windows.Controls.Button> 父级（即 <xref:System.Windows.Controls.StackPanel>）。  该事件可能会冒泡到 <xref:System.Windows.Controls.Border>，然后会到达元素树的页面根（未显示出来）。  
  
 换言之，此 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件的事件路由为：  
  
 Button\-\-\>StackPanel\-\-\>Border\-\-\>...  
  
### 路由事件的顶级方案  
 下面简要概述了需运用路由事件的方案，以及为什么典型的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件不适合这些方案：  
  
 **控件的撰写和封装：** [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的各个控件都有一个丰富的内容模型。  例如，可以将图像放在 <xref:System.Windows.Controls.Button> 的内部，这会有效地扩展按钮的可视化树。  但是，所添加的图像不得中断命中测试行为（该行为会使按钮响应对图像内容的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click>），即使用户所单击的像素在技术上属于该图像也是如此  
  
 **单一处理程序附加点：**在 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]中，必须多次附加同一个处理程序，才能处理可能是从多个元素引发的事件。  路由事件使您可以只附加该处理程序一次（像上例中那样），并在必要时使用处理程序逻辑来确定该事件源自何处。  例如，这可以是前面显示的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 的处理程序：  
  
 [!code-csharp[EventOvwSupport#GroupButtonCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml.cs#groupbuttoncodebehind)]
 [!code-vb[EventOvwSupport#GroupButtonCodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/EventOvwSupport/visualbasic/default.xaml.vb#groupbuttoncodebehind)]  
  
 **类处理：**路由事件允许使用由类定义的静态处理程序。  这个类处理程序能够抢在任何附加的实例处理程序之前来处理事件。  
  
 **引用事件，而不反射：**某些代码和标记技术需要能标识特定事件的方法。  路由事件创建 <xref:System.Windows.RoutedEvent> 字段作为标识符，以此提供不需要静态反射或运行时反射的可靠的事件标识技术。  
  
### 路由事件的实现方式  
 [路由事件](GTMT)是一个 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件，它由 <xref:System.Windows.RoutedEvent> 类的实例提供支持并向 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 事件系统注册。  从注册中获取的 <xref:System.Windows.RoutedEvent> 实例通常保留为某种类的 `public` `static` `readonly` 字段成员，该类进行了注册并因此“拥有”路由事件。  与同名 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件（有时称为“包装”事件）的连接是通过重写 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件的 `add` 和 `remove` 实现来完成的。  通常，`add` 和 `remove` 保留为隐式默认值，该默认值使用特定于语言的相应事件语法来添加和移除该事件的处理程序。  路由事件的支持和连接机制在概念上与以下机制相似：[依赖项属性](GTMT)是一个 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 属性，该属性由 <xref:System.Windows.DependencyProperty> 类提供支持并向 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统注册。  
  
 下面的示例演示自定义 `Tap` 路由事件的声明，其中包括注册和公开 <xref:System.Windows.RoutedEvent> 标识符字段以及对 `Tap` [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件进行 `add` 和 `remove` 实现。  
  
 [!code-csharp[RoutedEventCustom#AddRemoveHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventCustom/CSharp/SDKSampleLibrary/class1.cs#addremovehandler)]
 [!code-vb[RoutedEventCustom#AddRemoveHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventCustom/VB/SDKSampleLibrary/Class1.vb#addremovehandler)]  
  
### 路由事件处理程序和 XAML  
 若要使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 为某个事件添加处理程序，请将该事件的名称声明为用作事件侦听器的元素的特性。  该特性的值是所实现的处理程序方法的名称，该方法必须存在于代码隐藏文件的分部类中。  
  
 [!code-xml[EventOvwSupport#SimplestSyntax](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml#simplestsyntax)]  
  
 用来添加标准 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件处理程序的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 语法与用来添加路由事件处理程序的语法相同，因为您实际上是在向底层具有路由事件实现的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件包装中添加处理程序。  有关在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中添加事件处理程序的更多信息，请参见 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)。  
  
<a name="routing_strategies"></a>   
## 路由策略  
 路由事件使用以下三个路由策略之一：  
  
-   **冒泡：**针对事件源调用事件处理程序。  路由事件随后会路由到后续的父元素，直到到达元素树的根。  大多数路由事件都使用冒泡路由策略。  冒泡路由事件通常用来报告来自不同控件或其他 UI 元素的输入或状态变化。  
  
-   **直接：**只有源元素本身才有机会调用处理程序以进行响应。  这与 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]用于事件的“路由”相似。  但是，与标准 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件不同的是，直接路由事件支持类处理（类处理将在下一节中介绍）而且可以由 <xref:System.Windows.EventSetter> 和 <xref:System.Windows.EventTrigger> 使用。  
  
-   **隧道：**最初将在元素树的根处调用事件处理程序。  随后，路由事件将朝着路由事件的源节点元素（即引发路由事件的元素）方向，沿路由线路传播到后续的子元素。  在合成控件的过程中通常会使用或处理隧道路由事件，这样，就可以有意地禁止显示复合部件中的事件，或者将其替换为特定于整个控件的事件。  在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中提供的输入事件通常是以隧道\/冒泡对实现的。  隧道事件有时又称作 Preview 事件，这是由隧道\/冒泡对所使用的命名约定决定的。  
  
<a name="why_use"></a>   
## 为什么使用路由事件？  
 作为应用程序开发人员，您不需要始终了解或关注正在处理的事件是否作为路由事件实现。  路由事件具有特殊的行为，但是，如果您在引发该行为的元素上处理事件，则该行为通常会不可见。  
  
 如果您使用以下任一建议方案，路由事件的功能将得到充分发挥：在公用根处定义公用处理程序、合成自己的控件或者定义您自己的自定义控件类。  
  
 路由事件侦听器和路由事件源不必在其层次结构中共享公用事件。  任何 <xref:System.Windows.UIElement> 或 <xref:System.Windows.ContentElement> 可以是任一路由事件的事件侦听器。  因此，您可以使用在整个工作 [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 集内可用的全套路由事件作为概念“接口”，应用程序中的不同元素凭借这个接口来交换事件信息。  路由事件的这个“接口”概念特别适用于输入事件。  
  
 路由事件还可以用来通过元素树进行通信，因为事件的事件数据会永存到路由中的每个元素中。  一个元素可以更改事件数据中的某项内容，该更改将对于路由中的下一个元素可用。  
  
 之所以将任何给定的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 事件作为路由事件实现（而不是作为标准 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件实现），除了路由方面的原因，还有两个其他原因。  如果您要实现自己的事件，则可能也需要考虑这两个因素：  
  
-   某些 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 样式和模板功能（如 <xref:System.Windows.EventSetter> 和 <xref:System.Windows.EventTrigger>）要求被引用的事件是路由事件。  前面提到的事件标识符方案就是这样的。  
  
-   路由事件支持类处理机制，类可以凭借该机制来指定静态方法，这些静态方法能够在任何已注册的实例程序访问路由事件之前，处理这些路由事件。  这在控件设计中非常有用，因为您的类可以强制执行事件驱动的类行为，以防它们在处理实例上的事件时被意外禁止。  
  
 本主题将用单独的章节来讨论每个考虑因素。  
  
<a name="event_handing"></a>   
## 为路由事件添加和实现事件处理程序  
 若要在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中添加事件处理程序，只需将相应的事件名称作为一个特性添加到某个元素中，并将特性值设置为用来实现相应委托的事件处理程序的名称，如下面的示例中所示。  
  
 [!code-xml[EventOvwSupport#SimplestSyntax](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml#simplestsyntax)]  
  
 `b1SetColor` 是实现的处理程序的名称，该处理程序包含用来处理 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件的代码。  `b1SetColor` 必须具备与 <xref:System.Windows.RoutedEventHandler> 委托相同的签名，该委托是 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件的事件处理程序委托。  所有路由事件处理程序委托的第一个参数都指定要向其中添加事件处理程序的元素，第二个参数指定事件的数据。  
  
 [!code-csharp[EventOvwSupport#SimpleHandlerA](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml.cs#simplehandlera)]
 [!code-vb[EventOvwSupport#SimpleHandlerA](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/EventOvwSupport/visualbasic/default.xaml.vb#simplehandlera)]  
[!code-csharp[EventOvwSupport#SimpleHandlerB](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml.cs#simplehandlerb)]
[!code-vb[EventOvwSupport#SimpleHandlerB](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/EventOvwSupport/visualbasic/default.xaml.vb#simplehandlerb)]  
  
 <xref:System.Windows.RoutedEventHandler> 是基本的路由事件处理程序委托。  对于针对某些控件或方案而专门处理的路由事件，要用于路由事件处理程序的委托还可能会变得更加专用化，因此它们可以传输专用的事件数据。  例如，在常见的输入方案中，可以处理 <xref:System.Windows.UIElement.DragEnter> 路由事件。  您的处理程序应当实现 <xref:System.Windows.DragEventHandler> 委托。  借助更具体的委托，可以对处理程序中的 <xref:System.Windows.DragEventArgs> 进行处理，并读取 <xref:System.Windows.DragEventArgs.Data%2A> 属性，该属性中包含拖动操作的剪贴板内容。  
  
 有关如何使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 向元素中添加事件处理程序的完整示例，请参见[处理路由事件](../../../../docs/framework/wpf/advanced/how-to-handle-a-routed-event.md)。  
  
 在用代码创建的应用程序中为路由事件添加处理程序非常简单。  路由事件处理程序始终可以通过帮助器方法 <xref:System.Windows.UIElement.AddHandler%2A> 来添加，现有支持为 `add` 调用的也是此方法。但是，现有的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 路由事件通常借助于支持机制来实现 `add` 和 `remove` 逻辑，这些逻辑允许使用特定于语言的事件语法来添加路由事件的处理程序，特定于语言的事件语法比帮助器方法更直观。  下面是帮助器方法的示例用法：  
  
 [!code-csharp[EventOvwSupport#AddHandlerCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml.cs#addhandlercode)]
 [!code-vb[EventOvwSupport#AddHandlerCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/EventOvwSupport/visualbasic/default.xaml.vb#addhandlercode)]  
  
 下一个示例演示 [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] 运算符语法（[!INCLUDE[TLA2#tla_visualb](../../../../includes/tla2sharptla-visualb-md.md)] 的运算符语法稍有不同，因为它以不同的方法来处理取消引用）：  
  
 [!code-csharp[EventOvwSupport#AddHandlerPlusEquals](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml.cs#addhandlerplusequals)]
 [!code-vb[EventOvwSupport#AddHandlerPlusEquals](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/EventOvwSupport/visualbasic/default.xaml.vb#addhandlerplusequals)]  
  
 有关如何在代码中添加事件处理程序的示例，请参见[使用代码添加事件处理程序](../../../../docs/framework/wpf/advanced/how-to-add-an-event-handler-using-code.md)。  
  
 如果使用的是 [!INCLUDE[TLA2#tla_visualb](../../../../includes/tla2sharptla-visualb-md.md)]，则还可以使用 `Handles` 关键字，将处理程序作为处理程序声明的一部分来添加。  有关更多信息，请参见 [Visual Basic 和 WPF 事件处理](../../../../docs/framework/wpf/advanced/visual-basic-and-wpf-event-handling.md)。  
  
<a name="concept_handled"></a>   
### “已处理”概念  
 所有的路由事件都共享一个公共的事件数据基类 <xref:System.Windows.RoutedEventArgs>。  <xref:System.Windows.RoutedEventArgs> 定义了一个采用布尔值的 <xref:System.Windows.RoutedEventArgs.Handled%2A> 属性。  <xref:System.Windows.RoutedEventArgs.Handled%2A> 属性的目的在于，允许路由中的任何事件处理程序通过将 <xref:System.Windows.RoutedEventArgs.Handled%2A> 的值设置为 `true` 来将路由事件标记为“已处理”。  处理程序在路由路径上的某个元素处对共享事件数据进行处理之后，这些数据将再次报告给路由路径上的每个侦听器。  
  
 <xref:System.Windows.RoutedEventArgs.Handled%2A> 的值影响路由事件在沿路由线路向远处传播时的报告或处理方式。  在路由事件的事件数据中，如果 <xref:System.Windows.RoutedEventArgs.Handled%2A> 为 `true`，则通常不再为该特定事件实例调用负责在其他元素上侦听该路由事件的处理程序。  这条规则对以下两类处理程序均适用：在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中附加的处理程序；由语言特定的事件处理程序附加语法（如 `+=` 或 `Handles`）添加的处理程序。  对于最常见的处理程序方案，如果将 <xref:System.Windows.RoutedEventArgs.Handled%2A> 设置为 `true`，以此将事件标记为“已处理”，则将“停止”隧道路由或冒泡路由，同时，类处理程序在某个路由点处理的所有事件的路由也将“停止”。  
  
 但是，侦听器仍可以凭借“handledEventsToo”机制来运行处理程序，以便在事件数据中的 <xref:System.Windows.RoutedEventArgs.Handled%2A> 为 `true` 时响应路由事件。  换言之，将事件数据标记为“已处理”并不会真的停止事件路由。  您只能在代码或 <xref:System.Windows.EventSetter> 中使用 handledEventsToo 机制：  
  
-   在代码中，不使用适用于一般 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件的特定于语言的事件语法，而是通过调用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 方法 <xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> 来添加处理程序。  使用此方法时，请将 `handledEventsToo` 的值指定为 `true`。  
  
-   在 <xref:System.Windows.EventSetter> 中，请将 <xref:System.Windows.EventSetter.HandledEventsToo%2A> 特性设置为 `true`。  
  
 除了 <xref:System.Windows.RoutedEventArgs.Handled%2A> 状态在路由事件中生成的行为以外，<xref:System.Windows.RoutedEventArgs.Handled%2A> 概念还暗示您应当如何设计自己的应用程序和编写事件处理程序代码。  可以将 <xref:System.Windows.RoutedEventArgs.Handled%2A> 概念化为由路由事件公开的简单协议。  此协议的具体使用方法由您来决定，但是需要按照如下方式来对 <xref:System.Windows.RoutedEventArgs.Handled%2A> 值的预期使用方式进行概念设计：  
  
-   如果路由事件标记为“已处理”，则它不必由该路由中的其他元素再次处理。  
  
-   如果路由事件未标记为“已处理”，则说明该路由中前面的其他侦听器已经选择了不注册处理程序，或者已经注册的处理程序选择不操作事件数据并将 <xref:System.Windows.RoutedEventArgs.Handled%2A> 设置为 `true`。  （或者，当前的侦听器很可能就是路由中的第一个点。）当前侦听器上的处理程序现在有三个可能的操作方案：  
  
    -   不执行任何操作；该事件保持未处理状态，该事件将路由到下一个侦听器。  
  
    -   执行代码以响应该事件，但是所执行的操作被视为不足以保证将事件标记为“已处理”。  该事件将路由到下一个侦听器。  
  
    -   执行代码以响应该事件。  在传递到处理程序的事件数据中将该事件标记为“已处理”，因为所执行的操作被视为不足以保证将该事件标记为“已处理”。  该事件仍将路由到下一个侦听器，但是，由于其事件数据中存在 <xref:System.Windows.RoutedEventArgs.Handled%2A>\=`true`，因此只有 `handledEventsToo` 侦听器才有机会调用进一步的处理程序。  
  
 这个概念设计是通过前面提到的路由行为来加强的：即使路由中前面的处理程序已经将 <xref:System.Windows.RoutedEventArgs.Handled%2A> 设置为 `true`，也会增加为所调用的路由事件附加处理程序的难度（尽管仍可以在代码或样式中实现这一目的）。  
  
 有关 <xref:System.Windows.RoutedEventArgs.Handled%2A>、路由事件的类处理的更多信息，以及针对何时适合将路由事件标记为 <xref:System.Windows.RoutedEventArgs.Handled%2A> 的建议，请参见[将路由事件标记为“已处理”和“类处理”](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md)。  
  
 在应用程序中，相当常见的做法是只针对引发冒泡路由事件的对象来处理该事件，而根本不考虑事件的路由特征。  但是，在事件数据中将路由事件标记为“已处理”仍是一个不错的做法，因为这样可以防止元素树中位置更高的元素也对同一个路由事件附加了处理程序而出现意外的副作用。  
  
<a name="class_handlers"></a>   
## 类处理程序  
 如果您定义的类是以某种方式从 <xref:System.Windows.DependencyObject> 派生的，那么对于作为类的已声明或已继承事件成员的路由事件，还可以定义和附加一个类处理程序。  每当路由事件到达其路由中的元素实例时，都会先调用类处理程序，然后再调用附加到该类某个实例的任何实例侦听器处理程序。  
  
 有些 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件对某些路由事件具有固有的类处理。  路由事件可能看起来从未引发过，但实际上正对其进行类处理，如果您使用某些技术的话，路由事件还是可能由实例处理程序进行处理。  同样，许多基类和控件都公开可用来重写类处理行为的虚方法。  有关如何解决不需要的类处理以及如何在自定义类中定义自己的类处理的更多信息，请参见[将路由事件标记为“已处理”和“类处理”](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md)。  
  
<a name="attached_events"></a>   
## WPF 中的附加事件  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 语言还定义了一个名为“附加事件”的特殊类型的事件。  使用附加事件，可以将特定事件的处理程序添加到任意元素中。  处理事件的元素不必定义或继承附加事件，可能引发事件的对象和用来处理实例的目标也都不必将该事件定义为类成员或将其作为类成员来“拥有”。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 输入系统大量地使用附加事件。  但是，几乎所有的附加事件都是通过基本元素转发的。  输入事件随后会显示为等效的、作为基本元素类成员的非附加路由事件。  例如，通过针对该 <xref:System.Windows.UIElement> 使用 <xref:System.Windows.UIElement.MouseDown>（而不是在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 或代码中处理附加事件语法），可以针对任何给定的 <xref:System.Windows.UIElement>，更方便地处理基础附加事件 <xref:System.Windows.Input.Mouse.MouseDown?displayProperty=fullName>。  
  
 有关 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中附加事件的更多信息，请参见[附加事件概述](../../../../docs/framework/wpf/advanced/attached-events-overview.md)。  
  
<a name="Qualifying_Event_Names_in_XAML_for_Anticipated_Routing"></a>   
## XAML 中的限定事件名称  
 为子元素所引发的路由事件附加处理程序是另一个语法用法，它与*类型名称*.*事件名称* 附加事件语法相似，但它并非严格意义上的附加事件用法。  可以向公用父级附加处理程序以利用事件路由，即使公用父级可能不将相关的路由事件作为其成员也是如此。  请再次考虑下面的示例：  
  
 [!code-xml[EventOvwSupport#GroupButton](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/default.xaml#groupbutton)]  
  
 在这里，在其中添加处理程序的父元素侦听器是 <xref:System.Windows.Controls.StackPanel>。  但是，它正在为已经声明而且将由 <xref:System.Windows.Controls.Button> 类（实际上是 <xref:System.Windows.Controls.Primitives.ButtonBase>，但是可以由 <xref:System.Windows.Controls.Button> 通过继承来使用）引发的路由事件添加处理程序。  <xref:System.Windows.Controls.Button>“拥有”该事件，但是路由事件系统允许将任何路由事件的处理程序附加到任何 <xref:System.Windows.UIElement> 或 <xref:System.Windows.ContentElement> 实例侦听器，该侦听器可能会以其他方式为[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 事件附加侦听器。  对于这些限定的事件特性名来说，默认的 xmlns 命名空间通常是默认的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] xmlns 命名空间，但是您还可以为自定义路由事件指定带有前缀的命名空间。  有关 xmlns 的更多信息，请参见 [WPF XAML 的 XAML 命名空间和命名空间映射](../../../../docs/framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)。  
  
<a name="how_event_processing_works"></a>   
## WPF 输入事件  
 路由事件在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 平台中的常见用法之一是用于事件输入。在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，按照约定，隧道路由事件的名称以单词“Preview”开头。  输入事件通常成对出现，一个是冒泡事件，另一个是隧道事件。  例如，<xref:System.Windows.ContentElement.KeyDown> 事件和 <xref:System.Windows.ContentElement.PreviewKeyDown> 事件具有相同的签名，前者是冒泡输入事件，后者是隧道输入事件。  偶尔，输入事件只有冒泡版本，或者有可能只有直接路由版本。  在本文档中，当存在具有替换路由策略的类似路由事件时，路由事件主题交叉引用它们，而且托管引用页面中的各个节阐释每个路由事件的路由策略。  
  
 实现成对出现的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 输入事件的目的在于，使来自输入的单个用户操作（如按鼠标按钮）按顺序引发该对中的两个路由事件。  首先引发隧道事件并沿路由传播，  然后引发冒泡事件并沿其路由传播。  顾名思义，这两个事件会共享同一个事件数据实例，因为用来引发冒泡事件的实现类中的 <xref:System.Windows.UIElement.RaiseEvent%2A> 方法调用会侦听隧道事件中的事件数据，并在新引发的事件中重用它。  具有隧道事件处理程序的侦听器首先获得将路由事件标记为“已处理”的机会（首先是类处理程序，然后是实例处理程序）。  如果隧道路由中的某个元素将路由事件标记为“已处理”，则会针对冒泡事件发送已经处理的事件数据，而且将不调用为等效的冒泡输入事件附加的典型处理程序。  已处理的冒泡事件看起来好像尚未引发过。  此处理行为对于控件合成非常有用，因为此时您可能希望所有基于命中测试的输入事件或者所有基于焦点的输入事件都由最终的控件（而不是它的复合部件）报告。  作为可支持控件类的代码的一部分，最后一个控件元素靠近合成链中的根，因此将有机会首先对隧道事件进行类处理，或许还有机会将该路由事件“替换”为更特定于控件的事件。  
  
 为了说明输入事件处理的工作方式，请考虑下面的输入事件示例。  在下面的树插图中，`leaf element #2` 是先后发生的 `PreviewMouseDown` 事件和 `MouseDown` 事件的源。  
  
 ![事件路由示意图](../../../../docs/framework/wpf/advanced/media/wcsdkcoreinputevents.png "wcsdkCoreInputEvents")  
输入事件的冒泡和隧道  
  
 事件的处理顺序如下所示：  
  
1.  针对根元素处理 `PreviewMouseDown`（隧道）。  
  
2.  针对中间元素 1 处理 `PreviewMouseDown`（隧道）。  
  
3.  针对源元素 2 处理 `PreviewMouseDown`（隧道）。  
  
4.  针对源元素 2 处理 `MouseDown`（冒泡）。  
  
5.  针对中间元素 1 处理 `MouseDown`（冒泡）。  
  
6.  针对根元素处理 `MouseDown`（冒泡）。  
  
 路由事件处理程序委托提供对以下两个对象的引用：引发该事件的对象以及在其中调用处理程序的对象。  在其中调用处理程序的对象是由 `sender` 参数报告的对象。  首先在其中引发事件的对象是由事件数据中的 <xref:System.Windows.RoutedEventArgs.Source%2A> 属性报告的。  路由事件仍可以由同一个对象引发和处理，在这种情况下，`sender` 和 <xref:System.Windows.RoutedEventArgs.Source%2A> 是相同的（事件处理示例列表中的步骤 3 和 4 就是这样的情况）。  
  
 由于存在隧道和冒泡，因此父元素接收 <xref:System.Windows.RoutedEventArgs.Source%2A> 作为其子元素之一的输入事件。  当有必要知道源元素是哪个元素时，可以通过访问 <xref:System.Windows.RoutedEventArgs.Source%2A> 属性来标识源元素。  
  
 通常，一旦将输入事件标记为 <xref:System.Windows.RoutedEventArgs.Handled%2A>，就将不进一步调用处理程序。  通常，一旦调用了用来对输入事件的含义进行特定于应用程序的逻辑处理的处理程序，就应当将输入事件标记为“已处理”。  
  
 对于这个有关 <xref:System.Windows.RoutedEventArgs.Handled%2A> 状态的通用声明有一个例外，那就是，注册为有意忽略事件数据 <xref:System.Windows.RoutedEventArgs.Handled%2A> 状态的输入事件处理程序仍将在其路由中被调用。  有关更多信息，请参见 [预览事件](../../../../docs/framework/wpf/advanced/preview-events.md)或[将路由事件标记为“已处理”和“类处理”](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md)。  
  
 通常，隧道事件和冒泡事件之间的共享事件数据模型以及先引发隧道事件后引发冒泡事件等概念并非对于所有的路由事件都适用。  该行为的实现取决于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 输入设备选择引发和连接输入事件对的具体方式。  实现自己的输入事件是一个高级方案，但是您也可以选择针对自己的输入事件遵循该模型。  
  
 一些类选择对某些输入事件进行类处理，其目的通常是重新定义用户驱动的特定输入事件在该控件中的含义并引发新事件。  有关更多信息，请参见[将路由事件标记为“已处理”和“类处理”](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md)。  
  
 有关输入以及在典型的应用程序方案中输入和事件如何交互的更多信息，请参见[输入概述](../../../../docs/framework/wpf/advanced/input-overview.md)。  
  
<a name="events_styles"></a>   
## EventSetter 和 EventTrigger  
 在样式中，可以通过使用 <xref:System.Windows.EventSetter> 在标记中包括某个预先声明的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 事件处理语法。  在应用样式时，所引用的处理程序会添加到带样式的实例中。  只能针对路由事件声明 <xref:System.Windows.EventSetter>。  下面是一个示例。  请注意，此处引用的 `b1SetColor` 方法位于代码隐藏文件中。  
  
 [!code-xml[EventOvwSupport#XAML2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/EventOvwSupport/CSharp/page2.xaml#xaml2)]  
  
 这样做的好处在于，样式有可能包含大量可应用于应用程序中任何按钮的其他信息，让 <xref:System.Windows.EventSetter> 成为该样式的一部分甚至可以提高代码在标记级别的重用率。  而且，<xref:System.Windows.EventSetter> 还进一步从通用的应用程序和页面标记中提取处理程序方法的名称。  
  
 另一个将 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的路由事件和动画功能结合在一起的专用语法是 <xref:System.Windows.EventTrigger>。  与 <xref:System.Windows.EventSetter> 一样，只有路由事件可以用于 <xref:System.Windows.EventTrigger>。通常将 <xref:System.Windows.EventTrigger> 声明为样式的一部分，但是还可以在页面级元素上将 <xref:System.Windows.EventTrigger> 声明为 <xref:System.Windows.FrameworkElement.Triggers%2A> 集合的一部分或者在 <xref:System.Windows.Controls.ControlTemplate> 中对其进行声明。使用 <xref:System.Windows.EventTrigger>，可以指定当路由事件到达其路由中的某个元素（这个元素针对该事件声明了 <xref:System.Windows.EventTrigger>）时将运行 <xref:System.Windows.Media.Animation.Storyboard>。  与只是处理事件并且会导致它启动现有演示图板相比，<xref:System.Windows.EventTrigger> 的好处在于，<xref:System.Windows.EventTrigger> 对演示图板及其运行时行为提供更好的控制。有关更多信息，请参见[在演示图板启动之后使用事件触发器来控制演示图板](../../../../docs/framework/wpf/graphics-multimedia/how-to-use-event-triggers-to-control-a-storyboard-after-it-starts.md)。  
  
<a name="more_about"></a>   
## 有关路由事件的更多信息  
 本主题主要从以下角度讨论路由事件：描述基本概念；就如何以及何时响应各种基元素和基控件中已经存在的路由事件提供指南。  但是，您可以为自定义类创建自己的路由事件，还可以创建所有必要的支持（如专用的事件数据类和委托）。  路由事件的所有者可以是任何类，但是路由事件只有在由 <xref:System.Windows.UIElement> 或 <xref:System.Windows.ContentElement> 派生类引发和处理之后才有用。  有关自定义事件的更多信息，请参见[创建自定义路由事件](../../../../docs/framework/wpf/advanced/how-to-create-a-custom-routed-event.md)。  
  
## 请参阅  
 <xref:System.Windows.EventManager>   
 <xref:System.Windows.RoutedEvent>   
 <xref:System.Windows.RoutedEventArgs>   
 [将路由事件标记为“已处理”和“类处理”](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md)   
 [输入概述](../../../../docs/framework/wpf/advanced/input-overview.md)   
 [命令概述](../../../../docs/framework/wpf/advanced/commanding-overview.md)   
 [自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [WPF 中的树](../../../../docs/framework/wpf/advanced/trees-in-wpf.md)   
 [弱事件模式](../../../../docs/framework/wpf/advanced/weak-event-patterns.md)