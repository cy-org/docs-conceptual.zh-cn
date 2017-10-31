---
title: "优化性能：应用程序资源 | Microsoft Docs"
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
  - "应用程序资源, 性能"
  - "画笔, 性能"
  - "资源, 性能"
  - "不进行复制而共享画笔"
  - "共享资源"
  - "静态资源"
ms.assetid: 62b88488-c08e-4804-b7de-a1c34fbe929c
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 优化性能：应用程序资源
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 允许您共享应用程序资源，以便您可以在类型相似的元素之间保持一致的外观或行为。  本主题针对该领域提供了一些建议，以帮助您改进您的应用程序的性能。  
  
 有关资源的更多信息，请参见[XAML 资源](../../../../docs/framework/wpf/advanced/xaml-resources.md)。  
  
## 共享资源  
 如果您的应用程序使用自定义控件，并在 <xref:System.Windows.ResourceDictionary>（或 XAML 资源节点）中定义资源，则建议您在 <xref:System.Windows.Application> 或 <xref:System.Windows.Window> 对象级别定义它们，或在自定义控件的默认主题中定义它们。  在自定义控件的 <xref:System.Windows.ResourceDictionary> 中定义资源会影响该控件每个实例的性能。  例如，如果在某个自定义控件以及该自定义控件的许多实例的资源定义中定义了对性能要求非常高的画笔操作，则应用程序的工作集将显著增加。  
  
 以下示例说明了这一点：  假设您在使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 开发一个纸牌游戏。  对于大多数纸牌游戏，需要 52 张牌，52 种不同的外观。  您决定实现一个纸牌自定义控件，并在该控件的资源中定义 52 支画笔（每支画笔代表一种纸牌外观）。  在您的主应用程序中，最初创建该纸牌自定义控件的 52 个实例。  该纸牌自定义控件的每个实例生成 52 个 <xref:System.Windows.Media.Brush> 对象实例，在您的应用程序中提供 52 \* 52 个 <xref:System.Windows.Media.Brush> 对象。  通过将画笔从纸牌自定义控件资源移出到 <xref:System.Windows.Application> 或 <xref:System.Windows.Window> 对象级别，或者在自定义控件的默认主题中定义它们，您减少了应用程序的工作集，因为您现在在纸牌控件的 52 个实例中共享 52 支画笔。  
  
## 不进行复制而共享画笔  
 如果有多个元素使用同一个 <xref:System.Windows.Media.Brush> 对象，请将画笔定义为资源并引用它，而不要在 [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)] 中以内联方式定义它。  该方法将创建一个实例并重复使用它，而在 [!INCLUDE[TLA#tla_titlexaml](../../../../includes/tlasharptla-titlexaml-md.md)] 中以内联方式定义画笔会为每个元素创建一个新实例。  
  
 下面的标记示例说明了这一点：  
  
 [!code-xml[Performance#PerformanceSnippet7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/BrushResource.xaml#performancesnippet7)]  
  
## 尽可能使用静态资源  
 静态资源通过查找对已定义资源的引用，为任何 XAML 属性特性提供值。  对该资源的查找行为类似于编译时查找。  
  
 另一方面，动态资源则在初始编译过程中创建一个临时表达式，因而会延迟到实际需要所请求的资源值来构造对象时，才会查找资源。  对该资源的查找行为类似于运行时查找，这种查找会影响性能。  因此，请在应用程序中尽量使用静态资源，只在必需的情况下才使用动态资源。  
  
 下面的标记示例演示了这两种类型的资源的使用情况：  
  
 [!code-xml[Performance#PerformanceSnippet8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/DynamicResource.xaml#performancesnippet8)]  
  
## 请参阅  
 [优化 WPF 应用程序性能](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [规划应用程序性能](../../../../docs/framework/wpf/advanced/planning-for-application-performance.md)   
 [利用硬件](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)   
 [布局和设计](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [二维图形和图像处理](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [对象行为](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [数据绑定](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [其他性能建议](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)