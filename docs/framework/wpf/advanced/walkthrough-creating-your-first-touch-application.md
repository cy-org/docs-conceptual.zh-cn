---
title: "演练：创建您的第一个触控应用程序 | Microsoft Docs"
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
  - "创建触摸屏应用程序 [WPF]"
  - "创建触控敏感型应用程序 [WPF]"
  - "触摸屏应用程序 [WPF], 创建"
  - "触控敏感型应用程序 [WPF], 创建"
ms.assetid: d69e602e-9a25-4e24-950b-e89eaa2a906b
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 演练：创建您的第一个触控应用程序
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使应用程序可以对触控做出响应。  例如，您可以通过用一个或多个手指操纵触控敏感型设备（如触摸屏）来与应用程序交互。此演练将创建一个使用户可以使用触控功能移动、旋转一个对象或调整其大小的应用程序。  
  
## 必备组件  
 您需要以下组件来完成本演练：  
  
-   [!INCLUDE[vs_dev10_ext](../../../../includes/vs-dev10-ext-md.md)].  
  
-   Windows 7。  
  
-   接受触控输入的设备，如支持 Windows 触摸屏技术的触摸屏。  
  
 此外，您应该大致了解如何在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中创建应用程序，尤其是如何订阅和处理事件。  有关更多信息，请参见 [演练：开始使用 WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)。  
  
## 创建应用程序  
  
#### 创建应用程序  
  
1.  使用 Visual Basic 或 Visual C\# 新建一个名为 `BasicManipulation` 的 WPF 应用程序项目。  有关更多信息，请参见[如何：创建新的 WPF 应用程序项目](http://msdn.microsoft.com/zh-cn/1f6aea7a-33e1-4d3f-8555-1daa42e95d82)。  
  
2.  用以下 XAML 替换 MainWindow.xaml 的内容。  
  
     此标记会创建一个在 <xref:System.Windows.Controls.Canvas> 上包含红色 <xref:System.Windows.Shapes.Rectangle> 的简单应用程序。  <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.UIElement.IsManipulationEnabled%2A> 属性设置为 true，以使其可以接收操作事件。  该应用程序订阅 <xref:System.Windows.UIElement.ManipulationStarting>、<xref:System.Windows.UIElement.ManipulationDelta> 和 <xref:System.Windows.UIElement.ManipulationInertiaStarting> 事件。  这些事件包含在用户操作 <xref:System.Windows.Shapes.Rectangle> 时对该形状进行移动的逻辑。  
  
     [!code-xml[BasicManipulation#UI](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicmanipulation/csharp/mainwindow.xaml#ui)]  
  
3.  如果使用的是 Visual Basic，请在 MainWindow.xaml 的第一行中将 `x:Class="BasicManipulation.MainWindow"` 替换为 `x:Class="MainWindow"`。  
  
4.  在 `MainWindow` 类中，添加以下 <xref:System.Windows.UIElement.ManipulationStarting> 事件处理程序。  
  
     当 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 检测到触控输入开始操作对象时，会发生 <xref:System.Windows.UIElement.ManipulationStarting> 事件。  该代码通过设置 <xref:System.Windows.Input.ManipulationStartingEventArgs.ManipulationContainer%2A> 属性指定操作位置应相对于 <xref:System.Windows.Window>。  
  
     [!code-csharp[BasicManipulation#ManipulationStarting](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicmanipulation/csharp/mainwindow.xaml.cs#manipulationstarting)]
     [!code-vb[BasicManipulation#ManipulationStarting](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/basicmanipulation/visualbasic/mainwindow.xaml.vb#manipulationstarting)]  
  
5.  在 `MainWindow` 类中，添加以下 <xref:System.Windows.Input.ManipulationDelta> 事件处理程序。  
  
     <xref:System.Windows.Input.ManipulationDelta> 事件会在触控输入改变位置时发生，并且会在操作期间多次发生。  此事件还会在抬起手指后发生。  例如，如果用户在屏幕上拖动手指，则在手指移动时，会多次发生 <xref:System.Windows.Input.ManipulationDelta> 事件。  当用户将手指从屏幕上抬起时，<xref:System.Windows.Input.ManipulationDelta> 事件会不断发生以模拟惯性。  
  
     该代码将 <xref:System.Windows.Input.ManipulationDeltaEventArgs.DeltaManipulation%2A> 应用到 <xref:System.Windows.Shapes.Rectangle> 的 <xref:System.Windows.UIElement.RenderTransform%2A> 以在用户移动触控输入时移动该元素。  它还检查当在惯性期间发生该事件时 <xref:System.Windows.Shapes.Rectangle> 是否在 <xref:System.Windows.Window> 的边界之外。  如果是，则应用程序会调用 <xref:System.Windows.Input.ManipulationDeltaEventArgs.Complete%2A?displayProperty=fullName> 方法来结束操作。  
  
     [!code-csharp[BasicManipulation#ManipulationDelta](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicmanipulation/csharp/mainwindow.xaml.cs#manipulationdelta)]
     [!code-vb[BasicManipulation#ManipulationDelta](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/basicmanipulation/visualbasic/mainwindow.xaml.vb#manipulationdelta)]  
  
6.  在 `MainWindow` 类中，添加以下 <xref:System.Windows.UIElement.ManipulationInertiaStarting> 事件处理程序。  
  
     当用户将所有手指从屏幕上抬起时，会发生 <xref:System.Windows.UIElement.ManipulationInertiaStarting> 事件。  该代码会为矩形的移动、展开和旋转设置初始速度和减速。  
  
     [!code-csharp[BasicManipulation#ManipulationInertiaStarting](../../../../samples/snippets/csharp/VS_Snippets_Wpf/basicmanipulation/csharp/mainwindow.xaml.cs#manipulationinertiastarting)]
     [!code-vb[BasicManipulation#ManipulationInertiaStarting](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/basicmanipulation/visualbasic/mainwindow.xaml.vb#manipulationinertiastarting)]  
  
7.  生成并运行该项目。  
  
     您应该会看到窗口中显示一个红色的正方形。  
  
## 测试应用程序  
 若要测试应用程序，请尝试执行下列操作。  请注意，您可以同时执行以下多项操作。  
  
-   若要移动 <xref:System.Windows.Shapes.Rectangle>，请将手指放在 <xref:System.Windows.Shapes.Rectangle> 上并在屏幕上移动手指。  
  
-   若要调整 <xref:System.Windows.Shapes.Rectangle> 的大小，请将两个手指放在 <xref:System.Windows.Shapes.Rectangle> 上，并将两个手指靠拢或将其分开。  
  
-   若要旋转 <xref:System.Windows.Shapes.Rectangle>，请将两个手指放在 <xref:System.Windows.Shapes.Rectangle> 上，然后将一个手指围绕另一个手指旋转。  
  
 若要产生惯性，请在执行前面的操作时快速将手指从屏幕上抬起。  <xref:System.Windows.Shapes.Rectangle> 将继续移动、调整大小或旋转几秒钟，然后再停止。  
  
## 请参阅  
 <xref:System.Windows.UIElement.ManipulationStarting?displayProperty=fullName>   
 <xref:System.Windows.UIElement.ManipulationDelta?displayProperty=fullName>   
 <xref:System.Windows.UIElement.ManipulationInertiaStarting?displayProperty=fullName>