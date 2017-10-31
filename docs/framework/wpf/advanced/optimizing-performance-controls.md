---
title: "优化性能：控件 | Microsoft Docs"
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
  - "容器回收"
  - "控件 [WPF], 改善性能"
  - "用户界面虚拟化"
ms.assetid: 45a31c43-ea8a-4546-96c8-0631b9934179
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# 优化性能：控件
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 包括许多公共用户界面 \(UI\) 组件，大多数 Windows 应用程序中都会用到这些组件。  本主题介绍一些改进用户界面性能的技术。  
  
   
  
<a name="Displaying"></a>   
## 显示大型数据集  
 WPF 控件（如 <xref:System.Windows.Controls.ListView> 和 <xref:System.Windows.Controls.ComboBox>）用于在应用程序中显示项列表。  如果要显示的列表很大，则应用程序的性能可能会受到影响。  这是因为标准布局系统会为每个与列表控件关联的项创建一个布局容器，并计算其布局大小和位置。  一般来说，您不需要同时显示所有的项，而只需显示一个子集，用户可滚动查看列表。  在这种情况下，使用用户界面虚拟化很有意义，这意味着项容器生成和项的关联布局计算会推迟到相应项可见的时候进行。  
  
 用户界面虚拟化是列表控件的一个重要方面。  不应将用户界面虚拟化与数据虚拟化混淆。  用户界面虚拟化只将可见项存储在内存中，但在数据绑定应用场景中，它会将整个数据结构存储在内存中。  相反，数据虚拟化只将屏幕上可见的数据项存储在内存中。  
  
 默认情况下，只有当 <xref:System.Windows.Controls.ListView> 和 <xref:System.Windows.Controls.ListBox> 控件的列表项绑定到数据时，才会对这些控件启用 UI 虚拟化。  通过将 <xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizing%2A?displayProperty=fullName> 附加属性设置为 `true`，可以启用 <xref:System.Windows.Controls.TreeView> 虚拟化。  如果要对派生自 <xref:System.Windows.Controls.ItemsControl> 的自定义控件或使用 <xref:System.Windows.Controls.StackPanel> 类的现有项控件（如 <xref:System.Windows.Controls.ComboBox>）启用用户界面虚拟化，可将 <xref:System.Windows.Controls.ItemsControl.ItemsPanel%2A> 设置为 <xref:System.Windows.Controls.VirtualizingStackPanel>，并将 <xref:System.Windows.Controls.VirtualizingPanel.IsVirtualizing%2A> 设置为 `true`。  遗憾的是，您可能会在没有意识到的情况下对这些控件禁用用户界面虚拟化。  以下是禁用用户界面虚拟化的条件的列表。  
  
-   项容器直接添加到 <xref:System.Windows.Controls.ItemsControl>。  例如，如果应用程序将 <xref:System.Windows.Controls.ListBoxItem> 对象显式添加到 <xref:System.Windows.Controls.ListBox>，则 <xref:System.Windows.Controls.ListBox> 不会虚拟化 <xref:System.Windows.Controls.ListBoxItem> 对象。  
  
-   <xref:System.Windows.Controls.ItemsControl> 中的项容器属于不同类型。  例如，使用 <xref:System.Windows.Controls.Separator> 对象的 <xref:System.Windows.Controls.Menu> 无法实现项回收，因为 <xref:System.Windows.Controls.Menu> 包含 <xref:System.Windows.Controls.Separator> 和 <xref:System.Windows.Controls.MenuItem> 类型的对象。  
  
-   将 <xref:System.Windows.Controls.ScrollViewer.CanContentScroll%2A> 设置为 `false`。  
  
-   将 <xref:System.Windows.Controls.VirtualizingStackPanel.IsVirtualizing%2A> 设置为 `false`。  
  
 一个重要注意事项，当您有效项容器时是您是否具有不同的状态信息关联与属于该项的项容器。  在这种情况下，必须保存其他状态。  例如，您可能有一个包含在 <xref:System.Windows.Controls.Expander> 控件中的项，<xref:System.Windows.Controls.Expander.IsExpanded%2A> 状态绑定到该项的容器，而不是绑定到该项本身。  当将该容器重用于新项时，<xref:System.Windows.Controls.Expander.IsExpanded%2A> 的当前值也用于新项。  此外，旧项会丢失正确的 <xref:System.Windows.Controls.Expander.IsExpanded%2A> 值。  
  
 当前，没有 WPF 控件提供对数据虚拟化的内置支持。  
  
<a name="Container"></a>   
## 容器回收  
 “容器回收”是 .NET Framework 3.5 SP1 针对继承自 <xref:System.Windows.Controls.ItemsControl> 的控件新增的一项用户界面虚拟化优化功能，它还可以改进滚动性能。  在填充使用用户界面虚拟化的 <xref:System.Windows.Controls.ItemsControl> 时，它会为滚动到视图中的每个项创建一个项容器，并销毁滚动到视图之外的每个项的项容器。  通过容器回收，控件能够将现有项容器重复用于不同的数据项，因此当用户滚动 <xref:System.Windows.Controls.ItemsControl> 时，不会反复地创建和销毁项容器。  可以选择启用回收通过设置项目该 <xref:System.Windows.Controls.VirtualizingPanel.VirtualizationMode%2A> 附加属性设置为 <xref:System.Windows.Controls.VirtualizationMode>。  
  
 任何支持虚拟化的 <xref:System.Windows.Controls.ItemsControl> 都可以使用容器回收。  有关如何在 <xref:System.Windows.Controls.ListBox> 上启用容器回收的示例，请参见[提高 ListBox 的滚动性能](../../../../docs/framework/wpf/controls/how-to-improve-the-scrolling-performance-of-a-listbox.md)。  
  
<a name="Supporting"></a>   
## 支持双向虚拟化  
 <xref:System.Windows.Controls.VirtualizingStackPanel> 提供对一个方向（水平或垂直）上的用户界面虚拟化的内置支持。  如果您要对控件使用双向虚拟化，则必须实现一个扩展 <xref:System.Windows.Controls.VirtualizingStackPanel> 类的自定义面板。  <xref:System.Windows.Controls.VirtualizingStackPanel> 类公开虚方法，例如 <xref:System.Windows.Controls.VirtualizingStackPanel.OnViewportSizeChanged%2A>、<xref:System.Windows.Controls.VirtualizingStackPanel.LineUp%2A>、<xref:System.Windows.Controls.VirtualizingStackPanel.PageUp%2A> 和 <xref:System.Windows.Controls.VirtualizingStackPanel.MouseWheelUp%2A>。这些虚方法使您能够检测列表的可见部分中的更改，并相应地进行处理。  
  
<a name="Optimizing"></a>   
## 优化模板  
 可视化树中包含应用程序中的所有可视元素。  除了直接创建的对象之外，它还包含由于模板扩展而创建的对象。  例如，在创建 <xref:System.Windows.Controls.Button> 时，可视化树中还包含 <xref:Microsoft.Windows.Themes.ClassicBorderDecorator> 和 <xref:System.Windows.Controls.ContentPresenter> 对象。  如果您尚未优化控件模板，则可能在可视化树中创建大量不必要的额外对象。  有关可视化树的更多信息，请参见 [WPF 图形呈现疑难解答](../../../../docs/framework/wpf/graphics-multimedia/wpf-graphics-rendering-overview.md)。  
  
<a name="Deferred"></a>   
## 延迟滚动  
 默认情况下，当用户拖动滚动条上的滚动块时，内容视图会不断更新。  如果控件中的滚动速度很慢，请考虑使用延迟滚动。  在延迟滚动中，只有当用户松开滚动块时，内容才会更新。  
  
 若要实现延迟滚动，请将 <xref:System.Windows.Controls.ScrollViewer.IsDeferredScrollingEnabled%2A> 属性设置为 `true`。  <xref:System.Windows.Controls.ScrollViewer.IsDeferredScrollingEnabled%2A> 是一个附加属性，可在 <xref:System.Windows.Controls.ScrollViewer> 上设置，也可在其控件模板中具有 <xref:System.Windows.Controls.ScrollViewer> 的任何控件上设置。  
  
<a name="Controls"></a>   
## 实现性能功能的控件  
 下表列出了用于显示数据的公共控件，以及它们对性能功能的支持。  有关如何启用这些功能的信息，请参见上面几部分。  
  
|控件|虚拟化|容器回收|延迟滚动|  
|--------|---------|----------|----------|  
|<xref:System.Windows.Controls.ComboBox>|可以启用|可以启用|可以启用|  
|<xref:System.Windows.Controls.ContextMenu>|可以启用|可以启用|可以启用|  
|<xref:System.Windows.Controls.DocumentViewer>|不可用|不可用|可以启用|  
|<xref:System.Windows.Controls.ListBox>|默认|可以启用|可以启用|  
|<xref:System.Windows.Controls.ListView>|默认|可以启用|可以启用|  
|<xref:System.Windows.Controls.TreeView>|可以启用|可以启用|可以启用|  
|<xref:System.Windows.Controls.ToolBar>|不可用|不可用|可以启用|  
  
> [!NOTE]
>  有关如何在 <xref:System.Windows.Controls.TreeView> 上启用虚拟化和容器回收的示例，请参见[提高 TreeView 的性能](../../../../docs/framework/wpf/controls/how-to-improve-the-performance-of-a-treeview.md)。  
  
## 请参阅  
 [布局](../../../../docs/framework/wpf/advanced/layout.md)   
 [布局和设计](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [数据绑定](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [控件](../../../../docs/framework/wpf/controls/index.md)   
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [演练：在 WPF 应用程序中缓存应用程序数据](../../../../docs/framework/wpf/advanced/walkthrough-caching-application-data-in-a-wpf-application.md)