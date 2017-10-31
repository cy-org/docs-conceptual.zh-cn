---
title: "属性更改事件 | Microsoft Docs"
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
  - "更改事件 [WPF], 属性"
  - "创建属性触发器 [WPF]"
  - "依赖项属性 [WPF], 更改事件"
  - "事件 [WPF], 属性值更改"
  - "标识更改的属性事件 [WPF]"
  - "属性更改事件 [WPF]"
  - "属性更改事件 [WPF], 类型"
  - "属性触发器 [WPF]"
  - "属性触发器 [WPF], 定义"
  - "属性值更改 [WPF]"
ms.assetid: 0a7989df-9674-4cc1-bc50-5d8ef5d9c055
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 属性更改事件
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 定义几个为响应属性值的更改而引发的事件。  属性通常是一个[依赖项属性](GTMT)。  事件本身有时是一个[路由事件](GTMT)，有时是一个标准的[!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 事件。  事件的定义因具体情况的不同而不同，因为有些属性更改更适于在元素树中路由，而其他属性更改则通常只关系到属性发生更改的对象。  
  
## 标识属性更改事件  
 不是所有报告属性更改的事件都显式地通过签名模式或命名模式来标识为属性更改事件。  通常，[!INCLUDE[TLA#tla_sdk](../../../../includes/tlasharptla-sdk-md.md)] 文档中的事件描述会指出事件是否直接与属性值更改关联，并提供属性与事件之间的交叉引用。  
  
### RoutedPropertyChanged 事件  
 某些事件使用显式用于属性更改事件的事件数据类型和委托。  该事件数据类型是 <xref:System.Windows.RoutedPropertyChangedEventArgs%601>，委托是 <xref:System.Windows.RoutedPropertyChangedEventHandler%601>。  事件数据和委托都具有用于在您定义处理程序时指定更改属性的实际类型的泛型参数。  事件数据包含两个属性，即 <xref:System.Windows.RoutedPropertyChangedEventArgs%601.OldValue%2A> 和 <xref:System.Windows.RoutedPropertyChangedEventArgs%601.NewValue%2A>，之后它们均作为事件数据中的类型参数传递。  
  
 名称中的“Routed”部分表示属性更改事件注册为一个路由事件。  路由属性更改事件的好处是，如果子元素（控件的组成部分）的属性值更改，控件的顶级也可以接收到属性更改事件。  例如，您可能创建一个合并 <xref:System.Windows.Controls.Primitives.RangeBase> 控件（如 <xref:System.Windows.Controls.Slider>）的控件。  如果滑块部分的 <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> 属性值更改，则您可能需要在父控件（而不是在该部分）处理此更改。  
  
 因为您有一个旧值和一个新值，所以很可能使用此事件处理程序作为属性值的验证程序。  但是，这不是大多数属性更改事件的设计意图。  通常，提供这些值是为了使您可以在代码的其他逻辑领域处理这些值，但是，在事件处理程序内部更改值实际上是并不可取的，并且可能导致意外的递归，具体取决于处理程序的实现方式。  
  
 如果属性是一个自定义依赖项属性，或者您处理的是定义了实例化代码的派生类，则存在一种更好的机制来跟踪属性更改，并且此机制是内置于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统中的，即：属性系统回调 <xref:System.Windows.CoerceValueCallback> 和 <xref:System.Windows.PropertyChangedCallback>。  有关如何使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性系统来进行验证和强制的更多详细信息，请参见[依赖项属性回调和验证](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md)和[自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)。  
  
### DependencyPropertyChanged 事件  
 属于属性更改事件方案一部分的另一对类型是 <xref:System.Windows.DependencyPropertyChangedEventArgs> 和 <xref:System.Windows.DependencyPropertyChangedEventHandler>。  这些属性更改的事件不会路由；它们是标准的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件。  <xref:System.Windows.DependencyPropertyChangedEventArgs> 不是普通的事件数据报告类型，因为它不是派生自 <xref:System.EventArgs>；<xref:System.Windows.DependencyPropertyChangedEventArgs> 是一个结构，而不是一个类。  
  
 使用 <xref:System.Windows.DependencyPropertyChangedEventArgs> 和 <xref:System.Windows.DependencyPropertyChangedEventHandler> 的事件比 `RoutedPropertyChanged` 事件稍稍通用一些。  使用这些类型的事件的一个示例是 <xref:System.Windows.UIElement.IsMouseCapturedChanged>。  
  
 与 <xref:System.Windows.RoutedPropertyChangedEventArgs%601> 类似，<xref:System.Windows.DependencyPropertyChangedEventArgs> 也报告属性的旧值和新值。  此外，关于可以对值执行的操作的注意事项也同样适用；通常不建议您为响应事件而尝试在发送方再次更改值。  
  
## 属性触发器  
 与属性更改事件密切相关的一个概念是属性触发器。  属性触发器是在样式或模板内部创建的，使用它，您可以创建基于分配有属性触发器的属性的值的条件行为。  
  
 属性触发器的属性必须是一个依赖项属性。  它可以是（并且通常是）只读依赖项属性。  要判断控件公开的依赖项属性是否至少部分设计为属性触发器，一个简单的方法是看属性名称是否以“Is”开头。  采用此命名规则的属性通常是只读的布尔依赖项属性，属性的主要方案是报告控件状态，可能与实时 UI 具有因果关系，并因此是一个属性触发器候选项。  
  
 其中的一些属性还具有专用属性更改事件。  例如，属性 <xref:System.Windows.UIElement.IsMouseCaptured%2A> 具有一个属性更改事件 <xref:System.Windows.UIElement.IsMouseCapturedChanged>。  该属性本身是只读的，其值由输入系统调整，并且输入系统对每次实时更改都引发 <xref:System.Windows.UIElement.IsMouseCapturedChanged>。  
  
 与真正的属性更改事件相比，使用属性触发器来作用于属性更改具有一些限制。  
  
 属性触发器通过完全匹配逻辑来工作。  您指定一个属性以及一个值，该值指示触发器将针对特定值工作。  例如：`<Setter Property="IsMouseCaptured" Value="true"> ... </Setter>`。  由于此限制，大多数属性触发器用法都将针对布尔属性或者采用专用枚举值的属性，其可能值范围是可管理的，足以为每种情况定义一个触发器。  或者属性触发器可能仅仅用于特殊值，例如，当项计数达到零，并且没有触发器来处理当属性值再次从零变为其他值的情况（这里您可能需要代码事件处理程序，或者当值不为零时再次从触发器状态切换回来的默认行为，而不是为所有情况都创建触发器）。  
  
 属性触发器语法与编程中的“if”语句类似。  如果触发器条件为 true，将“执行”属性触发器的“主体”。  属性触发器的“主体”是标记，而不是代码。  该标记被限制为只能使用一个或多个 <xref:System.Windows.Setter> 元素来设置应用样式或模板的对象的其他属性。  
  
 为了补偿具有各种可能值的属性触发器的“if”条件，通常最好使用 <xref:System.Windows.Setter> 将该属性值设置为默认值。  这样，当触发器条件为 true 时，<xref:System.Windows.Trigger> 包含的 setter 将具有优先权，而只要触发器条件为 false，则不在 <xref:System.Windows.Trigger> 内部的 <xref:System.Windows.Setter> 就具有优先权。  
  
 属性触发器通常适合于一个或多个外观属性应基于同一元素的其他属性的状态而更改的情况。  
  
 若要了解有关属性触发器的更多信息，请参见[样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)。  
  
## 请参阅  
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)