---
title: "演练：在 WPF 中排列 Windows 窗体控件 | Microsoft Docs"
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
  - "排列控件"
  - "混合应用程序 [WPF 互操作性]"
ms.assetid: a1db8049-15c7-45d6-ae3d-36a6735cb848
caps.latest.revision: 31
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 28
---
# 演练：在 WPF 中排列 Windows 窗体控件
本演练演示如何使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 布局功能在混合应用程序中排列 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。  
  
 本演练涉及以下任务：  
  
-   创建项目。  
  
-   使用默认布局设置。  
  
-   根据内容调整大小。  
  
-   使用绝对定位。  
  
-   显式指定大小。  
  
-   设置布局属性。  
  
-   了解 Z 顺序限制。  
  
-   停靠。  
  
-   设置可见性。  
  
-   承载不拉伸的控件。  
  
-   缩放。  
  
-   旋转。  
  
-   设置空白和边距。  
  
-   使用动态布局容器。  
  
 有关本演练中所阐释任务的完整代码清单，请参见 [Arranging Windows Forms Controls in WPF Sample](http://go.microsoft.com/fwlink/?LinkID=159971)（在 WPF 中排列 Windows 窗体控件示例）。  
  
 在完成本演练后，您将对基于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的应用程序中的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]布局功能有一定了解。  
  
## 系统必备  
 您需要以下组件来完成本演练：  
  
-   [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)].  
  
## 创建项目  
  
#### 创建和设置项目  
  
1.  创建一个名为 `WpfLayoutHostingWf` 的 WPF 应用程序项目。  
  
2.  在解决方案资源管理器中，添加对以下程序集的引用。  
  
    -   WindowsFormsIntegration  
  
    -   System.Windows.Forms  
  
    -   System.Drawing  
  
3.  双击 MainWindow.xaml 将其在 XAML 视图中打开。  
  
4.  在 <xref:System.Windows.Window> 元素中，添加以下 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]命名空间映射。  
  
    ```xaml  
    xmlns:wf="clr-namespace:System.Windows.Forms;assembly=System.Windows.Forms"  
    ```  
  
5.  在 <xref:System.Windows.Controls.Grid> 元素中，将 <xref:System.Windows.Controls.Grid.ShowGridLines%2A> 属性设置为 `true`，并定义五行和三列。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#2)]  
  
## 使用默认布局设置  
 默认情况下，<xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素处理所承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件的布局。  
  
#### 使用默认布局设置  
  
1.  将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素中。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#3)]  
  
2.  按 F5 生成并运行该应用程序。  此时 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] <xref:System.Windows.Forms.Button?displayProperty=fullName> 控件将出现在 <xref:System.Windows.Controls.Canvas> 中。  所承载的控件根据其内容调整大小，并且 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素也会根据所承载的控件调整大小。  
  
## 根据内容调整大小  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素确保调整所承载的控件的大小，以正确地显示其内容。  
  
#### 根据内容调整大小  
  
1.  将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素中。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#4)]  
  
2.  按 F5 生成并运行该应用程序。  两个新按钮控件会调整大小以正确地显示较长的文本字符串和较大的字号，并且 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素也会根据所承载的控件调整大小。  
  
## 使用绝对定位  
 您可以使用绝对定位将 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素放在用户界面 \(UI\) 中的任意位置。  
  
#### 使用绝对定位  
  
1.  将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素中。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#5)]  
  
2.  按 F5 生成并运行该应用程序。  <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素置于网格单元格中距离顶部 20 像素、距离左侧 20 像素的位置。  
  
## 显式指定大小  
 可以使用 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 属性指定 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素的大小。  
  
#### 显式指定大小  
  
1.  将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素中。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#6)]  
  
2.  按 F5 生成并运行该应用程序。  <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素的大小设置为 50 像素宽、70 像素高，这比默认布局设置小。  [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件的内容相应地重新排列。  
  
## 设置布局属性  
 应始终使用 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素的属性对所承载的控件设置与布局有关的属性。  直接对所承载的控件设置布局属性会产生意外的结果。  
  
 以 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 对所承载的控件设置与布局有关的属性无效。  
  
#### 查看对所承载的控件设置属性的效果  
  
1.  将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素中。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#7)]  
  
2.  在“解决方案资源管理器”中，双击 MainWindow.xaml.  vb 或 MainWindow.xaml.cs 以在代码编辑器中将其打开。  
  
3.  将下面的代码复制到 `MainWindow` 类定义中。  
  
     [!code-csharp[WpfLayoutHostingWfWithXaml#101](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#101)]
     [!code-vb[WpfLayoutHostingWfWithXaml#101](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#101)]  
  
4.  按 F5 生成并运行该应用程序。  
  
5.  单击**“Click me”（单击这里）**按钮。  `button1_Click` 事件处理程序设置所承载的控件的 <xref:System.Windows.Forms.Control.Top%2A> 和 <xref:System.Windows.Forms.Control.Left%2A> 属性。  这导致所承载的控件在 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素中重新定位。  宿主占据相同的屏幕区域，但所承载的控件被剪辑。  所承载的控件应总是填充 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素。  
  
## 了解 Z 顺序限制  
 默认情况下，可见 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素始终绘制在其他 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素的顶部，并且，它们按 z 顺序不受影响。  若要启用 z 顺序，请设置 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 的 <xref:System.Windows.Interop.HwndHost.IsRedirected%2A> 属性设置为 true 和 <xref:System.Windows.Interop.HwndHost.CompositionMode%2A> 属性设置为 <xref:System.Windows.Interop.CompositionMode.Full> 或 <xref:System.Windows.Interop.CompositionMode.OutputOnly>。  
  
#### 查看默认 z 顺序行为  
  
1.  将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素中。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#8)]  
  
2.  按 F5 生成并运行该应用程序。  <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素绘制在标签元素的上面。  
  
#### 查看 z 顺序行为，当 IsRedirected 为 true  
  
1.  用下面的 XAML 替换以前的 z 顺序示例。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#8b](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml#8b)]  
  
     按 F5 生成并运行该应用程序。  label 元素绘制在 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素。  
  
## 停靠  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素支持 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 停靠。  设置 <xref:System.Windows.Controls.DockPanel.Dock%2A> 附加属性，以便将所承载的控件停靠在 <xref:System.Windows.Controls.DockPanel> 元素中。  
  
#### 停靠所承载的控件  
  
1.  将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素中。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#9)]  
  
2.  按 F5 生成并运行该应用程序。  <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素停靠在 <xref:System.Windows.Controls.DockPanel> 元素的右侧。  
  
## 设置可见性  
 通过在 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素上设置 <xref:System.Windows.UIElement.Visibility%2A> 属性，可以使 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件不可见或将它折叠。  当控件不可见时，它不会显示，但会占据布局空间。  当控件折叠时，它不会显示，也不会占据布局控件。  
  
#### 设置所承载控件的可见性  
  
1.  将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素中。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#10)]  
  
2.  在 MainWindow.xaml.vb 或 MainWindow.xaml.cs 中，将以下代码复制到类定义中。  
  
     [!code-csharp[WpfLayoutHostingWfWithXaml#102](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#102)]
     [!code-vb[WpfLayoutHostingWfWithXaml#102](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#102)]  
  
3.  按 F5 生成并运行该应用程序。  
  
4.  单击**“Click to make invisible”（单击隐藏）**按钮使 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素不可见。  
  
5.  单击**“Click to collapse”（单击折叠）**按钮使 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素完全从布局中隐藏。  当 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件折叠时，周围的元素会重新排列以占据它的空间。  
  
## 承载不拉伸的控件  
 一些 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件具有固定的大小，不会拉伸以填满布局中的可用空间。  例如，<xref:System.Windows.Forms.MonthCalendar> 控件在固定的空间中显示月份。  
  
#### 承载不拉伸的控件  
  
1.  将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素中。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#11)]  
  
2.  按 F5 生成并运行该应用程序。  <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素在网格行中居中，但它不会拉伸以填满可用空间。  如果窗口足够大，您可能会看到所承载的 <xref:System.Windows.Forms.MonthCalendar> 控件显示两个或更多个月份，但这些月份在一行中居中。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 布局引擎使不能调整大小以填满可用空间的元素居中。  
  
## 缩放  
 与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素不同，大多数 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件都不是可连续缩放的。  默认情况下， <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素调用其承载的控件，如果可能。  若要启用完整的缩放，请设置 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 的 <xref:System.Windows.Interop.HwndHost.IsRedirected%2A> 属性设置为 true 和 <xref:System.Windows.Interop.HwndHost.CompositionMode%2A> 属性设置为 <xref:System.Windows.Interop.CompositionMode.Full> 或 <xref:System.Windows.Interop.CompositionMode.OutputOnly>。  
  
#### 通过使用默认行为，对所承载的控件进行缩放  
  
1.  将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素中。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#12)]  
  
2.  按 F5 生成并运行该应用程序。  所承载的控件及其周围元素按 0.5 的比例进行缩放。  但是，所承载控件的字体不缩放。  
  
#### 通过设置为 true IsRedirected 对所承载的控件进行缩放  
  
1.  用下面的 XAML 替换以前缩放示例。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#12b](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml#12b)]  
  
2.  按 F5 生成并运行该应用程序。  所承载的控件、它周围的元素和承载控件的字体按 0.5 的比例缩放。  
  
## 旋转  
 与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素不同，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件不支持旋转。  默认情况下，那么，当应用旋转变换时， <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素不旋转与其他 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素。  180 度以外的任何旋转值都会引发 <xref:System.Windows.Forms.Integration.WindowsFormsHost.LayoutError> 事件。  若要启用对所有旋转角度来看，请设置 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 的 <xref:System.Windows.Interop.HwndHost.IsRedirected%2A> 属性设置为 true 和 <xref:System.Windows.Interop.HwndHost.CompositionMode%2A> 属性设置为 <xref:System.Windows.Interop.CompositionMode.Full> 或 <xref:System.Windows.Interop.CompositionMode.OutputOnly>。  
  
#### 查看混合应用程序中的旋转效果  
  
1.  将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素中。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#13)]  
  
2.  按 F5 生成并运行该应用程序。  所承载的控件不旋转，但是它周围的元素旋转 180 度。  您可能必须调整窗口大小才能看到这些元素。  
  
#### 看到的旋转效果在混合应用程序中，当 IsRedirected 为 true  
  
1.  用下面的 XAML 替换以前的旋转示例。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#13b](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml#13b)]  
  
2.  按 F5 生成并运行该应用程序。  所承载的控件上旋转。  请注意 <xref:System.Windows.Media.RotateTransform.Angle%2A> 属性可设置为任何值。  您可能必须调整窗口大小才能看到这些元素。  
  
## 设置空白和边距  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 布局中的空白和边距与 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]中的空白和边距类似。  只需在 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素上设置 <xref:System.Windows.Controls.Control.Padding%2A> 和 <xref:System.Windows.FrameworkElement.Margin%2A> 属性。  
  
#### 为承载的控件设置空白和边距  
  
1.  将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素中。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#14)]  
    [!code-xml[WpfLayoutHostingWfWithXaml#15](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#15)]  
  
2.  按 F5 生成并运行该应用程序。  空白和边距设置应用于承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件，就像在 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]中应用一样。  
  
## 使用动态布局容器  
 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]提供两个动态布局容器，即 <xref:System.Windows.Forms.FlowLayoutPanel> 和 <xref:System.Windows.Forms.TableLayoutPanel>。  您还可以在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 布局中使用这些容器。  
  
#### 使用动态布局容器  
  
1.  将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素中。  
  
     [!code-xml[WpfLayoutHostingWfWithXaml#16](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml#16)]  
  
2.  在 MainWindow.xaml.vb 或 MainWindow.xaml.cs 中，将以下代码复制到类定义中。  
  
     [!code-csharp[WpfLayoutHostingWfWithXaml#103](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#103)]
     [!code-vb[WpfLayoutHostingWfWithXaml#103](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#103)]  
  
3.  在构造函数中添加对 `InitializeFlowLayoutPanel` 方法的调用。  
  
     [!code-csharp[WpfLayoutHostingWfWithXaml#104](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/CSharp/Window1.xaml.cs#104)]
     [!code-vb[WpfLayoutHostingWfWithXaml#104](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfLayoutHostingWfWithXaml/VisualBasic/Window1.xaml.vb#104)]  
  
4.  按 F5 生成并运行该应用程序。  <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素填充 <xref:System.Windows.Controls.DockPanel>，<xref:System.Windows.Forms.FlowLayoutPanel> 按默认 <xref:System.Windows.Forms.FlowLayoutPanel.FlowDirection%2A> 排列它的子控件。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)   
 [WindowsFormsHost 元素的布局注意事项](../../../../docs/framework/wpf/advanced/layout-considerations-for-the-windowsformshost-element.md)   
 [Arranging Windows Forms Controls in WPF Sample](http://go.microsoft.com/fwlink/?LinkID=159971)   
 [演练：在 WPF 中承载 Windows 窗体复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)   
 [演练：在 Windows 窗体中承载 WPF 复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)