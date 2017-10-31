---
title: "演练：开始使用 WPF | Microsoft Docs"
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
  - "入门, WPF"
  - "WPF, 入门"
ms.assetid: b96bed40-8946-4285-8fe4-88045ab854ed
caps.latest.revision: 71
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 68
---
# 演练：开始使用 WPF
<a name="introduction"></a> 本演练介绍了包含元素对于大多数 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序所共有的 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 应用程序的开发: [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 标记，代码隐藏中，应用程序定义、控件、布局、数据绑定和样式。  
  
 使用以下步骤，本演练通过简单的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序的开发引导您完成。  
  
-   定义 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 设计应用程序的 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]的外观。  
  
-   编写代码以生成应用程序的行为。  
  
-   创建应用程序定义托管应用程序。  
  
-   添加控件和创建布局以构成应用程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  
  
-   创建样式创建在应用程序的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]中的一致的外观。  
  
-   绑定 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 到数据请填写从数据的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 并保留数据，并 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 同步。  
  
 在本演练结束时，您生成了用户可以查看所选人员的零用金报销单的独立 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 应用程序。  应用程序在浏览器样式的窗口承载的几 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 页组成。  
  
 用于生成此演练中的代码示例为 [!INCLUDE[TLA#tla_visualb](../../../../includes/tlasharptla-visualb-md.md)] 和 [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] 可用[生成 WPF 应用程序简介](http://go.microsoft.com/fwlink/?LinkID=160008)。  
  
<a name="Requirements"></a>   
## 系统必备  
 您需要以下组件来完成本演练:  
  
-   [!INCLUDE[vs_dev11_long](../../../../includes/vs-dev11-long-md.md)]  
  
 有关安装 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)]的更多信息，请 [安装 Visual Studio](../Topic/Install%20Visual%20Studio%202015.md)参见。  
  
<a name="Create_The_Application_Code_Files"></a>   
## 创建应用程序项目  
 在本节中，您将创建应用程序基础结构，其中包括一个应用程序定义，这两个页和一个图像。  
  
1.  创建新的 WPF 名为 `ExpenseIt`的应用程序项目在 Visual Basic 或 Visual C\#。  有关更多信息，请参见 [如何：创建新的 WPF 应用程序项目](http://msdn.microsoft.com/zh-cn/1f6aea7a-33e1-4d3f-8555-1daa42e95d82)。  
  
    > [!NOTE]
    >  本演练使用能在 .NET framework 4. 的 <xref:System.Windows.Controls.DataGrid> 控件。  请确保项目以 .NET framework 4。  有关更多信息，请参见 [如何：面向 .NET Framework 的某个版本](../Topic/How%20to:%20Target%20a%20Version%20of%20the%20.NET%20Framework.md)。  
  
2.  打开 Application.xaml \(Visual Basic\) 或 App.xaml \(c\#\)。  
  
     此 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件定义一 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序和任何应用程序资源。 也可以使用此文件指定自动显示的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，当应用程序启动时;在这种情况下， MainWindow.xaml。  
  
     您的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 应如下所示在 Visual Basic 中:  
  
     [!code-xml[ExpenseIt#1_A](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/Application.xaml#1_a)]  
  
     或 c\# 中应如下所示:  
  
     [!code-xml[ExpenseIt#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/App.xaml#1)]  
  
3.  打开 MainWindow.xaml。  
  
     此 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件是应用程序的主窗口并在页中创建的内容。  <xref:System.Windows.Window> 类定义窗口的属性，例如标题、大小或图标和处理事件，如关闭或隐藏。  
  
4.  更改 <xref:System.Windows.Window> 元素。 <xref:System.Windows.Navigation.NavigationWindow>。  
  
     此应用程序将导航到其他基于目录的用户交互。  因此，主 <xref:System.Windows.Window> 需要更改为 <xref:System.Windows.Navigation.NavigationWindow>。  <xref:System.Windows.Navigation.NavigationWindow> 继承 <xref:System.Windows.Window>所有属性。  在 XAML 文件的 <xref:System.Windows.Navigation.NavigationWindow> 元素创建 <xref:System.Windows.Navigation.NavigationWindow> 类的实例。  有关更多信息，请参见 [导航概述](../../../../docs/framework/wpf/app-development/navigation-overview.md)。  
  
5.  将 <xref:System.Windows.Navigation.NavigationWindow> 元素的下列属性:  
  
    -   设置 <xref:System.Windows.Window.Title%2A> 属性设置为 “ExpenseIt”。  
  
    -   设置 <xref:System.Windows.FrameworkElement.Width%2A> 属性设置为 500 像素。  
  
    -   设置 <xref:System.Windows.FrameworkElement.Height%2A> 属性设置为 350 像素。  
  
    -   移除 <xref:System.Windows.Controls.Grid> 元素在 <xref:System.Windows.Navigation.NavigationWindow> 标记之间。  
  
     您的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 应如下所示在 Visual Basic 中:  
  
     [!code-xml[ExpenseIt#2_A](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt/MainWindow.xaml#2_a)]  
  
     或 c\# 中应如下所示:  
  
     [!code-xml[ExpenseIt#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/MainWindow.xaml#2)]  
  
6.  打开 MainWindow.xaml.vb 或 MainWindow.xaml.cs。  
  
     此文件为代码在包含代码以处理事件在 MainWindow.xaml 声明的隐藏文件。  此文件包含 XAML 中定义的窗口的分部类。  
  
7.  如果您使用的是 c\#，请更改 `MainWindow` 类从 <xref:System.Windows.Navigation.NavigationWindow>派生。  
  
     在 Visual Basic 中，那么，当您在 XAML 中更改窗口时，这会自动发生。  
  
     您的代码应如下所示。  
  
     [!code-csharp[ExpenseIt#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/MainWindow.xaml.cs#3)]
     [!code-vb[ExpenseIt#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/MainWindow.xaml.vb#3)]  
  
<a name="add_files_to_the_application"></a>   
## 向应用程序中添加文件  
 在本节中，将添加两页和一个图像。应用程序。  
  
1.  添加新页 \(wpf\)。名为 `ExpenseItHome.xaml`的项。  有关更多信息，请参见 [如何：向 WPF 项目中添加新项](http://msdn.microsoft.com/zh-cn/17e6b238-fc32-4385-98ef-2f66ca09d9ad)。  
  
     此页是显示的第一页，则应用程序启动时。  它显示用户可以选择人员显示一个零用金报销单的人的列表。  
  
2.  打开 ExpenseItHome.xaml。  
  
3.  设置 <xref:System.Windows.Controls.Page.Title%2A> 为 “ExpenseIt \-”。  
  
     您的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 应如下所示在 Visual Basic 中:  
  
     [!code-xml[ExpenseIt#6_A](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseItHome.xaml#6_a)]  
  
     或者在 c\#:  
  
     [!code-xml[ExpenseIt#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt2/ExpenseItHome.xaml#6)]  
  
4.  打开 MainWindow.xaml。  
  
5.  将 <xref:System.Windows.Navigation.NavigationWindow> 的 <xref:System.Windows.Navigation.NavigationWindow.Source%2A> 属性设置为 “ExpenseItHome.xaml”。  
  
     ，当应用程序启动时，它设置 ExpenseItHome.xaml 已打开的第一页。  您的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 应如下所示在 Visual Basic 中:  
  
     [!code-xml[ExpenseIt#7_A](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/MainWindow.xaml#7_a)]  
  
     或者在 c\#:  
  
     [!code-xml[ExpenseIt#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt2/MainWindow.xaml#7)]  
  
6.  添加新页 \(wpf\)。名为 `ExpenseReportPage.xaml`的项。  
  
     此页将显示 ExpenseItHome.xaml 中所选人员的零用金报销单。  
  
7.  打开 ExpenseReportPage.xaml。  
  
8.  设置 <xref:System.Windows.Controls.Page.Title%2A> 为 “ExpenseIt \- 查看 expense”。  
  
     您的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 应如下所示在 Visual Basic 中:  
  
     [!code-xml[ExpenseIt#4_A](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseReportPage.xaml#4_a)]  
  
     或者在 c\#:  
  
     [!code-xml[ExpenseIt#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/ExpenseReportPage.xaml#4)]  
  
9. 打开 ExpenseItHome.xaml.vb 和 ExpenseReportPage.xaml.vb 或打开 ExpenseItHome.xaml.cs。  
  
     当您创建新的页文件时， Visual Studio 会自动创建代码隐藏文件。  这些代码隐藏文件处理响应用户输入的逻辑。  
  
     您的代码应如下所示。  
  
     [!code-csharp[ExpenseIt#2_5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt2/ExpenseItHome.xaml.cs#2_5)]
     [!code-vb[ExpenseIt#2_5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseItHome.xaml.vb#2_5)]  
  
     [!code-csharp[ExpenseIt#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt/ExpenseReportPage.xaml.cs#5)]
     [!code-vb[ExpenseIt#5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt1_A/ExpenseReportPage.xaml.vb#5)]  
  
10. 添加一个名为 watermark.png 的图像添加到项目中。  可以创建自己的图像，也可以从代码示例中复制的文件。  有关更多信息，请参见 [NIB:How to: Add Existing Items to a Project](http://msdn.microsoft.com/zh-cn/15f4cfb7-78ab-457f-9f14-099a25a6a2d3)。  
  
<a name="Build_The_Application"></a>   
## 生成并运行应用程序  
 在本节中，您将生成和运行应用程序。  
  
1.  生成并运行该应用程序通过按 F5 或选择 **启动调试** 从 **调试** 菜单。  
  
     下面的插图显示了具有 <xref:System.Windows.Navigation.NavigationWindow> 按钮的应用程序。  
  
     ![ExpenseIt 示例屏幕快照](../../../../docs/framework/wpf/getting-started/media/gettingstartedfigure1.png "GettingStartedFigure1")  
  
2.  关闭应用程序返回到 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)]。  
  
<a name="Add_Layout"></a>   
## 创建布局  
 ，当 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 调整的大小时，布局提供一个有序的方式将 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素，并管理这些元素的大小和位置。  使用以下格式控件之一通常创建一个布局:  
  
-   <xref:System.Windows.Controls.Canvas>  
  
-   <xref:System.Windows.Controls.DockPanel>  
  
-   <xref:System.Windows.Controls.Grid>  
  
-   <xref:System.Windows.Controls.StackPanel>  
  
-   <xref:System.Windows.Controls.VirtualizingStackPanel>  
  
-   <xref:System.Windows.Controls.WrapPanel>  
  
 这些窗体控件中的每一个支持布局的一种特殊类型的子元素的。  ExpenseIt 页面可以调整大小，并且，每页都有垂直同其他元素水平排列和的元素。  因此， <xref:System.Windows.Controls.Grid> 是应用程序的理想布局元素。  
  
> [!NOTE]
>  有关 <xref:System.Windows.Controls.Panel> 元素的更多信息，请 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)参见。  有关布局的更多信息，请 [布局](../../../../docs/framework/wpf/advanced/layout.md)参见。  
  
 在本节中，您将三行和 10 像素的边距创建一个列表中添加列和行定义。 <xref:System.Windows.Controls.Grid> 在 ExpenseItHome.xaml 上。  
  
1.  打开 ExpenseItHome.xaml。  
  
2.  将 <xref:System.Windows.Controls.Grid> 元素的 <xref:System.Windows.FrameworkElement.Margin%2A> 属性设置为 “对应于左、上，右箭头和下边距的 10,0,10,10 "。  
  
3.  将 <xref:System.Windows.Controls.Grid> 标记之间添加以下 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 创建行和列定义。  
  
     [!code-xml[ExpenseIt#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt3/ExpenseItHome.xaml#8)]  
  
     两行 <xref:System.Windows.Controls.RowDefinition.Height%2A> 设置为表示的 <xref:System.Windows.GridLength.Auto%2A> 行将位于内容调整大小的基础在行。  默认值 <xref:System.Windows.Controls.RowDefinition.Height%2A> 是调整大小， <xref:System.Windows.GridUnitType> ，这意味着行将为可用空间的加权比例。  例如，如果两个行中的高度均为 “\*”，则它们各自的将为可用空间的一半的一个高度。  
  
     您的 <xref:System.Windows.Controls.Grid> 现在应类似于以下 XAML:  
  
     [!code-xml[ExpenseIt#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt3/ExpenseItHome.xaml#9)]  
  
<a name="Add_Controls"></a>   
## 添加控件  
 在本节中，主页将更新以 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 显示用户可以选择显示选定人员的零用金报销单方的列表。  控件是一个允许用户与应用程序交互的 UI 对象。  有关更多信息，请参见 [控件](../../../../docs/framework/wpf/controls/index.md)。  
  
 若要创建此 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，将以下元素添加到 ExpenseItHome.xaml:  
  
-   <xref:System.Windows.Controls.ListBox> \(用于人员列表\)。  
  
-   <xref:System.Windows.Controls.Label> \(用于列表标题\)。  
  
-   <xref:System.Windows.Controls.Button> \(单击可查看列表中选定的人员的零用金报销单。  
  
 每个行放置 <xref:System.Windows.Controls.Grid> 通过将 <xref:System.Windows.Controls.Grid.Row%2A?displayProperty=fullName> 附加属性。  有关附加属性的更多信息，请参见 [附加属性概述](../../../../docs/framework/wpf/advanced/attached-properties-overview.md)。  
  
1.  打开 ExpenseItHome.xaml。  
  
2.  将 <xref:System.Windows.Controls.Grid> 标记之间添加以下 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]。  
  
     [!code-xml[ExpenseIt#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt4/ExpenseItHome.xaml#10)]  
  
3.  生成并运行应用程序。  
  
 下图显示了 XAML 中创建的本节中的控件。  
  
 ![ExpenseIt 示例屏幕快照](../../../../docs/framework/wpf/getting-started/media/gettingstartedfigure2.png "GettingStartedFigure2")  
  
<a name="Add_an_Image"></a>   
## 添加图像和标题  
 在本节中，主页 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 更新为包含图像和页标题。  
  
1.  打开 ExpenseItHome.xaml。  
  
2.  将另一列添加到 <xref:System.Windows.Controls.Grid.ColumnDefinitions%2A> 和 230 像素内置的 <xref:System.Windows.Controls.ColumnDefinition.Width%2A> 。  
  
     [!code-xml[ExpenseIt#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#11)]  
  
3.  向中添加另一行 <xref:System.Windows.Controls.Grid.RowDefinitions%2A>。  
  
     [!code-xml[ExpenseIt#11b](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#11b)]  
  
4.  将一个控件移动到第二列通过将 <xref:System.Windows.Controls.Grid.Column%2A?displayProperty=fullName> 到 1。  通过添加 <xref:System.Windows.Controls.Grid.Row%2A?displayProperty=fullName> 移一行下的每个控件， 1。  
  
     [!code-xml[ExpenseIt#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#12)]  
  
5.  设置 <xref:System.Windows.Controls.Grid> 的 <xref:System.Windows.Controls.Panel.Background%2A> 为 watermark.png 图像文件。  
  
     [!code-xml[ExpenseIt#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#14)]  
  
6.  在 <xref:System.Windows.Controls.Border>之前，添加一个内容 “view expense report” <xref:System.Windows.Controls.Label> 是页的标题。  
  
     [!code-xml[ExpenseIt#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt5/ExpenseItHome.xaml#13)]  
  
7.  生成并运行应用程序。  
  
 下图显示本节的结果。  
  
 ![ExpenseIt 示例屏幕快照](../../../../docs/framework/wpf/getting-started/media/gettingstartedfigure3.png "GettingStartedFigure3")  
  
<a name="Add_Code_to_Process_Events"></a>   
## 添加代码以处理事件  
  
1.  打开 ExpenseItHome.xaml。  
  
2.  添加一个 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件处理程序。 <xref:System.Windows.Controls.Button> 元素。  有关更多信息，请参见 [如何：创建简单的事件处理程序](http://msdn.microsoft.com/zh-cn/b1456e07-9dec-4354-99cf-18666b64f480)。  
  
     [!code-xml[ExpenseIt#15](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt6/ExpenseItHome.xaml#15)]  
  
3.  打开 ExpenseItHome.xaml.vb 或 ExpenseItHome.xaml.cs。  
  
4.  将以下代码添加到 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件处理程序，使窗口导航到 ExpenseReportPage.xaml 文件。  
  
     [!code-csharp[ExpenseIt#16](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt6/ExpenseItHome.xaml.cs#16)]
     [!code-vb[ExpenseIt#16](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt6/ExpenseItHome.xaml.vb#16)]  
  
<a name="Create_the_UI_for_Pane2"></a>   
## 创建 ExpenseReportPage 的 UI  
 ExpenseReportPage.xaml 显示 ExpenseItHome.xaml 中所选人员的零用金报销单。  本节为 ExpenseReportPage.xaml 添加控件和创建的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 。  本节还添加背景色和填充颜色为各个 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素。  
  
1.  打开 ExpenseReportPage.xaml。  
  
2.  将 <xref:System.Windows.Controls.Grid> 标记之间添加以下 XAML。  
  
     此 UI 类似于在 ExpenseItHome.xaml 上创建的 UI，只不过报告数据在 <xref:System.Windows.Controls.DataGrid>显示。  
  
     [!code-xml[ExpenseIt#17](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt6/ExpenseReportPage.xaml#17)]  
  
3.  生成并运行应用程序。  
  
    > [!NOTE]
    >  如果收到错误未找到 <xref:System.Windows.Controls.DataGrid> 或不存在，确保，您的项目以 .NET framework 4。  有关更多信息，请参见 [如何：面向 .NET Framework 的某个版本](../Topic/How%20to:%20Target%20a%20Version%20of%20the%20.NET%20Framework.md)。  
  
4.  单击 **视图** 按钮。  
  
     零用金报销单页。  
  
 下图显示 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素添加到 ExpenseReportPage.xaml。  通知向后导航按钮均处于启用状态。  
  
 ![ExpenseIt 示例屏幕快照](../../../../docs/framework/wpf/getting-started/media/gettingstartedfigure4.png "GettingStartedFigure4")  
  
<a name="Add_Code_to_Style_a_Control"></a>   
## 样式控件  
 各个元素的外观通常可以是对于所有元素的相同的输入 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 使用样式使外观可重用在多个元素。  样式的可重用性有助于简化 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 创建和管理。  有关样式的更多信息，请 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)参见。  此节替换在使用样式前面的步骤中定义的每个元素的属性。  
  
1.  打开 Application.xaml 或 App.xaml。  
  
2.  将 <xref:System.Windows.Application.Resources%2A?displayProperty=fullName> 标记之间添加以下 XAML:  
  
     [!code-xml[ExpenseIt#18](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt7/App.xaml#18)]  
  
     此 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 添加以下样式:  
  
    -   `headerTextStyle`:设置页标题 <xref:System.Windows.Controls.Label>。  
  
    -   `labelStyle`:格式 <xref:System.Windows.Controls.Label> 控件。  
  
    -   `columnHeaderStyle`:格式 <xref:System.Windows.Controls.Primitives.DataGridColumnHeader>。  
  
    -   `listHeaderStyle`:设置列表标题 <xref:System.Windows.Controls.Border> 控件。  
  
    -   `listHeaderTextStyle`:设置列表标题 <xref:System.Windows.Controls.Label>。  
  
    -   `buttonStyle`:设置 ExpenseItHome.xaml 中的 <xref:System.Windows.Controls.Button> 。  
  
     通知样式是 <xref:System.Windows.Application.Resources%2A?displayProperty=fullName> 属性元素的资源和子项。  这里，样式将应用于应用程序的所有元素。  有关使用的示例在 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 应用程序的资源，请参见 [使用应用程序资源](../../../../docs/framework/wpf/advanced/how-to-use-application-resources.md)。  
  
3.  打开 ExpenseItHome.xaml。  
  
4.  用下面的 XAML 替换所有内容。 <xref:System.Windows.Controls.Grid> 元素之间。  
  
     [!code-xml[ExpenseIt#19](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt7/ExpenseItHome.xaml#19)]  
  
     定义每个控件中查找例如 <xref:System.Windows.VerticalAlignment> 和 <xref:System.Windows.Media.FontFamily> 应用样式移除的属性并替换。  例如， `headerTextStyle` 适用于 “view expense report” <xref:System.Windows.Controls.Label>。  
  
5.  打开 ExpenseReportPage.xaml。  
  
6.  用下面的 XAML 替换所有内容。 <xref:System.Windows.Controls.Grid> 元素之间。  
  
     [!code-xml[ExpenseIt#20](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt7/ExpenseReportPage.xaml#20)]  
  
     这将添加样式添加到 <xref:System.Windows.Controls.Label> 和 <xref:System.Windows.Controls.Border> 元素。  
  
7.  生成并运行应用程序。  
  
     在添加本节中的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 后，应用程序看上去与在中使用样式更新之前的。  
  
<a name="Bind_Data_to_a_Control"></a>   
## 将数据绑定到控件  
 在本节中，将创建绑定到各种控件的 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 数据。  
  
1.  打开 ExpenseItHome.xaml。  
  
2.  在打开的 <xref:System.Windows.Controls.Grid> 元素后，添加包含每个人员的数据的下面的 XAML 创建 <xref:System.Windows.Data.XmlDataProvider> 。  
  
     数据创建为 <xref:System.Windows.Controls.Grid> 资源。  这通常将以文件形式加载，但是，该数据为简单起见将添加在内联。  
  
     [!code-xml[ExpenseIt#21](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml#21)]  
    [!code-xml[ExpenseIt#23](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml#23)]  
    [!code-xml[ExpenseIt#22](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml#22)]  
  
3.  在 <xref:System.Windows.Controls.Grid> 资源，添加以下 <xref:System.Windows.DataTemplate>，定义如何显示在 <xref:System.Windows.Controls.ListBox>的数据。  有关数据模板的更多信息，请 [数据模板化概述](../../../../docs/framework/wpf/data/data-templating-overview.md)参见。  
  
     [!code-xml[ExpenseIt#21](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml#21)]  
    [!code-xml[ExpenseIt#24](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml#24)]  
    [!code-xml[ExpenseIt#22](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml#22)]  
  
4.  用下面的 XAML 替换现有 <xref:System.Windows.Controls.ListBox> 。  
  
     [!code-xml[ExpenseIt#25](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml#25)]  
  
     此 XAML 将 <xref:System.Windows.Controls.ListBox> 的 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 属性设置为数据源并应用数据模板作为 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>。  
  
<a name="Connect_Data_to_Controls"></a>   
## 将数据连接到控件  
 本节中，您将编写检索在人员列表中选择 ExpenseItHome.xaml 页的代码，并通过其对 `ExpenseReportPage` 构造函数中实例化时。  `ExpenseReportPage` 将其可通过项目中的数据上下文，正是在 ExpenseReportPage.xaml 定义的控件将绑定。  
  
1.  打开 ExpenseReportPage.xaml.vb 或 ExpenseReportPage.xaml.cs。  
  
2.  添加获取对象的构造函数，因此可以传递所选人员的零用金报销单数据。  
  
     [!code-csharp[ExpenseIt#26](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseReportPage.xaml.cs#26)]
     [!code-vb[ExpenseIt#26](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt8/ExpenseReportPage.xaml.vb#26)]  
  
3.  打开 ExpenseItHome.xaml.vb 或 ExpenseItHome.xaml.cs。  
  
4.  更改 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件处理程序调用传递所选人员的零用金报销单数据的函数。  
  
     [!code-csharp[ExpenseIt#27](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt8/ExpenseItHome.xaml.cs#27)]
     [!code-vb[ExpenseIt#27](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ExpenseIt/VB/ExpenseIt8/ExpenseItHome.xaml.vb#27)]  
  
<a name="Add_Style_to_Data"></a>   
## 样式使用数据模板的数据  
 通过使用数据模板，在本节中，您在每个项目的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 在数据绑定列表。  
  
1.  打开 ExpenseReportPage.xaml。  
  
2.  将 “名称”和 “部门” <xref:System.Windows.Controls.Label> 元素的内容绑定到相应的数据源属性。  有关数据绑定的更多信息，请 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)参见。  
  
     [!code-xml[ExpenseIt#31](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseReportPage.xaml#31)]  
  
3.  在打开的 <xref:System.Windows.Controls.Grid> 元素后，添加以下数据模板，定义如何显示零用金报销单数据。  
  
     [!code-xml[ExpenseIt#30](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseReportPage.xaml#30)]  
  
4.  将模板应用于显示零用金报销单数据的 <xref:System.Windows.Controls.DataGrid> 列。  
  
     [!code-xml[ExpenseIt#32](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ExpenseIt/CSharp/ExpenseIt9/ExpenseReportPage.xaml#32)]  
  
5.  生成并运行应用程序。  
  
6.  选择 person 然后单击 **视图** 按钮。  
  
 下图显示 ExpenseIt 应用程序的两个页使用控件、布局、样式、数据绑定和数据模板。  
  
 ![ExpenseIt 示例屏幕快照](../../../../docs/framework/wpf/getting-started/media/gettingstartedfigure5.png "GettingStartedFigure5")  
  
<a name="Best_Practices"></a>   
## 最佳做法  
 此示例演示 WPF 的特定功能，因此，因此，未遵循应用程序开发的最佳做法。  有关 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 应用程序开发的最佳做法的全面介绍，请相应参见以下主题:  
  
-   辅助功能 \- [辅助功能最佳方案](../../../../docs/framework/ui-automation/accessibility-best-practices.md)  
  
-   安全 \- [安全性](../../../../docs/framework/wpf/security-wpf.md)  
  
-   本地化 \- [WPF 全球化和本地化概述](../../../../docs/framework/wpf/advanced/wpf-globalization-and-localization-overview.md)  
  
-   性能 \- [优化 WPF 应用程序性能](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)  
  
<a name="Whats_Next"></a>   
## 接下来的内容  
 使用 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]，现在有多种技术在您的进程中创建 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 。  现在应该对的清楚地了解的基本构造块一个数据 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] 应用程序。  本主题并未涵盖所有信息的，因此，不过您现在还具有特定的意义可以在本主题中的方法之外自己发现可能性。  
  
 有关 WPF 体系结构和编程模型的更多信息，请参见以下主题:  
  
-   [WPF 体系结构](../../../../docs/framework/wpf/advanced/wpf-architecture.md)  
  
-   [XAML 概述 \(WPF\)](../../../../docs/framework/wpf/advanced/xaml-overview-wpf.md)  
  
-   [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)  
  
-   [布局](../../../../docs/framework/wpf/advanced/layout.md)  
  
 有关创建应用程序的更多信息，请参见以下主题:  
  
-   [应用程序开发](../../../../docs/framework/wpf/app-development/index.md)  
  
-   [控件](../../../../docs/framework/wpf/controls/index.md)  
  
-   [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)  
  
-   [图形和多媒体](../../../../docs/framework/wpf/graphics-multimedia/index.md)  
  
-   [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)  
  
## 请参阅  
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)   
 [数据模板化概述](../../../../docs/framework/wpf/data/data-templating-overview.md)   
 [生成 WPF 应用程序](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md)   
 [样式和模板](../../../../docs/framework/wpf/controls/styles-and-templates.md)