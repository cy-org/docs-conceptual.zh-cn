---
title: "附加事件概述 | Microsoft Docs"
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
  - "附加事件 [WPF], 定义"
  - "附加事件 [WPF], 方案"
  - "附加事件与路由事件 [WPF]"
  - "将路由事件用作附加事件的后备 [WPF]"
  - "将附加事件定义为路由事件 [WPF]"
  - "处理附加事件 [WPF]"
ms.assetid: 2c40eae3-80e4-4a45-ae09-df6c9ab4d91e
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 附加事件概述
[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 定义了一个语言组件和称为“附加事件”的事件类型。  附加事件的概念允许您针对特定事件为任意元素（而不是为实际定义或继承该事件的元素）添加处理程序。  在这种情况下，对象既不会引发该事件，目标处理实例也不会定义或“拥有”该事件。  
  
   
  
<a name="prerequisites"></a>   
## 必备组件  
 本主题假定您已阅读[路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)和 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)。  
  
<a name="Syntax"></a>   
## 附加事件语法  
 附加事件具有一种 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 语法和编码模式，后备代码必须使用该语法和编码模式才支持附加事件的使用。  
  
 在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 语法中，不仅可以通过事件名称来指定附加事件，而且还可以通过用点 \(.\) 分隔的事件拥有类型加上事件名称来指定。  因为事件名称是使用其拥有类型的名称限定的，所以附加事件语法允许将任何附加事件附加到可以实例化的任何元素上。  
  
 例如，下面是为自定义 `NeedsCleaning` 附加事件附加处理程序的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 语法：  
  
 [!code-xml[WPFAquariumSln#AE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquarium/Window1.xaml#ae)]  
  
 请注意 `aqua:` 前缀；该前缀在本例中是必需的，因为附加事件是来自自定义映射 xmlns 的自定义事件。  
  
<a name="WPFImplements"></a>   
## 如何在 WPF 中实现附加事件  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，附加事件由 <xref:System.Windows.RoutedEvent> 字段来支持，并在引发后通过元素树进行路由。  通常，附加事件的源（引发该事件的对象）是系统或服务源，所以运行引发该事件的代码的对象并不是元素树的直接组成部分。  
  
<a name="Scenarios"></a>   
## 附加事件的方案  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，附加事件存在于具有服务级抽象的某些功能区域，例如，对于通过静态 <xref:System.Windows.Input.Mouse> 类或 <xref:System.Windows.Controls.Validation> 类实现的事件。  与服务交互或使用服务的类可以在附加事件语法中使用该事件，也可以选择将附加事件作为路由事件来实现（这是类如何集成服务功能的一部分）。  
  
 尽管 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 定义了许多附加事件，但您直接使用或处理附加事件的方案却很有限。  一般情况下，附加事件用于实现体系结构目的，但随后即被转发给非附加（使用 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 事件“包装”提供支持）路由事件。  
  
 例如，通过针对该 <xref:System.Windows.UIElement> 使用 <xref:System.Windows.UIElement.MouseDown>（而不是在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 或代码中处理附加事件语法），可以针对任何给定的 <xref:System.Windows.UIElement>，更方便地处理基础附加事件 <xref:System.Windows.Input.Mouse.MouseDown?displayProperty=fullName>。  附加事件用于实现体系结构目的，因为它允许进一部扩展输入设备。  假设的设备只需引发 <xref:System.Windows.Input.Mouse.MouseDown?displayProperty=fullName> 即可模拟鼠标输入，而不需要从 <xref:System.Windows.Input.Mouse> 派生。  但是，此方案会涉及事件的代码处理，而附加事件的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理则与此方案无关。  
  
<a name="Handling"></a>   
## 在 WPF 中处理附加事件  
 处理附加事件的过程以及您将要编写的处理程序代码与路由事件基本相同。  
  
 一般情况下，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 附加事件与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 路由事件并没有太大的区别。  不同之处在于如何确定事件的源，以及如何通过类将事件作为成员进行公开。（这还将影响 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理程序语法。）  
  
 但是，正如前文所述，现有的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 附加事件并不是专门用于在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中进行处理。  该事件的目的常常是实现合成元素，以便向合成中的父元素报告某个状态，在这种情况下，该事件常常在代码中引发，并且还依赖于相关父类中的类处理。  例如，<xref:System.Windows.Controls.Primitives.Selector> 中的项应引发附加的 <xref:System.Windows.Controls.Primitives.Selector.Selected> 事件，该事件随后将由 <xref:System.Windows.Controls.Primitives.Selector> 类进行类处理，然后可能由 <xref:System.Windows.Controls.Primitives.Selector> 类转换为不同的路由事件 <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged>。  有关路由事件和类处理的更多信息，请参见[将路由事件标记为“已处理”和“类处理”](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md)。  
  
<a name="Custom"></a>   
## 将您自己的附加事件定义为路由事件  
 如果您从通用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 基类派生，则可以通过在类中包括某些模式方法并使用基类中已经存在的实用工具方法来实现您自己的附加事件。  
  
 模式如下：  
  
-   带有两个参数的方法 `Add*Handler`。  第一个参数必须标识事件，而标识的事件必须与方法名称中带有 \* 的名称相匹配。  第二个参数是要添加的处理程序。  该方法必须是公共且静态的，没有任何返回值。  
  
-   带有两个参数的方法 `Remove*Handler`。  第一个参数必须标识事件，而标识的事件必须与方法名称中带有 \* 的名称相匹配。  第二个参数是要移除的处理程序。  该方法必须是公共且静态的，没有任何返回值。  
  
 当针对某个元素声明附加事件处理程序特性时，`Add*Handler` 访问器方法可以加快 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理。  `Add*Handler` 和 `Remove*Handler` 方法还可实现对附加事件的事件处理程序存储区的代码访问。  
  
 这个普通模式对于框架中的实际实现还不够精确，因为任何给定的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 读取器实现都可能采用不同的架构在支持语言和体系结构中标识基础事件。  这是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 将附加事件作为路由事件来实现的原因之一；用于事件的标识符 \(<xref:System.Windows.RoutedEvent>\) 已经由 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 事件系统进行定义。  而且，路由一个事件也是对附加事件的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 语言级概念的自然实现扩展。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 附加事件的 `Add*Handler` 实现包括将路由事件和处理程序用作参数来调用 <xref:System.Windows.UIElement.AddHandler%2A>。  
  
 此实现策略和路由事件系统一般将附加事件的处理限制为 <xref:System.Windows.UIElement> 派生类或 <xref:System.Windows.ContentElement> 派生类，因为只有这些类才具有 <xref:System.Windows.UIElement.AddHandler%2A> 实现。  
  
 例如，下面的代码按照 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 将附加事件作为路由事件进行声明的附加事件策略为所有者类 `Aquarium` 定义 `NeedsCleaning` 附加事件。  
  
 [!code-csharp[WPFAquariumSln#AECode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#aecode)]
 [!code-vb[WPFAquariumSln#AECode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#aecode)]  
  
 请注意，用来确定附加事件标识符字段的方法 <xref:System.Windows.EventManager.RegisterRoutedEvent%2A> 实际上与用来注册非附加路由事件的方法相同。  附加事件和路由事件都是在集中管理的内部存储区中进行注册的。  此事件存储区实现则实现了[路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)中讨论的“事件作为界面”概念方面的注意事项。  
  
<a name="Raising"></a>   
## 引发 WPF 附加事件  
 通常不需要从代码中引发 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 定义的现有附加事件。  这些事件采用一般的“服务”概念模型，而服务类（如 <xref:System.Windows.Input.InputManager>）则负责引发事件。  
  
 但是，如果您根据将 <xref:System.Windows.RoutedEvent> 作为附加事件基础的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 模型来定义自定义附加事件，则可以使用 <xref:System.Windows.UIElement.RaiseEvent%2A> 从任何 <xref:System.Windows.UIElement> 或 <xref:System.Windows.ContentElement> 中引发附加事件。  引发路由事件（不管是否附加）要求声明元素树中的一个特定元素作为事件源；该事件源被报告为 <xref:System.Windows.UIElement.RaiseEvent%2A> 调用方。  您的服务负责决定将哪个元素报告为元素树中的事件源。  
  
## 请参阅  
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [XAML 语法详述](../../../../docs/framework/wpf/advanced/xaml-syntax-in-detail.md)   
 [XAML 及 WPF 的自定义类](../../../../docs/framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)