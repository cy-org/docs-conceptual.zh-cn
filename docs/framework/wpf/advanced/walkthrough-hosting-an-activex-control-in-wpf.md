---
title: "演练：在 WPF 中承载 ActiveX 控件 | Microsoft Docs"
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
  - "ActiveX 控件 [WPF 互操作性]"
  - "承载 ActiveX 控件"
ms.assetid: 1931d292-0dd1-434f-963c-dcda7638d75a
caps.latest.revision: 30
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 30
---
# 演练：在 WPF 中承载 ActiveX 控件
若要改进与浏览器的交互，可以在基于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的应用程序中使用 [!INCLUDE[TLA#tla_actx](../../../../includes/tlasharptla-actx-md.md)] 控件。  本演练演示如何在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 页上将 [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] 作为控件来承载。  
  
 本演练涉及以下任务：  
  
-   创建项目。  
  
-   创建 ActiveX 控件。  
  
-   在 WPF 页上承载 ActiveX 控件。  
  
 在完成本演练之后，您将了解如何在基于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的应用程序中使用 [!INCLUDE[TLA#tla_actx](../../../../includes/tlasharptla-actx-md.md)] 控件。  
  
## 系统必备  
 您需要以下组件来完成本演练：  
  
-   在装有 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 的计算机上安装 [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)]。  
  
-   [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)].  
  
## 创建项目  
  
#### 创建和设置项目  
  
1.  创建名为 `HostingAxInWpf` 的 WPF 应用程序项目。  
  
2.  向解决方案中添加一个 Windows 窗体控件库项目，将该项目命名为 `WmpAxLib`。  
  
3.  在 WmpAxLib 项目中，添加对 Windows Media Player 程序集（名为 wmp.dll）的引用。  
  
4.  打开**“工具箱”**。  
  
5.  在**“工具箱”**中右击，再单击**“选择项”**。  
  
6.  单击**“COM 组件”**选项卡，选择**“Windows Media Player”**控件，然后单击**“确定”**。  
  
     Windows Media Player 控件会添加到**“工具箱”**中。  
  
7.  在解决方案资源管理器中，右击**“UserControl1”**文件，再单击**“重命名”**。  
  
8.  根据语言，将名称更改为 `WmpAxControl.vb` 或 `WmpAxControl.cs`。  
  
9. 如果系统提示您重命名所有的引用，请单击**“是”**。  
  
## 创建 ActiveX 控件  
 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 自动在 [!INCLUDE[TLA#tla_actx](../../../../includes/tlasharptla-actx-md.md)] 控件添加到设计图面时为该控件生成 <xref:System.Windows.Forms.AxHost> 包装类。  下面的过程会创建一个名为 AxInterop.WMPLib.dll 的托管程序集。  
  
#### 创建 ActiveX 控件  
  
1.  在 Windows 窗体设计器中，打开 WmpAxControl.vb 或 WmpAxControl.cs。  
  
2.  从**“工具箱”**中，将 Windows Media Player 控件添加到设计图面。  
  
3.  在“属性”窗口中，将 Windows Media Player 控件的 <xref:System.Windows.Forms.Control.Dock%2A> 属性的值设置为 <xref:System.Windows.Forms.DockStyle>。  
  
4.  生成 WmpAxLib 控件库项目。  
  
## 在 WPF 页上承载 ActiveX 控件  
  
#### 承载 ActiveX 控件  
  
1.  在 HostingAxInWpf 项目中，添加一个对所生成的 [!INCLUDE[TLA2#tla_actx](../../../../includes/tla2sharptla-actx-md.md)] 互操作程序集的引用。  
  
     此程序集的名称为 AxInterop.WMPLib.dll，当您导入 Windows Media Player 控件时，此程序集会添加到 WmpAxLib 项目的 Debug 文件夹中。  
  
2.  添加一个对名为 WindowsFormsIntegration.dll 的 WindowsFormsIntegration 程序集的引用。  
  
3.  添加一个对名为 System.Windows.Forms.dll 的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]程序集的引用。  
  
4.  在 WPF 设计器中打开 MainWindow.xaml。  
  
5.  将 <xref:System.Windows.Controls.Grid> 元素命名为 `grid1`。  
  
     [!code-xml[HostingAxInWpf#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HostingAxInWpf/CSharp/HostingAxInWpf/window1.xaml#1)]  
  
6.  在设计视图或 XAML 视图中，选择 <xref:System.Windows.Window> 元素。  
  
7.  在“属性”窗口中，单击**“事件”**选项卡。  
  
8.  双击 <xref:System.Windows.FrameworkElement.Loaded> 事件。  
  
9. 插入下面的代码以处理 <xref:System.Windows.FrameworkElement.Loaded> 事件。  
  
     此代码会创建一个 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件实例，并添加一个 `AxWindowsMediaPlayer` 控件实例来作为其子级。  
  
     [!code-csharp[HostingAxInWpf#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HostingAxInWpf/CSharp/HostingAxInWpf/window1.xaml.cs#11)]
     [!code-vb[HostingAxInWpf#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HostingAxInWpf/VisualBasic/HostingAxInWpf/window1.xaml.vb#11)]  
  
10. 按 F5 生成并运行该应用程序。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)   
 [演练：在 WPF 中承载 Windows 窗体复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)   
 [演练：在 Windows 窗体中承载 WPF 复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)