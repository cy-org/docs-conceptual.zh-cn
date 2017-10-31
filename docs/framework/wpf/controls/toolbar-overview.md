---
title: "ToolBar 概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "控件, ToolBar"
  - "ToolBar 控件"
ms.assetid: a8edb32c-118d-4f31-b6e6-8899082b504b
caps.latest.revision: 28
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 27
---
# ToolBar 概述
<xref:System.Windows.Controls.ToolBar> 控件是一组通常在功能上相关的命令或控件的容器。  <xref:System.Windows.Controls.ToolBar> 通常包含用于调用命令的按钮。  
  
   
  
<a name="ToolBarControl"></a>   
## ToolBar 控件  
 <xref:System.Windows.Controls.ToolBar> 控件因其按钮或其他控件像条形栏一样排列成一行或一列而得名。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.ToolBar> 控件提供一种溢出机制，将不能自然适合于有大小限制的 <xref:System.Windows.Controls.ToolBar> 的任意项放入一个特殊的溢出区域。  另外，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.ToolBar> 控件通常还与相关的 <xref:System.Windows.Controls.ToolBarTray> 控件一起使用，后者提供特殊的布局行为，并支持用户启动的工具栏大小调整和排列。  
  
<a name="Creating_ToolBars"></a>   
## 在 ToolBarTray 中指定工具栏的位置  
 使用 <xref:System.Windows.Controls.ToolBar.Band%2A> 和 <xref:System.Windows.Controls.ToolBar.BandIndex%2A> 属性定位 <xref:System.Windows.Controls.ToolBarTray> 中的 <xref:System.Windows.Controls.ToolBar>。  <xref:System.Windows.Controls.ToolBar.Band%2A> 指示 <xref:System.Windows.Controls.ToolBar> 在其父 <xref:System.Windows.Controls.ToolBarTray> 中的位置。  <xref:System.Windows.Controls.ToolBar.BandIndex%2A> 指示 <xref:System.Windows.Controls.ToolBar> 放入其 Band 中的顺序。  下面的示例演示如何使用此属性在 <xref:System.Windows.Controls.ToolBarTray> 内放置 <xref:System.Windows.Controls.ToolBar> 控件。  
  
 [!code-xml[ToolBarExample#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolBarExample/CS/Pane1.xaml#2)]  
  
<a name="ToolBars_with_Overflow_Items"></a>   
## 具有溢出项的工具栏  
 通常，<xref:System.Windows.Controls.ToolBar> 控件包含的项多于工具栏大小可以容纳的项数。  出现此情况时，<xref:System.Windows.Controls.ToolBar> 会显示一个溢出按钮。  要查看溢出项，用户可以单击溢出按钮，这些项即会显示在 <xref:System.Windows.Controls.ToolBar> 下方的弹出窗口中。  下图显示了一个带溢出项的 <xref:System.Windows.Controls.ToolBar>。  
  
 ![存在溢出的工具栏](../../../../docs/framework/wpf/controls/media/toolbarwithoverflowitem.png "ToolbarWithOverflowItem")  
具有溢出项的工具栏  
  
 通过将 <xref:System.Windows.Controls.ToolBar.OverflowMode%2A?displayProperty=fullName> 附加属性设置为 <xref:System.Windows.Controls.OverflowMode?displayProperty=fullName>、<xref:System.Windows.Controls.OverflowMode?displayProperty=fullName> 或 <xref:System.Windows.Controls.OverflowMode?displayProperty=fullName>，您可以指定工具栏上的项何时会放置在溢出面板上。  下面的示例指定工具栏上的最后四个按钮应总是显示在溢出面板上。  
  
 [!code-xml[ToolBarExample#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolBarExample/CS/Pane1.xaml#3)]  
  
 <xref:System.Windows.Controls.ToolBar> 在其 <xref:System.Windows.Controls.ControlTemplate> 中使用 <xref:System.Windows.Controls.Primitives.ToolBarPanel> 和 <xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>。  <xref:System.Windows.Controls.Primitives.ToolBarPanel> 负责工具栏上的项的布局。  <xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel> 负责 <xref:System.Windows.Controls.ToolBar> 上容不下的项的布局。  有关 <xref:System.Windows.Controls.ToolBar> 的 <xref:System.Windows.Controls.ControlTemplate> 的示例，请参见  
  
 [ToolBar 样式和模板](../../../../docs/framework/wpf/controls/toolbar-styles-and-templates.md).  
  
## 请参阅  
 <xref:System.Windows.Controls.Primitives.ToolBarPanel>   
 <xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>   
 [设置 ToolBar 上的控件的样式](../../../../docs/framework/wpf/controls/how-to-style-controls-on-a-toolbar.md)   
 [WPF Controls Gallery Sample](http://go.microsoft.com/fwlink/?LinkID=160053)