---
title: "将路由事件标记为“已处理”和“类处理” | Microsoft Docs"
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
  - "冒泡事件"
  - "类侦听器"
  - "复合控件"
  - "控件, 复合"
  - "事件, Bubbling — 冒泡"
  - "事件, 取消显示"
  - "事件, Tunneling — 隧道"
  - "实例侦听器"
  - "侦听器"
  - "预览路由事件"
  - "路由事件, 标记为已处理"
  - "路由事件, 预览"
  - "取消显示事件"
  - "隧道事件"
ms.assetid: 5e745508-4861-4b48-b5f6-5fc7ce5289d2
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 将路由事件标记为“已处理”和“类处理”
路由事件的处理程序可以在事件数据内将事件标记为已处理。  处理事件将有效地缩短路由。  类处理是一个编程概念，受路由事件支持。  类处理程序有机会在类级别使用处理程序处理特定路由事件，该处理程序在类的任何实例上的任何实例处理程序之前调用。  
  
   
  
<a name="prerequisites"></a>   
## 必备组件  
 本主题是以[路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)中介绍的概念为基础进行阐述的。  
  
<a name="When_to_Mark_Events_as_Handled"></a>   
## 何时将事件标记为已处理  
 当您在路由事件的事件数据中将 <xref:System.Windows.RoutedEventArgs.Handled%2A> 属性值设置为 `true` 时，这称为“将事件标记为已处理”。  对于应用程序创作者或者响应现有路由事件或实现新路由事件的控件创建者而言，何时应将路由事件标记为已处理，没有一定之规。  大多数情形下，路由事件的事件数据中携带的“已处理”信息应当用作一种限定协议，用以限定您自己的应用程序对于在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 中公开的各个路由事件以及任意自定义路由事件的响应。  另一个要考虑“已处理”问题的情形是，如果您的代码以重要且相对完整的方式响应路由事件，则您通常应将路由事件标记为已处理。通常，不应该有一个以上的重要响应。所谓重要响应，是指对于发生的任意单个路由事件，都需要单独的处理程序实现。  如果需要多个响应，则应通过在单个处理程序内链接的应用程序逻辑实现必要的代码，而不是使用路由事件系统进行转发。  “重要”这一概念指的是什么，也是仁者见仁的问题，具体取决于您的应用程序或代码。  作为一般性指导原则，一些“重要响应”示例包括：设置焦点、修改公共状态、设置影响可视表示的属性以及引发其他新事件。  非重要响应的示例包括：修改私有状态（无可视影响，或编程表示形式）、记录事件或查看事件参数并选择不响应该事件。  
  
 路由事件系统行为在使用路由事件的已处理状态方面增强了此“重要响应”模型，因为不会调用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中添加的处理程序或 <xref:System.Windows.UIElement.AddHandler%2A> 的公用签名，以响应事件数据已标记为已处理的路由事件。  您必须额外添加带 `handledEventsToo` 参数版本的处理程序 \(<xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29>\)，才能处理由事件路由中的早期参与者标记为已处理的路由事件。  
  
 在某些情况下，控件本身会将某些路由事件标记为已处理。  已处理的路由事件表示 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件作者做出的以下决定：响应路由事件的控件操作是重要的，或者作为控件实现的一部分已完成，事件无需进一步处理。  通常，通过为事件添加一个类处理程序，或重写存在于基类上的虚拟类处理程序之一，可以完成此操作。  必要时您仍然可以应对此事件处理，请参见本主题后面部分的[通过控件解决事件禁止问题](#WorkingAroundEventSuppressionByControls)。  
  
<a name="Preview_Events_vs__Bubbling_Events_and_Handling"></a>   
## “预览”（隧道）事件与冒泡事件的对比以及事件处理  
 预览路由事件是指遵循元素树的[隧道](GTMT)路由的事件。  命名约定中的“Preview”是指输入事件的一般原则，即预览（隧道）路由事件是在对等的冒泡路由事件之前引发的。  另外，具有隧道和冒泡对的输入路由事件具有截然不同的处理逻辑。  如果隧道\/预览路由事件标记为已由事件侦听器处理，则冒泡路由事件将标记为已处理，这甚至可能发生在冒泡路由事件的任何侦听器接收到该事件之前。  隧道路由事件和冒泡路由事件在技术层面上是单独的事件，但是它们有意共享相同的事件数据实例以实现此行为。  
  
 隧道路由事件与冒泡路由事件之间的连接是由给定的任意 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 类引发自己的已声明路由事件的方式的内部实现来完成的，对于成对的输入路由事件也是如此。  但是除非这一类级实现存在，否则共享命名方案的隧道路由事件与冒泡路由事件之间将没有连接：没有上述实现，它们将是两个完全独立的路由事件，不会顺次引发，也不会共享事件数据。  
  
 有关如何在自定义类中实现隧道\/冒泡输入路由事件对的更多信息，请参见[创建自定义路由事件](../../../../docs/framework/wpf/advanced/how-to-create-a-custom-routed-event.md)。  
  
<a name="Class_Handlers_and_Instance_Handlers"></a>   
## 类处理程序和实例处理程序  
 路由事件会考虑事件的两种不同类型的侦听器，即类侦听器和实例侦听器。  由于类型已在其静态构造函数中调用特定的 <xref:System.Windows.EventManager> [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)]，即 <xref:System.Windows.EventManager.RegisterClassHandler%2A>，或者已从元素基类重写类处理程序虚方法，因此类侦听器存在。  在已通过调用 <xref:System.Windows.UIElement.AddHandler%2A> 为该路由事件附加了一个或多个处理程序的情况下，实例侦听器是特定的类实例\/元素。作为事件的[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 事件包装 add{} 和 remove{} 实现的一部分，现有的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 路由事件会对 <xref:System.Windows.UIElement.AddHandler%2A> 进行调用，这也是通过特性语法附加事件处理程序的简单 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 机制的启用方式。  因此，即使简单的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 用法最终也等同于 <xref:System.Windows.UIElement.AddHandler%2A> 调用。  
  
 会检查可视化树内的元素是否有注册的处理程序实现。  可能会在整个路由过程中以该路由事件的路由策略类型所固有的顺序调用处理程序。  例如，冒泡路由事件将首先调用那些附加到引发该路由事件的同一元素的处理程序。  然后，路由事件“冒泡”到下一父元素，以此类推，直到到达应用程序根元素。  
  
 从冒泡路由中的根元素的角度而言，如果类处理或者更靠近路由事件源的任意元素调用那些将事件参数标记为正在处理的处理程序，那么就不会调用根元素上的处理程序，这样在到达该根元素之前事件路由会有效缩短。  不过，路由并未完全停止，因为可以使用仍应调用处理程序的特殊条件来添加处理程序，即使类处理程序或实例处理程序已将路由事件标记为已处理也是如此。  本主题后面部分的[添加即使在事件标记为已处理时仍引发的实例处理程序](#AddingInstanceHandlersthatAreRaisedEvenWhenEventsareMarkedHandled)对此进行了说明。  
  
 在比事件路由更深的级别上，还可能存在作用于类的任意给定实例上的多个类处理程序。  这是因为，路由事件的类处理模型使得类层次结构中的所有可能的类都可以针对每个路由事件注册自己的类处理程序。  每个类处理程序都会添加到一个内部存储，并且当构造应用程序的事件路由时，所有类处理程序都会添加到该事件路由中。  类处理程序是以这样的顺序添加到路由中的：最先调用派生程度最高的类处理程序，然后调用每个后续基类的类处理程序。  通常，不会注册类处理程序以便它们也响应已标记为已处理的路由事件。  因此，此类处理机制可提供以下两个选项之一：  
  
-   派生类可以通过添加一个不将路由事件标记为已处理的处理程序，来补充从基类继承的类处理，因为有时会在派生类处理程序之后调用基类处理程序。  
  
-   派生类可以通过添加一个将路由事件标记为已处理的类处理程序，来替换从基类继承的类处理。  应慎用此方法，因为它可能会更改诸如可视外观、状态逻辑、输入处理和命令处理等方面的基控件设计意图。  
  
<a name="Class_Handling_of_Routed_Events"></a>   
## 按控件基类进行的路由事件类处理  
 在事件路由中的每个给定元素节点上，类侦听器都有机会在元素的任意实例侦听器之前响应路由事件。  为此，类处理程序有时用于禁止某个特定控件类实现不希望继续传播的路由事件，或者用于提供该路由事件的特殊处理并将此作为类的一项功能。  例如，类可能引发它自己的类特定事件，其中包含有关某个用户输入条件在该特定类的上下文中所代表的意义的更多具体信息。  然后，此类实现可能会将较为常规的路由事件标记为已处理。  通常，会以相应的方法添加类处理程序，使其不针对共享事件数据已标记为已处理的路由事件调用，但是对于非典型情况，还存在一个 <xref:System.Windows.EventManager.RegisterClassHandler%28System.Type%2CSystem.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> 签名，用于将类处理程序注册为即使路由事件标记为已处理时也仍调用。  
  
### 类处理程序虚方法  
 某些元素（特别是诸如 <xref:System.Windows.UIElement> 这样的基元素）会公开与其公共路由事件列表对应的空的“On\*Event”和“OnPreview\*Event”虚方法。  可以重写这些虚方法以便为该路由事件实现类处理程序。  如前所述，基元素类会使用 <xref:System.Windows.EventManager.RegisterClassHandler%28System.Type%2CSystem.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> 将上述虚方法注册为每个此类路由事件的类处理程序。  因为无需在静态构造函数中针对每个类型进行特殊初始化，所以 On\*Event 虚方法使得为相关路由事件实现类处理变得简单得多。  例如，通过重写 <xref:System.Windows.UIElement.OnDragEnter%2A> 虚方法，您可以在任意 <xref:System.Windows.UIElement> 派生类中为 <xref:System.Windows.UIElement.DragEnter> 事件添加类处理。  在重写代码内，您可以处理路由事件、引发其他事件、启动可能更改实例的元素属性的类特定逻辑或上述操作的任意组合。  通常情况下，在此类重写代码中，即使您将事件标记为已处理，也应调用基实现。  强烈建议调用基实现，因为虚方法是在基类上。  从每个虚方法调用基实现的标准受保护虚拟模式实质上会替换路由事件类处理所固有的机制并与之并行，因此可以在任意给定实例上调用类层次结构中所有类的类处理程序，并从派生程度最高的类的处理程序开始，一直继续到基类处理程序。  如果您的类明确要求更改基类处理逻辑，则您应仅忽略基实现调用。  在重写代码之前还是之后调用基实现取决于您的实现的性质。  
  
#### 输入事件类处理  
 类处理程序虚方法均以相应的方式注册，使得只有在有任意共享事件数据尚未标记为已处理的情况下才调用它们。  另外，仅仅对于输入事件而言，隧道和冒泡版本通常是顺次引发的，并且共享事件数据。  这必然使得对于一对给定的输入事件类处理程序（其中一个是隧道版本，另一个是冒泡版本），您可能不希望立即将事件标记为已处理。  如果您实现隧道类处理虚方法以便将事件标记为已处理，那么这样将会阻止调用冒泡类处理程序（并阻止调用隧道或冒泡事件的任意正常注册的实例处理程序）。  
  
 节点上的类处理一经完成，就会考虑实例侦听器。  
  
<a name="AddingInstanceHandlersthatAreRaisedEvenWhenEventsareMarkedHandled"></a>   
## 添加即使在事件标记为已处理时仍引发的实例处理程序  
 <xref:System.Windows.UIElement.AddHandler%2A> 方法提供一个特定重载，允许您添加只要事件到达路由中的处理元素，就会由事件系统调用的处理程序（即使另外某个处理程序已调整事件数据，将该事件标记为已处理）。  通常情况下不会这样做。  通常情况下，不论事件是在元素树中的什么位置处理（即使需要多个最终结果），都可以编写处理程序来调整可能受事件影响的应用程序代码的所有方面。  另外，通常情况下，需要响应该事件的实际只有一个元素，并且已发生了适当的应用程序逻辑。  不过，对于元素树中另外某个元素或控件复合已经将事件标记为已处理，但其他元素（位于元素树中或高或低的位置，具体取决于路由）仍希望调用自己的处理程序这种例外情况，`handledEventsToo` 重载可用。  
  
#### 何时将已处理事件标记为未处理  
 通常，标记为已处理的路由事件不应再标记为未处理（将 <xref:System.Windows.RoutedEventArgs.Handled%2A> 重设回 `false`），即便作用于 `handledEventsToo` 的处理程序也不应这样做。  不过，某些输入事件具有高级别和低级别两种事件表示形式，当在树中的一个位置看到高级别事件，在另一个位置看到低级别事件时，这两种表示形式可以重叠。  例如，假设这样一种情况：一个子元素侦听高级别键事件（如 <xref:System.Windows.UIElement.TextInput>），而父事件侦听低级别事件（如 <xref:System.Windows.UIElement.KeyDown>）。  如果父元素处理低级别事件，则高级别事件甚至可能在子元素中被禁止，尽管直观看来子元素应该具有处理事件的先机。  
  
 在上述情形下，可能需要针对低级别事件既向父元素中添加处理程序，也向子元素中添加处理程序。  子元素处理程序实现可以将低级别事件标记为已处理，但父元素处理程序实现会再次将其设置为未处理，这样树的向上方向上的更多元素（以及高级别事件）就可以有机会响应。  这种情形应该非常少见。  
  
<a name="Deliberately_Suppressing_Input_Events_for_Control"></a>   
## 有意对控件复合禁止输入事件  
 路由事件的类处理主要是用于输入事件和复合控件。  按照定义，复合控件是由多个实际控件或控件基类组成的。  控件作者通常希望合并每个子组件可能引发的所有可能的输入事件，以便将整个控件报告为单事件源。  某些情况下，控件作者可能希望完全禁止来自组件的事件，或者替换上携带更多信息或者指示更具体的行为的组件定义事件。  任意组件作者都可直接看到的规范化示例是 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] <xref:System.Windows.Controls.Button> 如何处理任意鼠标事件（最终会解析为所有按钮都有的一个直观事件，即 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件）。  
  
 <xref:System.Windows.Controls.Button> 基类 \(<xref:System.Windows.Controls.Primitives.ButtonBase>\) 是从 <xref:System.Windows.Controls.Control> 派生，而后者又是从 <xref:System.Windows.FrameworkElement> 和 <xref:System.Windows.UIElement> 派生的，控件输入处理所需的大部分事件基础结构都在 <xref:System.Windows.UIElement> 级别可用。  具体而言，<xref:System.Windows.UIElement> 会处理常规 <xref:System.Windows.Input.Mouse> 事件（为在其边界范围内的鼠标光标处理命中测试），并为最常见的按钮操作（如 <xref:System.Windows.UIElement.MouseLeftButtonDown>）提供截然不同的事件。  <xref:System.Windows.UIElement> 还将一个空的虚拟 <xref:System.Windows.UIElement.OnMouseLeftButtonDown%2A> 作为 <xref:System.Windows.UIElement.MouseLeftButtonDown> 的预注册类处理程序提供，并且 <xref:System.Windows.Controls.Primitives.ButtonBase> 会对它进行重写。  与此类似，<xref:System.Windows.Controls.Primitives.ButtonBase> 对 <xref:System.Windows.UIElement.MouseLeftButtonUp> 也使用类处理程序。  在获得传递的事件数据的重写代码中，实现通过将 <xref:System.Windows.RoutedEventArgs.Handled%2A> 设置为 `true` 来将该 <xref:System.Windows.RoutedEventArgs> 实例标记为已处理，并且同样的事件数据会继续沿路由的其余部分传递到其他类处理程序，以及实例处理程序或事件 setter。  另外，<xref:System.Windows.Controls.Primitives.ButtonBase.OnMouseLeftButtonUp%2A> 重写接下来会引发 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件。  大多数侦听器的最终结果是 <xref:System.Windows.UIElement.MouseLeftButtonDown> 和 <xref:System.Windows.UIElement.MouseLeftButtonUp> 事件“消失”，而转而由 <xref:System.Windows.Controls.Primitives.ButtonBase.Click>（保存更多意义的事件）取代，因为已知此事件是从真正的按钮发出，而不是从按钮的某个复合部分或从其他某个元素整体发出的。  
  
<a name="WorkingAroundEventSuppressionByControls"></a>   
### 通过控件解决事件禁止问题  
 有时，各个控件内的此事件禁止行为可能会干扰应用程序的事件处理逻辑的某些较为常规的意图。  例如，如果因某个原因，应用程序有一个位于应用程序根元素的 <xref:System.Windows.UIElement.MouseLeftButtonDown> 的处理程序，则您可能会注意到在按钮上任意单击鼠标都不会在根级别调用 <xref:System.Windows.UIElement.MouseLeftButtonDown> 或 <xref:System.Windows.UIElement.MouseLeftButtonUp> 处理程序。  事件本身实际上会向上冒泡（同样，事件路由未真正结束，但路由事件系统会在事件标记为已处理后更改其处理程序调用行为）。  当路由事件到达按钮时，<xref:System.Windows.Controls.Primitives.ButtonBase> 类处理会将 <xref:System.Windows.UIElement.MouseLeftButtonDown> 标记为已处理，因为它希望替换上具有更多意义的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件。  因此，不会调用将继续向上路由的任何标准 <xref:System.Windows.UIElement.MouseLeftButtonDown> 处理程序。  您可以使用两种方法来确保处理程序在此情形下会被调用。  
  
 第一种方法是使用 <xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> 的 `handledEventsToo` 签名有意添加处理程序。  这种方法的限制是用于附加事件处理程序的这种技术只可能来自代码，而不能来自标记。  通过[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 将事件处理程序名称指定为事件特性值的简单语法不能实现此行为。  
  
 第二种技术仅适用于输入事件，其中路由事件的隧道版本和冒泡版本是配对的。  对于这些路由事件，您可以转而将处理程序添加到预览\/[隧道](GTMT)对等路由事件。  该路由事件将从根开始在路由中传递，所以按钮类处理代码不会截获到它，前提是在应用程序的元素树中的某个上级元素级别附加了 Preview 处理程序。  如果您使用此方法，则将任意 Preview 事件标记为已处理时一定要谨慎。  以在根元素处理的 <xref:System.Windows.UIElement.PreviewMouseLeftButtonDown> 为例，如果您在处理程序实现中将此事件标记为 <xref:System.Windows.RoutedEventArgs.Handled%2A>，则实际上会禁止 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件。  这通常不是希望的行为。  
  
## 请参阅  
 <xref:System.Windows.EventManager>   
 [预览事件](../../../../docs/framework/wpf/advanced/preview-events.md)   
 [创建自定义路由事件](../../../../docs/framework/wpf/advanced/how-to-create-a-custom-routed-event.md)   
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)