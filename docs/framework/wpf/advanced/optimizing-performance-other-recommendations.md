---
title: "优化性能：其他建议 | Microsoft Docs"
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
  - "画笔, 性能"
  - "命中测试对象 [WPF]"
  - "不透明度"
  - "ScrollBarVisibility 枚举"
  - "终端服务呈现"
ms.assetid: d028cc65-7e97-4a4f-9859-929734eaf40d
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 优化性能：其他建议
<a name="introduction"></a> 本主题提供[优化 WPF 应用程序性能](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)这一节中各主题内容之外的性能改进建议。  
  
 本主题包含以下各节：  
  
-   [画笔的不透明度与元素的不透明度](#Opacity)  
  
-   [导航到对象](#Navigation_Objects)  
  
-   [对大型三维图面进行命中测试](#Hit_Testing)  
  
-   [CompositionTarget.Rendering 事件](#CompositionTarget_Rendering_Event)  
  
-   [避免使用 ScrollBarVisibility\=Auto](#Avoid_Using_ScrollBarVisibility)  
  
-   [配置字体缓存服务以缩短启动时间](#FontCache)  
  
<a name="Opacity"></a>   
## 画笔的不透明度与元素的不透明度  
 在使用 <xref:System.Windows.Media.Brush> 设置元素的 <xref:System.Windows.Shapes.Shape.Fill%2A> 或 <xref:System.Windows.Shapes.Shape.Stroke%2A> 时，设置 <xref:System.Windows.Media.Brush.Opacity%2A?displayProperty=fullName> 值比设置元素的 <xref:System.Windows.UIElement.Opacity%2A> 属性效果要好。  修改元素的 <xref:System.Windows.UIElement.Opacity%2A> 属性会导致 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 创建临时图面。  
  
<a name="Navigation_Objects"></a>   
## 导航到对象  
 <xref:System.Windows.Navigation.NavigationWindow> 对象派生自 <xref:System.Windows.Window> 并用内容导航支持对其进行了扩展，这主要是通过聚合 <xref:System.Windows.Navigation.NavigationService> 与日记完成的。  通过指定[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 或对象，您可以更新 <xref:System.Windows.Navigation.NavigationWindow> 的工作区。  下面的示例演示了这两种方法：  
  
 [!code-csharp[Performance#PerformanceSnippet14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/TestNavigation.xaml.cs#performancesnippet14)]
 [!code-vb[Performance#PerformanceSnippet14](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Performance/visualbasic/testnavigation.xaml.vb#performancesnippet14)]  
  
 每个 <xref:System.Windows.Navigation.NavigationWindow> 对象都有一个日记，其中记录了用户在该窗口中的导航历史记录。  日记的作用之一便是用户可通过它回溯他们执行的步骤。  
  
 当您使用[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 导航时，日记只存储[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 引用。  这意味着，每当您重新访问该页时都会动态地重新构造该页。根据页面的复杂程度，此过程可能会非常耗时。  在这种情况下，虽然占用的日记存储较少，但用于重建该页的时间可能会较长。  
  
 当您使用对象进行导航时，日记会存储对象的整个可视化树。  这意味着，每当您重新访问该页时，无需重新构造即可立即呈现该页。  在这种情况下，虽然占用的日记存储较多，但重建页面的时间却较短。  
  
 使用 <xref:System.Windows.Navigation.NavigationWindow> 对象时，您需要记住日记支持是如何对应用程序的性能造成影响的。  有关更多信息，请参见[导航概述](../../../../docs/framework/wpf/app-development/navigation-overview.md)。  
  
<a name="Hit_Testing"></a>   
## 对大型三维图面进行命中测试  
 就 CPU 占用率而言，对大型三维图面进行命中测试是一项非常占用资源的操作。  这在三维图面具有动画效果时更是如此。  如果不需要对这些图面进行命中测试，请禁用命中测试。  通过将 <xref:System.Windows.UIElement.IsHitTestVisible%2A> 属性设置为 `false`，派生自 <xref:System.Windows.UIElement> 的对象可以禁用命中测试。  
  
<a name="CompositionTarget_Rendering_Event"></a>   
## CompositionTarget.Rendering 事件  
 <xref:System.Windows.Media.CompositionTarget.Rendering?displayProperty=fullName> 事件可使 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 连续显示动画效果。  使用此事件时，应尽量将其分离。  
  
<a name="Avoid_Using_ScrollBarVisibility"></a>   
## 避免使用 ScrollBarVisibility\=Auto  
 应尽量避免对 `HorizontalScrollBarVisibility` 和 `VerticalScrollBarVisibility` 属性使用 <xref:System.Windows.Controls.ScrollBarVisibility?displayProperty=fullName> 值。  这些属性是为 <xref:System.Windows.Controls.RichTextBox>、<xref:System.Windows.Controls.ScrollViewer> 和 <xref:System.Windows.Controls.TextBox> 对象定义的，并且定义为 <xref:System.Windows.Controls.ListBox> 对象的附加属性。  应改为将 <xref:System.Windows.Controls.ScrollBarVisibility> 设置为 <xref:System.Windows.Controls.ScrollBarVisibility>、<xref:System.Windows.Controls.ScrollBarVisibility> 或 <xref:System.Windows.Controls.ScrollBarVisibility>。  
  
 <xref:System.Windows.Controls.ScrollBarVisibility> 值适用于空间有限且只应在必要时才显示滚动条的情况。  例如，与具有数百行文本的 <xref:System.Windows.Controls.TextBox> 相比，在具有 30 个项目的 <xref:System.Windows.Controls.ListBox> 中使用此 <xref:System.Windows.Controls.ScrollBarVisibility> 值可能会更为有用。  
  
<a name="FontCache"></a>   
## 配置字体缓存服务以缩短启动时间  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 字体缓存服务负责在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序之间共享字体数据。  如果该服务尚未运行，则运行第一个 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序时将启动此服务。  如果您使用的是 [!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)]，则可以将“[!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 字体缓存 3.0.0.0”服务从“手动”（默认值）设置为“自动\(延迟的启动\)”，以缩短 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序的初始启动时间。  
  
## 请参阅  
 [规划应用程序性能](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)   
 [利用硬件](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)   
 [布局和设计](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [二维图形和图像处理](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [对象行为](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)   
 [应用程序资源](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [数据绑定](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [动画提示和技巧](../../../../docs/framework/wpf/graphics-multimedia/animation-tips-and-tricks.md)