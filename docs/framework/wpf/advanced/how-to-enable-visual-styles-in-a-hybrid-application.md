---
title: "如何：在混合应用程序中启用视觉样式 | Microsoft Docs"
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
  - "混合应用程序 [WPF 互操作性]"
  - "视觉样式 [Windows 窗体]"
ms.assetid: 95de9b9c-d804-405c-b2d1-49a88c1e0fe1
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：在混合应用程序中启用视觉样式
本主题演示如何在基于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的应用程序中承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件上启用 [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] 视觉样式。  
  
 如果应用程序调用 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> 方法，则当应用程序在 [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] 上运行时，大多数 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件将自动使用视觉样式。  有关更多信息，请参见[使用视觉样式呈现控件](../../../../docs/framework/winforms/controls/rendering-controls-with-visual-styles.md)。  
  
 有关本主题中所阐释任务的完整代码清单，请参见 [Enabling Visual Styles in a Hybrid Application Sample](http://go.microsoft.com/fwlink/?LinkID=159986)（在混合应用程序中启用可视样式示例）。  
  
## 启用 Windows 窗体视觉样式  
  
#### 启用 Windows 窗体视觉样式  
  
1.  创建一个名为 `HostingWfWithVisualStyles` 的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序项目。  
  
2.  在解决方案资源管理器中，添加对以下程序集的引用。  
  
    -   WindowsFormsIntegration  
  
    -   System.Windows.Forms  
  
3.  在工具箱中，双击 <xref:System.Windows.Controls.Grid> 图标，在设计图面上放置一个 <xref:System.Windows.Controls.Grid> 元素。  
  
4.  在“属性”窗口中，将 <xref:System.Windows.FrameworkElement.Height%2A> 和 <xref:System.Windows.FrameworkElement.Width%2A> 属性的值设置为**“自动”**。  
  
5.  在设计视图或 XAML 视图中，选择 <xref:System.Windows.Window>。  
  
6.  在“属性”窗口中，单击**“事件”**选项卡。  
  
7.  双击 <xref:System.Windows.FrameworkElement.Loaded> 事件。  
  
8.  在 MainWindow.xaml.vb 或 MainWindow.xaml.cs 中，插入以下代码以处理 <xref:System.Windows.FrameworkElement.Loaded> 事件。  
  
     [!code-csharp[HostingWfWithVisualStyles#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HostingWfWithVisualStyles/CSharp/HostingWfWithVisualStyles/Window1.xaml.cs#11)]
     [!code-vb[HostingWfWithVisualStyles#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWfWithVisualStyles/VisualBasic/HostingWfWithVisualStyles/Window1.xaml.vb#11)]  
  
9. 按 F5 生成并运行该应用程序。  
  
     将使用视觉样式绘制 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。  
  
## 禁用 Windows 窗体视觉样式  
 若要禁用视觉样式，只需移除对 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> 方法的调用。  
  
#### 禁用 Windows 窗体视觉样式  
  
1.  在代码编辑器中打开 MainWindow.xaml.vb 或 MainWindow.xaml.cs。  
  
2.  注释掉对 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> 方法的调用。  
  
3.  按 F5 生成并运行该应用程序。  
  
     将使用默认系统样式绘制 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。  
  
## 请参阅  
 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A>   
 <xref:System.Windows.Forms.VisualStyles>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [使用视觉样式呈现控件](../../../../docs/framework/winforms/controls/rendering-controls-with-visual-styles.md)   
 [演练：在 WPF 中承载 Windows 窗体控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md)