---
title: "对象生存期事件 | Microsoft Docs"
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
  - "Activated 事件"
  - "应用程序对象, 生存期事件"
  - "类, Frame"
  - "类, NavigationWindow"
  - "Closed 事件"
  - "Closing 事件"
  - "ContentRendered 事件"
  - "Deactivated 事件"
  - "事件, Activated"
  - "事件, 已关闭"
  - "事件, Closing"
  - "事件, ContentRendered"
  - "事件, Deactivated"
  - "事件, Initialized"
  - "事件, Loaded"
  - "事件, Unloaded"
  - "Exit 事件"
  - "Frame 类"
  - "Initialized 事件"
  - "对象的生存期事件"
  - "Loaded 事件"
  - "NavigationWindow 类"
  - "对象的生存期事件"
  - "Startup 事件"
  - "Unloaded 事件"
ms.assetid: face6fc7-465b-4502-bfe5-e88d2e729a78
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 对象生存期事件
本主题介绍表示对象生存期（创造、使用和析构）中的阶段的特定 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 事件。  
  
   
  
<a name="prerequisites"></a>   
## 必备组件  
 本主题假定您从 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 类的现有依赖项属性的使用者角度了解[依赖项属性](GTMT)，并且已阅读[依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)主题。  若要采用本主题中的示例，还应当了解[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]（请参见 [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)）并知道如何编写 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序。  
  
<a name="intro"></a>   
## 对象生存期事件  
 [!INCLUDE[TLA#tla_netframewk](../../../../includes/tlasharptla-netframewk-md.md)] 托管代码中的所有对象都要经历类似的一系列的生命阶段，即创造、使用和析构。  许多对象还包括生命终止阶段，该阶段属于析构阶段的一部分。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 对象，更具体而言，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 标识为元素的 Visual 对象，还具有对象生命的一系列通用阶段。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 编程和应用程序模型将这些阶段公开为一系列的事件。  在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中有四种与生存期事件有关的主要类型的对象；即常规元素、窗口元素、导航宿主和应用程序对象。  Windows 和导航宿主也都属于 Visual 对象（元素）这个较大的分组。  本主题先介绍对所有元素都通用的生存期事件，然后介绍应用于应用程序定义、窗口和导航宿主的更具体的生存期事件。  
  
<a name="common_events"></a>   
## 元素通用生存期事件  
 任何 [WPF 框架级](GTMT)元素（从 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.FrameworkContentElement> 派生的那些对象）都有三种通用的生存期事件：<xref:System.Windows.FrameworkElement.Initialized>、<xref:System.Windows.FrameworkElement.Loaded> 和 <xref:System.Windows.FrameworkElement.Unloaded>。  
  
### Initialized  
 首先引发 <xref:System.Windows.FrameworkElement.Initialized>，大致对应于由对其构造函数的调用执行的对象的初始化。  由于事件发生是为响应初始化，因此可以保证对象的所有属性均已设置。  （诸如动态资源或绑定等表达式用法是个例外；这些将是不进行计算的表达式。）需要设置所有属性的结果是，在标记中定义的嵌套元素引发的 <xref:System.Windows.FrameworkElement.Initialized> 的序列将开始发生，其顺序是先是元素树中最深层的元素，然后是朝向根的父元素。  此顺序的原因是父子关系和包容均为属性，因此直到填充该属性的子元素也完全初始化时，父级才能报告初始化。  
  
 当编写处理程序以响应 <xref:System.Windows.FrameworkElement.Initialized> 事件时，必须考虑无法保证元素树（[逻辑树](GTMT)或[可视化树](GTMT)）中处理程序所附加元素周围的所有其他元素（尤其是父元素）均已创建的情况。  成员变量可能为 null，或者基础绑定还未填充数据源（即使在表达式级别）。  
  
### Loaded  
 随后将引发 <xref:System.Windows.FrameworkElement.Loaded>。  在最终呈现之前，但是在布局系统已计算所有用于呈现所必需的值后，引发 <xref:System.Windows.FrameworkElement.Loaded> 事件。  <xref:System.Windows.FrameworkElement.Loaded> 要求包含元素的逻辑树是完整的，并连接到提供 HWND 和呈现图面的表示源。  标准数据绑定（到本地源的绑定，例如，其他属性或直接定义的数据源）将在 <xref:System.Windows.FrameworkElement.Loaded> 之前发生。  可能已发生异步数据绑定（外部或动态源），但是根据其异步特性的定义不能保证已发生异步数据绑定（外部或动态源）。  
  
 引发 <xref:System.Windows.FrameworkElement.Loaded> 事件的机制不同于 <xref:System.Windows.FrameworkElement.Initialized>。  将逐个元素引发 <xref:System.Windows.FrameworkElement.Initialized> 事件，而无需通过整个元素树直接协调。  相反，引发 <xref:System.Windows.FrameworkElement.Loaded> 事件是在整个元素树内协调的结果（特别是[逻辑树](GTMT)）。  当树中所有元素都处于被视为已加载状态中时，将首先在根元素上引发 <xref:System.Windows.FrameworkElement.Loaded> 事件。  然后在每个子级元素上连续引发 <xref:System.Windows.FrameworkElement.Loaded> 事件。  
  
> [!NOTE]
>  这种行为表面上可能类似[路由事件](GTMT)的隧道。  但是，未将任何信息从事件传送到事件。  每个元素始终有机会处理其 <xref:System.Windows.FrameworkElement.Loaded> 事件，并且将事件数据标记为已处理仅影响该元素。  
  
### Unloaded  
 最后引发 <xref:System.Windows.FrameworkElement.Unloaded>，并由表示源或要移除的可视父级启动。  当引发 <xref:System.Windows.FrameworkElement.Unloaded> 并对其进行处理后，可能还未设置属于事件源父级（由 <xref:System.Windows.FrameworkElement.Parent%2A> 属性确定）的元素或逻辑树或可视树中任何给定元素以上的元素，因此可能无法将样式设置为其正常或最后已知的运行时值。  
  
<a name="application_model_elements"></a>   
## 生存期事件应用程序模型元素  
 以元素的通用生存期事件为基础构建的有以下应用程序模型元素：<xref:System.Windows.Application>、<xref:System.Windows.Window>、<xref:System.Windows.Controls.Page>、<xref:System.Windows.Navigation.NavigationWindow> 和 <xref:System.Windows.Controls.Frame>。  这些元素使用与其特定用途关联的附加事件扩展了通用生存期事件。  将在以下位置详细介绍这些内容：  
  
-   <xref:System.Windows.Application>: [应用程序管理概述](../../../../docs/framework/wpf/app-development/application-management-overview.md).  
  
-   <xref:System.Windows.Window>: [WPF Windows 概述](../../../../docs/framework/wpf/app-development/wpf-windows-overview.md).  
  
-   <xref:System.Windows.Controls.Page>、<xref:System.Windows.Navigation.NavigationWindow> 和 <xref:System.Windows.Controls.Frame>：[导航概述](../../../../docs/framework/wpf/app-development/navigation-overview.md)。  
  
## 请参阅  
 [依赖项属性值优先级](../../../../docs/framework/wpf/advanced/dependency-property-value-precedence.md)   
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)