---
title: "基元素概述 | Microsoft Docs"
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
  - "基元素"
ms.assetid: 2c997092-72c6-4767-bc84-74267f4eee72
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 基元素概述
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的大部分类都是从 [!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)] 文档中通常称为基元素类的四个类派生而来。  这些类包括 <xref:System.Windows.UIElement>、<xref:System.Windows.FrameworkElement>、<xref:System.Windows.ContentElement> 和 <xref:System.Windows.FrameworkContentElement>。  <xref:System.Windows.DependencyObject> 也相关，因为它是 <xref:System.Windows.UIElement> 和 <xref:System.Windows.ContentElement> 的公共基类。  
  
   
  
<a name="base_apis"></a>   
## WPF 类中的基元素 API  
 <xref:System.Windows.UIElement> 和 <xref:System.Windows.ContentElement> 都是从 <xref:System.Windows.DependencyObject> 派生而来，但途径略有不同。  此级别的拆分涉及到 <xref:System.Windows.UIElement> 或 <xref:System.Windows.ContentElement> 在用户界面中的使用方式，以及它们在应用程序起到什么作用。  <xref:System.Windows.UIElement> 在其类层次结构中还有 <xref:System.Windows.Media.Visual>，后者是一个类，它公开 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 底层较低级别的图形支持。  <xref:System.Windows.Media.Visual> 定义独立的矩形屏幕区域，从而提供呈现框架。  在实践中，<xref:System.Windows.UIElement> 适用于支持大型数据模型的元素，这些元素旨在向可以称为矩形屏幕区域的区域中进行呈现和布局，在这些区域中内容模型特意地更加开放，以允许元素进行各种组合。  <xref:System.Windows.ContentElement> 不是从 <xref:System.Windows.Media.Visual> 派生的；它的模型是其他对象（例如随后将解释元素并生成完整的 <xref:System.Windows.Media.Visual> 供 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 使用的阅读器或查看器）将使用 <xref:System.Windows.ContentElement>。  某些 <xref:System.Windows.UIElement> 类要用作内容宿主：这些类为一个或多个 <xref:System.Windows.ContentElement> 类（<xref:System.Windows.Controls.DocumentViewer> 就是此类的一个示例）提供承载和呈现。  <xref:System.Windows.ContentElement> 用作以下元素的基类：所具有的对象模型稍小，并且更多地用于对 <xref:System.Windows.UIElement> 中可能承载的文本、信息或文档内容进行寻址。  
  
### 框架级和核心级  
 <xref:System.Windows.UIElement> 用作 <xref:System.Windows.FrameworkElement> 的基类，<xref:System.Windows.ContentElement> 用作 <xref:System.Windows.FrameworkContentElement> 的基类。  对于此下一级类，原因是要支持与[框架级](GTMT)相分离的 [WPF 核心级](GTMT)，这种分离还存在于 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 如何在 PresentationCore 和 PresentationFramework 程序集之间进行划分。  [WPF 框架级](GTMT)为基本应用程序需要提供了一个更完整的解决方案，包括用于表示的布局管理器的实现。  [WPF 核心级](GTMT)提供了一种方法，以充分利用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，而又不至于产生附加程序集开销。  对于大多数典型的应用程序开发方案而言，这些级别之间的区别很少有影响，而且一般情况下应将 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 视为一个整体，而无需担心 [WPF 框架级](GTMT)与 [WPF 核心级](GTMT)之间有何区别。  如果您的应用程序设计选择替换大量 [WPF 框架级](GTMT)功能，例如，如果您的整体解决方案已经有其自己的[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 组合和布局实现，则可能需要了解级别之间的差异。  
  
<a name="subclassing_elements"></a>   
## 选择从哪个元素派生  
 创建用于扩展 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的自定义类的最实用方法是从某个 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 类中派生，这样您可以通过现有的类层次结构获得尽可能多的所需功能。  本节列出了三个最重要的元素类附带的功能，以帮助您决定要从哪个类进行派生。  
  
 如果您要实现控件（这的确是从 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 类派生的更常见的原因之一），您可能需要从以下类中派生：实际控件、控件系列基类或至少是 <xref:System.Windows.Controls.Control> 基类。  有关部分指导信息和实用示例，请参见[控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)。  
  
 如果您不是创建控件，并且需要从层次结构中较高的类进行派生，则可以参考下列各节的内容，了解每个基元素类定义了哪些特征。  
  
 如果您创建从 <xref:System.Windows.DependencyObject> 派生的类，则将继承以下功能：  
  
-   <xref:System.Windows.DependencyObject.GetValue%2A> 和 <xref:System.Windows.DependencyObject.SetValue%2A> 支持以及一般的属性系统支持。  
  
-   使用以下两种属性的能力：[依赖项属性](GTMT)，以及作为[依赖项属性](GTMT)实现的[附加属性](GTMT)。  
  
 如果您创建从 <xref:System.Windows.UIElement> 派生的类，则除了能够继承 <xref:System.Windows.DependencyObject> 提供的功能外，还将继承以下功能：  
  
-   对动画属性值的基本支持。  有关更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
-   对基本输入事件和命令的支持。  有关更多信息，请参见[输入概述](../../../../docs/framework/wpf/advanced/input-overview.md)和[命令概述](../../../../docs/framework/wpf/advanced/commanding-overview.md)。  
  
-   可以重写以便为布局系统提供信息的虚方法。  
  
 如果您创建从 <xref:System.Windows.FrameworkElement> 派生的类，则除了能够继承 <xref:System.Windows.UIElement> 提供的功能外，还将继承以下功能：  
  
-   对样式设置和演示图板的支持。  有关更多信息，请参见 <xref:System.Windows.Style> 和[演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)。  
  
-   对数据绑定的支持。  有关更多信息，请参见[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。  
  
-   对动态资源引用的支持。  有关更多信息，请参见[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
-   对属性值继承以及元数据中有助于向框架服务报告属性的相关情况（如数据绑定、样式或布局的框架实现）的其他标志的支持。  有关更多信息，请参见[框架属性元数据](../../../../docs/framework/wpf/advanced/framework-property-metadata.md)。  
  
-   [逻辑树](GTMT)的概念。  有关更多信息，请参见 [WPF 中的树](../../../../docs/framework/wpf/advanced/trees-in-wpf.md)。  
  
-   对布局系统的实际 [WPF 框架级](GTMT)实现的支持，包括 <xref:System.Windows.FrameworkElement.OnPropertyChanged%2A> 重写（该重写可以检测到影响布局的属性更改）。  
  
 如果您创建从 <xref:System.Windows.ContentElement> 派生的类，则除了能够继承 <xref:System.Windows.DependencyObject> 提供的功能外，还将继承以下功能：  
  
-   对动画的支持。  有关更多信息，请参见[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
-   对基本输入事件和命令的支持。  有关更多信息，请参见[输入概述](../../../../docs/framework/wpf/advanced/input-overview.md)和[命令概述](../../../../docs/framework/wpf/advanced/commanding-overview.md)。  
  
 如果您创建从 <xref:System.Windows.FrameworkContentElement> 派生的类，则除了能够继承 <xref:System.Windows.ContentElement> 提供的功能外，还将获得以下功能：  
  
-   对样式设置和演示图板的支持。  有关更多信息，请参见 <xref:System.Windows.Style> 和[动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)。  
  
-   对数据绑定的支持。  有关更多信息，请参见[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。  
  
-   对动态资源引用的支持。  有关更多信息，请参见[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
-   对属性值继承以及元数据中有助于向框架服务报告属性情况（如数据绑定、样式或布局的框架实现）的其他标志的支持。  有关更多信息，请参见[框架属性元数据](../../../../docs/framework/wpf/advanced/framework-property-metadata.md)。  
  
-   您不会继承对布局系统修改（如 <xref:System.Windows.FrameworkElement.ArrangeOverride%2A>）的访问权限。  布局系统实现只在 <xref:System.Windows.FrameworkElement> 上提供。  但是，您会继承 <xref:System.Windows.FrameworkElement.OnPropertyChanged%2A> 重写（可以检测影响布局的属性更改并将这些更改报告给任何内容宿主）。  
  
 记录了各种类的内容模型。  如果您要找到一个合适的类以便从该类进行派生，其内容模型是一个应该考虑的可能因素。  有关更多信息，请参见 [WPF 内容模型](../../../../docs/framework/wpf/controls/wpf-content-model.md)。  
  
<a name="other_base_classes"></a>   
## 其他基类  
  
### DispatcherObject  
 <xref:System.Windows.Threading.DispatcherObject> 为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 线程模型提供支持，并允许为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序创建的所有对象与 <xref:System.Windows.Threading.Dispatcher> 相关联。  即使不从 <xref:System.Windows.UIElement>、<xref:System.Windows.DependencyObject> 或 <xref:System.Windows.Media.Visual> 派生，也应考虑从 <xref:System.Windows.Threading.DispatcherObject> 派生，以获得对线程模型的这种支持。  有关更多信息，请参见[线程处理模型](../../../../docs/framework/wpf/advanced/threading-model.md)。  
  
### Visual  
 <xref:System.Windows.Media.Visual> 实现二维对象在近似矩形的区域中通常需要具有可视化表示的概念。  <xref:System.Windows.Media.Visual> 的实际呈现发生在其他类中（不是独立的），但 <xref:System.Windows.Media.Visual> 类提供一个由呈现过程在多种级别使用的已知类型。  <xref:System.Windows.Media.Visual> 实现命中测试，但它不公开报告命中测试阳性结果（这些结果位于 <xref:System.Windows.UIElement> 中）的事件。  有关更多信息，请参见[可视化层编程](../../../../docs/framework/wpf/graphics-multimedia/visual-layer-programming.md)。  
  
### Freezable  
 <xref:System.Windows.Freezable> 通过在出于性能原因需要不可变对象时提供为对象生成副本的途径，来模拟可变对象的不变性。  <xref:System.Windows.Freezable> 类型为某些图形元素（如几何形状、画笔以及动画）提供了一个通用的基础。  值得注意的是，<xref:System.Windows.Freezable> 不是一个 <xref:System.Windows.Media.Visual>；当应用 <xref:System.Windows.Freezable> 以填充另一个对象的属性值时，它包含的属性将变成子属性，而这些子属性可能会影响呈现。  有关更多信息，请参见 [Freezable 对象概述](../../../../docs/framework/wpf/advanced/freezable-objects-overview.md)。  
  
 <xref:System.Windows.Media.Animation.Animatable>  
  
 <xref:System.Windows.Media.Animation.Animatable> 是一个 <xref:System.Windows.Freezable> 派生类，它特别添加了动画控件层和某些实用工具成员，从而使当前动画的属性可以与未动画的属性区分开。  
  
### 控件  
 <xref:System.Windows.Controls.Control> 是称为控件或组件（取决于技术）的对象类型的理想基类。  一般而言，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件类是直接表示 UI 控件或积极参与控件组合的类。  <xref:System.Windows.Controls.Control> 实现的主要功能是控件模板化。  
  
## 请参阅  
 <xref:System.Windows.Controls.Control>   
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)   
 [WPF 体系结构](../../../../docs/framework/wpf/advanced/wpf-architecture.md)