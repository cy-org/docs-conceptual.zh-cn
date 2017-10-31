---
title: "WPF Windows 概述 | Microsoft Docs"
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
  - "应用程序, Hosting — 承载"
  - "内容, 显示"
  - "内容, 通过程序代码显示"
  - "内容, 通过 XAML 显示"
  - "创建, 窗口"
  - "对话框"
  - "显示内容"
  - "通过程序代码显示内容"
  - "显示 XAML 页"
  - "事件"
  - "Hosting — 承载, 应用程序"
  - "管理窗口"
  - "有模式对话框"
  - "模式窗口"
  - "NavigationWindow 对象"
  - "Page 对象"
  - "程序代码, 显示内容"
  - "窗口事件"
  - "窗口管理"
  - "窗口对象"
  - "窗口"
  - "XAML 页面, 显示"
  - "XAML, 显示内容"
ms.assetid: 737d04ec-8861-46c3-8d44-fa11d3528d23
caps.latest.revision: 65
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 60
---
# WPF Windows 概述
用户通过窗口与 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 独立应用程序进行交互。  窗口的主要用途是承载可视化数据并使用户可以与数据进行交互的内容。独立 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序使用 <xref:System.Windows.Window> 类来提供它们自己的窗口。  本主题首先介绍 <xref:System.Windows.Window>，然后介绍在独立应用程序中创建和管理窗口的基础知识。  
  
> [!NOTE]
>  浏览器承载的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序（包括 [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] 和松散[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 页）不提供它们自己的窗口。  而是承载于 [!INCLUDE[TLA#tla_iegeneric](../../../../includes/tlasharptla-iegeneric-md.md)] 提供的窗口中。  请参见 [WPF XAML 浏览器应用程序概述](../../../../docs/framework/wpf/app-development/wpf-xaml-browser-applications-overview.md)。  
  
   
  
<a name="TheWindowClass"></a>   
## 窗口类  
 下图显示了窗口的构成部分。  
  
 ![窗口元素](../../../../docs/framework/wpf/app-development/media/windowoverviewfigure1.PNG "WindowOverviewFigure1")  
  
 窗口分为两个区域：非工作区和工作区。  
  
 窗口的非工作区由 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 实现，它包括大多数窗口所共有的窗口部分，其中包括：  
  
-   边框。  
  
-   标题栏。  
  
-   图标。  
  
-   “最小化”、“最大化”和“还原”按钮。  
  
-   “关闭”按钮。  
  
-   “系统”菜单，其中包含允许用户最小化、最大化、还原、移动和关闭窗口以及调整窗口大小的菜单项。  
  
 窗口的工作区是窗口的非工作区内部的区域，开发人员使用它来添加应用程序特定的内容，如菜单栏、工具栏和控件。  
  
 在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中，窗口通过 <xref:System.Windows.Window> 类进行封装，使用该类可以执行下面的操作：  
  
-   显示窗口。  
  
-   配置窗口的大小、位置和外观。  
  
-   承载应用程序特定的内容。  
  
-   管理窗口的生存期。  
  
<a name="DefiningAWindow"></a>   
## 实现窗口  
 典型窗口的实现既包括外观又包括行为，其中外观定义用户看到的窗口的样子，而行为则定义在用户与窗口进行交互时窗口的运行方式。  在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中，可以使用代码或 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 标记来实现窗口的外观和行为。  
  
 但一般来说，窗口的外观使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 标记来实现，而行为则使用代码隐藏来实现，如下面的示例所示。  
  
 [!code-xml[WindowsOverviewSnippets#MarkupAndCodeBehindWindowMARKUP](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/MarkupAndCodeBehindWindow.xaml#markupandcodebehindwindowmarkup)]  
  
 [!code-csharp[WindowsOverviewSnippets#MarkupAndCodeBehindWindowCODEBEHIND](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/MarkupAndCodeBehindWindow.xaml.cs#markupandcodebehindwindowcodebehind)]
 [!code-vb[WindowsOverviewSnippets#MarkupAndCodeBehindWindowCODEBEHIND](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WindowsOverviewSnippets/VisualBasic/MarkupAndCodeBehindWindow.xaml.vb#markupandcodebehindwindowcodebehind)]  
  
 为了使 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 标记文件和代码隐藏文件配合工作，需要达到下面的条件：  
  
-   在标记中，`Window` 元素必须包含 `x:Class` 特性。  生成应用程序时，标记文件中存在的 `x:Class` 将使 [!INCLUDE[TLA#tla_msbuild](../../../../includes/tlasharptla-msbuild-md.md)] 生成一个从 <xref:System.Windows.Window> 派生的 `partial` 类，并且该类的名称是由 `x:Class` 特性指定的。  这要求添加 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 架构的 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 命名空间声明 \(`xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`\)。  生成的 `partial` 类实现了 `InitializeComponent` 方法，调用此方法可注册事件并设置在标记中实现的属性。  
  
-   在代码隐藏中，该类必须是 `partial` 类，其名称必须与标记中 `x:Class` 特性指定的名称相同，且必须派生自 <xref:System.Windows.Window>。  这样，代码隐藏文件就与应用程序生成时为标记文件生成的 `partial` 类相关联（请参见[生成 WPF 应用程序](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md)）。  
  
-   在代码隐藏中，<xref:System.Windows.Window> 类必须实现调用 `InitializeComponent` 方法的构造函数。  标记文件的已生成的 `partial` 类实现 `InitializeComponent`，以便注册事件和设置在标记中定义的属性。  
  
> [!NOTE]
>  在使用 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 将新 <xref:System.Windows.Window> 添加到项目时，<xref:System.Windows.Window> 是同时使用标记和代码隐藏实现的，并且它包括了必要的配置来创建此处所述的标记文件和代码隐藏文件之间的关联。  
  
 进行此配置之后，您可以集中精力在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 标记中定义窗口的外观，并在代码隐藏中实现窗口的行为。  下面的示例显示一个包含按钮的窗口（在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 标记中实现）以及该按钮的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件的事件处理程序（在代码隐藏中实现）。  
  
 [!code-xml[WindowsOverviewWindowWithButtonSnippets#MarkupAndCodeBehindWindowMARKUP](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewWindowWithButtonSnippets/CSharp/MarkupAndCodeBehindWindow.xaml#markupandcodebehindwindowmarkup)]  
  
 [!code-csharp[WindowsOverviewWindowWithButtonSnippets#MarkupAndCodeBehindWindowCODEBEHIND](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewWindowWithButtonSnippets/CSharp/MarkupAndCodeBehindWindow.xaml.cs#markupandcodebehindwindowcodebehind)]
 [!code-vb[WindowsOverviewWindowWithButtonSnippets#MarkupAndCodeBehindWindowCODEBEHIND](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WindowsOverviewWindowWithButtonSnippets/VisualBasic/MarkupAndCodeBehindWindow.xaml.vb#markupandcodebehindwindowcodebehind)]  
  
<a name="ConfiguringWindowForMSBuild"></a>   
## 为 MSBuild 配置窗口定义  
 实现窗口的方式决定了为 [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] 配置窗口的方式。  对于使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 标记和代码隐藏定义的窗口：  
  
-   [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 标记文件配置为 [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] `Page` 项。  
  
-   代码隐藏文件配置为 [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] `Compile` 项。  
  
 这将在下面的 [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] 项目文件中显示。  
  
```  
<Project ... xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    ...  
    <Page Include="MarkupAndCodeBehindWindow.xaml" />  
    <Compile Include=" MarkupAndCodeBehindWindow.xaml.cs" />  
    ...  
</Project>  
```  
  
 有关生成 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序的信息，请参见[生成 WPF 应用程序](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md)。  
  
<a name="WindowLifetime"></a>   
## 窗口生存期  
 和所有类一样，窗口也有生存期，在第一次实例化窗口时生存期开始，然后就可以打开、激活和停用窗口，直到最终关闭窗口。  
  
   
  
<a name="Opening_a_Window"></a>   
### 打开窗口  
 若要打开窗口，首先应创建一个窗口实例，下面的示例演示此操作。  
  
 [!code-xml[WindowsOverviewStartupEventSnippets#AppMARKUP](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewStartupEventSnippets/CSharp/App.xaml#appmarkup)]  
  
 [!code-csharp[WindowsOverviewStartupEventSnippets#AppCODEBEHIND](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewStartupEventSnippets/CSharp/App.xaml.cs#appcodebehind)]  
  
 在此示例中，在应用程序启动时（在引发 <xref:System.Windows.Application.Startup> 事件时发生），`MarkupAndCodeBehindWindow` 进行实例化。  
  
 在实例化窗口时，指向该窗口的引用会自动添加到由 <xref:System.Windows.Application> 对象管理的窗口列表中（请参见 <xref:System.Windows.Application.Windows%2A?displayProperty=fullName>）。  另外，默认情况下，<xref:System.Windows.Application> 会将实例化的第一个窗口设置为主应用程序窗口（请参见 <xref:System.Windows.Application.MainWindow%2A?displayProperty=fullName>）。  
  
 最后，通过调用 <xref:System.Windows.Window.Show%2A> 方法打开窗口；结果如下图所示。  
  
 ![通过调用 Window.Show 而打开的窗口](../../../../docs/framework/wpf/app-development/media/windowoverviewfigure8.png "WindowOverviewFigure8")  
  
 通过调用 <xref:System.Windows.Window.Show%2A> 打开的窗口是无模式窗口，这意味着应用程序所运行的模式允许用户在同一个应用程序中激活其他窗口。  
  
> [!NOTE]
>  调用 <xref:System.Windows.Window.ShowDialog%2A> 来模式打开窗口，例如对话框。  有关更多信息，请参见[对话框概述](../../../../docs/framework/wpf/app-development/dialog-boxes-overview.md)。  
  
 当调用 <xref:System.Windows.Window.Show%2A> 时，在显示窗口以建立让窗口可以接收用户输入的基础结构之前，窗口会执行初始化工作。  当初始化窗口时，将引发 <xref:System.Windows.Window.SourceInitialized> 事件并显示窗口。  
  
 作为一种快捷方式，可以设置 <xref:System.Windows.Application.StartupUri%2A> 以指定在应用程序启动时自动打开的第一个窗口。  
  
 [!code-xml[WindowsOverviewSnippets#ApplicationStartupUriMARKUP](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/App.xaml#applicationstartupurimarkup)]  
  
 当应用程序启动时，<xref:System.Windows.Application.StartupUri%2A> 的值所指定的窗口会无模式地打开；在内部，则通过调用 <xref:System.Windows.Window.Show%2A> 方法来打开窗口。  
  
<a name="Ownership"></a>   
#### 窗口所属权  
 使用 <xref:System.Windows.Window.Show%2A> 方法打开的窗口与创建它的窗口之间没有隐式关系；用户可以与这两个窗口分别进行独立的交互，这意味着这两个窗口都可以执行下面的操作：  
  
-   覆盖另一个窗口（除非其中一个窗口的 <xref:System.Windows.Window.Topmost%2A> 属性设置为 `true`）。  
  
-   在不影响另一个窗口的情况下，最小化、最大化和还原一个窗口。  
  
 某些窗口要求与打开它们的窗口之间保持某种关系。  例如，[!INCLUDE[TLA#tla_ide](../../../../includes/tlasharptla-ide-md.md)] 应用程序可能会打开属性窗口和工具窗口，而这些窗口的典型行为是覆盖创建它们的窗口。  此外，此类窗口应始终与创建它们的窗口协调一致地进行关闭、最小化、最大化和还原。  可以通过让一个窗口拥有另一个窗口来建立这种关系，也可以通过使用对所有者窗口的引用来设置附属窗口的 <xref:System.Windows.Window.Owner%2A> 属性，以建立这种关系。  这将在下面的示例中显示。  
  
 [!code-csharp[WindowOwnerOwnedWindowsSnippets#SetWindowOwnerCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowOwnerOwnedWindowsSnippets/CSharp/MainWindow.xaml.cs#setwindowownercode)]
 [!code-vb[WindowOwnerOwnedWindowsSnippets#SetWindowOwnerCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WindowOwnerOwnedWindowsSnippets/visualbasic/mainwindow.xaml.vb#setwindowownercode)]  
  
 建立了所属权之后：  
  
-   附属窗口可以通过检查 <xref:System.Windows.Window.Owner%2A> 属性的值来引用它的所有者窗口。  
  
-   所有者窗口可以通过检查 <xref:System.Windows.Window.OwnedWindows%2A> 属性的值来发现它拥有的全部窗口。  
  
<a name="Preventing"></a>   
#### 防止窗口激活  
 有些情况下，不应在显示窗口时将其激活，例如 Internet Messenger 风格的应用程序的对话窗口或电子邮件应用程序的通知窗口。  
  
 如果应用程序具有不应在显示时被激活的窗口，可以在首次调用 <xref:System.Windows.Window.Show%2A> 方法之前将其 <xref:System.Windows.Window.ShowActivated%2A> 属性设置为 `false`。  这样：  
  
-   窗口便不会被激活。  
  
-   也不会引发窗口的 <xref:System.Windows.Window.Activated> 事件。  
  
-   当前激活的窗口保持激活状态。  
  
 但是，只要用户通过单击客户端或非客户端区域激活了窗口，窗口就会变为激活状态。  在这种情况下：  
  
-   窗口被激活。  
  
-   引发窗口的 <xref:System.Windows.Window.Activated> 事件。  
  
-   停用以前激活的窗口。  
  
-   随后作为对用户操作的响应，如期引发窗口的 <xref:System.Windows.Window.Deactivated> 和 <xref:System.Windows.Window.Activated> 事件。  
  
<a name="Window_Activation"></a>   
### 窗口激活  
 在首次打开一个窗口时，它便成为活动窗口（除非是在 <xref:System.Windows.Window.ShowActivated%2A> 设置为 `false` 的情况下显示）。  活动窗口是当前正在捕获用户输入（例如，键击和鼠标单击）的窗口。  当窗口变为活动窗口时，它会引发 <xref:System.Windows.Window.Activated> 事件。  
  
> [!NOTE]
>  当第一次打开窗口时，只有在引发了 <xref:System.Windows.Window.Activated> 事件之后，才会引发 <xref:System.Windows.FrameworkElement.Loaded> 和 <xref:System.Windows.Window.ContentRendered> 事件。  记住这一点，在引发 <xref:System.Windows.Window.ContentRendered> 时，便可认为窗口已打开。  
  
 窗口变为活动窗口之后，用户可以在同一个应用程序中激活其他窗口，还可以激活其他应用程序。  当这种情况出现时，当前的活动窗口将停用，并引发 <xref:System.Windows.Window.Deactivated> 事件。  同样，当用户选择当前停用的窗口时，该窗口会再次变成活动窗口并引发 <xref:System.Windows.Window.Activated>。  
  
 处理 <xref:System.Windows.Window.Activated> 和 <xref:System.Windows.Window.Deactivated> 的一个常见原因是为了启用和禁用只有在窗口活动时才能够运行的功能。  例如，某些窗口显示的交互式内容需要持续的用户输入或需要用户时刻注意，包括游戏和视频播放机。  下面的示例是一个简化的视频播放机，演示如何处理 <xref:System.Windows.Window.Activated> 和 <xref:System.Windows.Window.Deactivated> 以实现此行为。  
  
 [!code-xml[WindowsOverviewSnippets#ActivationDeactivationMARKUP](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/CustomMediaPlayerWindow.xaml#activationdeactivationmarkup)]  
  
 [!code-csharp[WindowsOverviewSnippets#ActivationDeactivationCODEBEHIND](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/CustomMediaPlayerWindow.xaml.cs#activationdeactivationcodebehind)]
 [!code-vb[WindowsOverviewSnippets#ActivationDeactivationCODEBEHIND](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WindowsOverviewSnippets/VisualBasic/CustomMediaPlayerWindow.xaml.vb#activationdeactivationcodebehind)]  
  
 其他类型的应用程序在窗口停用时可能仍会在后台运行代码。  例如，当用户使用其他应用程序时，邮件客户端可能会继续轮询邮件服务器。  这种类型的应用程序通常会在主窗口停用时提供不同的或其他的行为。  对于邮件程序，这可能意味着将新邮件项添加到收件箱并将通知图标添加到系统任务栏。  只有当邮件窗口不活动时，才需要显示通知图标，可以通过检查 <xref:System.Windows.Window.IsActive%2A> 属性来确定窗口是否不活动。  
  
 如果后台任务完成，窗口可能需要通过调用 <xref:System.Windows.Window.Activate%2A> 方法来更紧急地通知用户。  如果在调用 <xref:System.Windows.Window.Activate%2A> 时用户正在与另一个激活的应用程序交互，则窗口的任务栏按钮会闪烁。  如果用户正在与当前应用程序交互，则调用 <xref:System.Windows.Window.Activate%2A> 会将窗口置于前台。  
  
> [!NOTE]
>  可以使用 <xref:System.Windows.Application.Activated?displayProperty=fullName> 和 <xref:System.Windows.Application.Deactivated?displayProperty=fullName> 事件处理应用程序范围的激活。  
  
<a name="Closing_a_Window"></a>   
### 关闭窗口  
 当用户关闭窗口时，窗口的生命便开始走向终结。  可以使用非工作区中的元素来关闭窗口，这些元素包括：  
  
-   **“系统”**菜单的**“关闭”**项。  
  
-   按 Alt \+ F4。  
  
-   按**“关闭”**按钮。  
  
 可以为工作区提供关闭窗口的附加机制，其中比较常用的包括：  
  
-   **“文件”**菜单中的**“退出”**项，通常用于主应用程序窗口。  
  
-   **“文件”**菜单中的**“关闭”**项，通常出现在辅助应用程序窗口中。  
  
-   **“取消”**按钮，通常出现在模式对话框中。  
  
-   **“关闭”**按钮，通常出现在无模式对话框中。  
  
 若要响应这些自定义机制中某个机制来关闭窗口，需要调用 <xref:System.Windows.Window.Close%2A> 方法。  下面的示例实现通过选择**“文件”**菜单上的**“退出”**来关闭窗口的功能。  
  
 [!code-xml[WindowsOverviewSnippets#WindowWithFileExitMARKUP](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowWithFileExit.xaml#windowwithfileexitmarkup)]  
  
 [!code-csharp[WindowsOverviewSnippets#WindowWithFileExitCODEBEHIND](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowWithFileExit.xaml.cs#windowwithfileexitcodebehind)]
 [!code-vb[WindowsOverviewSnippets#WindowWithFileExitCODEBEHIND](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WindowsOverviewSnippets/VisualBasic/WindowWithFileExit.xaml.vb#windowwithfileexitcodebehind)]  
  
 当窗口关闭时，它会引发两个事件：<xref:System.Windows.Window.Closing> 和 <xref:System.Windows.Window.Closed>。  
  
 <xref:System.Windows.Window.Closing> 在窗口关闭之前引发，它提供一种机制，可以通过这种机制来阻止窗口关闭。  阻止窗口关闭的一个常见原因是窗口内容包含了已修改数据。  在这种情况下，可以处理 <xref:System.Windows.Window.Closing> 事件来确定数据是否已更新，如果已更新，则询问用户是继续关闭窗口而不保存数据，还是取消窗口关闭。  下面的示例显示处理 <xref:System.Windows.Window.Closing> 的关键方面。  
  
 [!code-csharp[WindowClosingSnippets#WindowClosingCODEBEHIND1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowClosingSnippets/CSharp/DataWindow.xaml.cs#windowclosingcodebehind1)]
 [!code-vb[WindowClosingSnippets#WindowClosingCODEBEHIND1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WindowClosingSnippets/visualbasic/datawindow.xaml.vb#windowclosingcodebehind1)]  
[!code-csharp[WindowClosingSnippets#WindowClosingCODEBEHIND2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowClosingSnippets/CSharp/DataWindow.xaml.cs#windowclosingcodebehind2)]
[!code-vb[WindowClosingSnippets#WindowClosingCODEBEHIND2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WindowClosingSnippets/visualbasic/datawindow.xaml.vb#windowclosingcodebehind2)]  
  
 向 <xref:System.Windows.Window.Closing> 事件处理程序传递一个 <xref:System.ComponentModel.CancelEventArgs>，该参数实现 `Boolean` <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 属性，将该属性设置为 `true` 可以阻止窗口关闭。  
  
 如果未处理 <xref:System.Windows.Window.Closing>，或者处理但未取消，则窗口将关闭。  在窗口真正关闭之前，会引发 <xref:System.Windows.Window.Closed>。  这时无法阻止窗口关闭。  
  
> [!NOTE]
>  可以将应用程序配置为当主应用程序窗口关闭（请参见 <xref:System.Windows.Application.MainWindow%2A>）或最后一个窗口关闭时自动关闭。  有关详细信息，请参见 <xref:System.Windows.Application.ShutdownMode%2A>。  
  
 尽管可以通过非工作区和工作区中提供的机制来显式关闭窗口，但窗口也可能会由于应用程序或 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 的其他部分中的行为而隐式关闭，这些行为包括：  
  
-   用户注销或关闭 [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)]。  
  
-   窗口的所有者关闭（请参见 <xref:System.Windows.Window.Owner%2A>）。  
  
-   主应用程序窗口关闭并且 <xref:System.Windows.Application.ShutdownMode%2A> 为 <xref:System.Windows.ShutdownMode>。  
  
-   调用 <xref:System.Windows.Application.Shutdown%2A>。  
  
> [!NOTE]
>  窗口关闭后将无法重新打开。  
  
<a name="Window_Lifetime_Events"></a>   
### 窗口生存期事件  
 下面的插图显示了窗口的生存期中的主体事件的顺序。  
  
 ![窗口生存期](../../../../docs/framework/wpf/app-development/media/windowlifetimeevents.png "WindowLifetimeEvents")  
  
 下面的插图显示了窗口（显示时没有激活）生存期中的主体事件的顺序（显示窗口之前将 <xref:System.Windows.Window.ShowActivated%2A> 设置为 `false`）。  
  
 ![窗口生存期 &#40;Window.ShowActivated &#61; False&#41;](../../../../docs/framework/wpf/app-development/media/windowlifetimenoact.png "WindowLifetimeNoAct")  
  
<a name="WindowLocation"></a>   
## 窗口位置  
 当窗口打开时，窗口在相对于桌面的 x 和 y 维度有一个位置。  可以通过分别检查 <xref:System.Windows.Window.Left%2A> 和 <xref:System.Windows.Window.Top%2A> 属性来确定此位置。  可以设置这些属性以更改窗口的位置。  
  
 通过将 <xref:System.Windows.Window.WindowStartupLocation%2A> 属性设置为下面的 <xref:System.Windows.WindowStartupLocation> 枚举值之一，还可以指定 <xref:System.Windows.Window> 第一次出现时的初始位置：  
  
-   <xref:System.Windows.WindowStartupLocation>（默认值）  
  
-   <xref:System.Windows.WindowStartupLocation>  
  
-   <xref:System.Windows.WindowStartupLocation>  
  
 如果将起始位置指定为 <xref:System.Windows.WindowStartupLocation>，并且未设置 <xref:System.Windows.Window.Left%2A> 和 <xref:System.Windows.Window.Top%2A> 属性，则 <xref:System.Windows.Window> 将向 [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)] 请求显示的位置。  
  
<a name="Topmost_Windows_and_Z_Order"></a>   
### 最顶层窗口和 Z 顺序  
 除了具有 x 和 y 位置之外，窗口还在 z 维度中具有位置，该位置确定窗口相对于其他窗口的垂直位置。  此位置称作窗口的 z 顺序，有两种 z 顺序：正常 z 顺序和最顶层 z 顺序。  在正常 z 顺序中，窗口的位置取决于窗口当前是否活动。  默认情况下，窗口位于正常 z 顺序中。  在最顶层 z 顺序中，窗口的位置也取决于窗口当前是否活动。  此外，在最顶层 z 顺序中的窗口总是位于正常 z 顺序中的窗口之上。  通过将窗口的 <xref:System.Windows.Window.Topmost%2A> 属性设置为 `true` 可以使窗口位于最顶层 z 顺序中。  
  
 [!code-xml[WindowsOverviewSnippets#TopmostWindowMARKUP1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/TopmostWindow.xaml#topmostwindowmarkup1)]  
[!code-xml[WindowsOverviewSnippets#TopmostWindowMARKUP2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/TopmostWindow.xaml#topmostwindowmarkup2)]  
  
 在每个 z 顺序中，当前活动的窗口都会显示在同一 z 顺序中的所有其他窗口之上。  
  
<a name="WindowSize"></a>   
## 窗口大小  
 除了具有桌面位置以外，窗口还有一定的大小，窗口大小由多个属性确定，包括各种宽度和高度属性以及 <xref:System.Windows.Window.SizeToContent%2A>。  
  
 <xref:System.Windows.FrameworkElement.MinWidth%2A>、<xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.MaxWidth%2A> 用于管理窗口在生存期中可以具有的宽度的范围，其配置如下面的示例所示。  
  
 [!code-xml[WindowsOverviewSnippets#WidthWindowMARKUP1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WidthWindow.xaml#widthwindowmarkup1)]  
[!code-xml[WindowsOverviewSnippets#WidthWindowMARKUP2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WidthWindow.xaml#widthwindowmarkup2)]  
  
 窗口高度由 <xref:System.Windows.FrameworkElement.MinHeight%2A>、<xref:System.Windows.FrameworkElement.Height%2A> 和 <xref:System.Windows.FrameworkElement.MaxHeight%2A> 管理，其设置如下面的示例所示。  
  
 [!code-xml[WindowsOverviewSnippets#HeightWindowMARKUP1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/HeightWindow.xaml#heightwindowmarkup1)]  
[!code-xml[WindowsOverviewSnippets#HeightWindowMARKUP2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/HeightWindow.xaml#heightwindowmarkup2)]  
  
 因为各个宽度值和高度值各自指定了一个范围，所以可调整大小的窗口的宽度和高度可以是相应维度的指定范围内的任何值。  若要检测窗口的当前宽度和高度，请分别检查 <xref:System.Windows.FrameworkElement.ActualWidth%2A> 和 <xref:System.Windows.FrameworkElement.ActualHeight%2A>。  
  
 如果您想让窗口的宽度和高度适应窗口内容的大小，则可以使用 <xref:System.Windows.Window.SizeToContent%2A> 属性，该属性具有下面的值：  
  
-   <xref:System.Windows.SizeToContent>.  不起任何作用（默认）。  
  
-   <xref:System.Windows.SizeToContent>.  可以适应内容宽度，这与将 <xref:System.Windows.FrameworkElement.MinWidth%2A> 和 <xref:System.Windows.FrameworkElement.MaxWidth%2A> 设置为内容的宽度具有相同的效果。  
  
-   <xref:System.Windows.SizeToContent>.  可以适应内容高度，这与将 <xref:System.Windows.FrameworkElement.MinHeight%2A> 和 <xref:System.Windows.FrameworkElement.MaxHeight%2A> 设置为内容的高度具有相同的效果。  
  
-   <xref:System.Windows.SizeToContent>.  可以适应与内容宽度和高度，这与将 <xref:System.Windows.FrameworkElement.MinHeight%2A> 和 <xref:System.Windows.FrameworkElement.MaxHeight%2A> 设置为内容的高度并将 <xref:System.Windows.FrameworkElement.MinWidth%2A> 和 <xref:System.Windows.FrameworkElement.MaxWidth%2A> 设置为内容的宽度具有相同的效果。  
  
 下面的示例演示一个窗口自动调整大小垂直和水平地适应其内容，，那么，当首次显示。  
  
 [!code-xml[WindowsOverviewSnippets#SizeToContentWindowMARKUP1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/SizeToContentWindow.xaml#sizetocontentwindowmarkup1)]  
[!code-xml[WindowsOverviewSnippets#SizeToContentWindowMARKUP2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/SizeToContentWindow.xaml#sizetocontentwindowmarkup2)]  
  
 下面的示例演示如何在代码中设置 <xref:System.Windows.Window.SizeToContent%2A> 属性指定调整窗口大小以适合其内容。  
  
 [!code-csharp[HOWTOWindowManagementSnippets#SetWindowSizeToContentPropertyCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/CSharp/MainWindow.xaml.cs#setwindowsizetocontentpropertycode)]
 [!code-vb[HOWTOWindowManagementSnippets#SetWindowSizeToContentPropertyCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/visualbasic/mainwindow.xaml.vb#setwindowsizetocontentpropertycode)]  
  
<a name="OrderOfPrecedence"></a>   
## 大小调整属性的优先级顺序  
 实质上，窗口的各种大小属性可以结合使用，以定义可调整大小的窗口的宽度和高度范围。  为了确保保持有效的范围，<xref:System.Windows.Window> 会使用下面的优先级顺序来计算大小属性的值。  
  
 **对于高度属性：**  
  
1.  <xref:System.Windows.FrameworkElement.MinHeight%2A?displayProperty=fullName> \>  
  
2.  <xref:System.Windows.FrameworkElement.MaxHeight%2A?displayProperty=fullName> \>  
  
3.  <xref:System.Windows.SizeToContent?displayProperty=fullName>\/<xref:System.Windows.SizeToContent?displayProperty=fullName> \>  
  
4.  <xref:System.Windows.FrameworkElement.Height%2A?displayProperty=fullName>  
  
 **对于宽度属性：**  
  
1.  <xref:System.Windows.FrameworkElement.MinWidth%2A?displayProperty=fullName> \>  
  
2.  <xref:System.Windows.FrameworkElement.MaxWidth%2A?displayProperty=fullName> \>  
  
3.  <xref:System.Windows.SizeToContent?displayProperty=fullName>\/<xref:System.Windows.SizeToContent?displayProperty=fullName> \>  
  
4.  <xref:System.Windows.FrameworkElement.Width%2A?displayProperty=fullName>  
  
 优先级顺序还可以确定窗口在最大化时的大小；此时的窗口大小使用 <xref:System.Windows.Window.WindowState%2A> 属性管理。  
  
<a name="WindowState"></a>   
## 窗口状态  
 在可调整大小的窗口的生存期内，窗口可以有三种状态：正常、最小化和最大化。  处于正常状态的窗口是窗口的默认状态。  处于此状态的窗口如果是可调整大小的，则允许用户使用大小调整手柄或边框来移动窗口或调整窗口大小。  
  
 如果 <xref:System.Windows.Window.ShowInTaskbar%2A> 设置为 `true`，则处于最小化状态的窗口会折叠到任务栏按钮；否则，窗口会折叠到可能的最小大小并重新定位到桌面的左下角。  尽管不在任务栏中显示的最小化窗口可以在桌面上四处拖动，但是不能使用边框或大小调整手柄来调整上述两种最小化窗口的大小。  
  
 处于最大化状态的窗口会扩展到可能达到的最大大小，而最大大小只能与 <xref:System.Windows.FrameworkElement.MaxWidth%2A>、<xref:System.Windows.FrameworkElement.MaxHeight%2A> 和 <xref:System.Windows.Window.SizeToContent%2A> 属性规定的大小相同。  与最小化窗口一样，最大化窗口的大小也无法通过使用大小调整手柄或拖动边框来调整。  
  
> [!NOTE]
>  窗口的 <xref:System.Windows.Window.Top%2A>、<xref:System.Windows.Window.Left%2A>、<xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 属性的值始终表示正常状态的值，即使当窗口当前处于最大化或最小化状态时也是如此。  
  
 可以通过设置 <xref:System.Windows.Window.WindowState%2A> 属性来配置窗口的状态，该属性可以取以下 <xref:System.Windows.WindowState> 枚举值之一：  
  
-   <xref:System.Windows.WindowState>（默认值）  
  
-   <xref:System.Windows.WindowState>  
  
-   <xref:System.Windows.WindowState>  
  
 下面的示例说明如何创建在打开时最大化显示的窗口。  
  
 [!code-xml[WindowsOverviewSnippets#WindowStateWindowMARKUP1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowStateWindow.xaml#windowstatewindowmarkup1)]  
[!code-xml[WindowsOverviewSnippets#WindowStateWindowMARKUP2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowStateWindow.xaml#windowstatewindowmarkup2)]  
  
 通常，应设置 <xref:System.Windows.Window.WindowState%2A> 以配置窗口的初始状态。  一旦显示了可调整大小的窗口，用户便可以按窗口的标题栏上的最小化、最大化和还原按钮来更改窗口状态。  
  
<a name="WindowAppearance"></a>   
## 窗口外观  
 通过向窗口工作区添加窗口特定内容（如按钮、标签和文本框），可以更改窗口工作区的外观。  为了配置非工作区，<xref:System.Windows.Window> 提供了多个属性，包括设置窗口图标的 <xref:System.Windows.Window.Icon%2A> 和设置窗口标题的 <xref:System.Windows.Window.Title%2A>。  
  
 还可以通过配置窗口的大小调整模式、窗口样式，以及窗口是否显示为桌面任务栏中的按钮，来更改非工作区边框的外观和行为。  
  
   
  
<a name="Resize_Mode"></a>   
### 大小调整模式  
 根据 <xref:System.Windows.Window.WindowStyle%2A> 属性，您可以控制用户如何（以及是否可以）调整窗口的大小。  窗口样式的选择将影响用户是否可以通过用鼠标拖动边框来调整窗口的大小，非工作区是否显示**“最小化”**、**“最大化”**和**“调整大小”**按钮，以及如果显示这些按钮是否启用它们。  
  
 可以通过设置 <xref:System.Windows.Window.ResizeMode%2A> 属性来配置窗口调整大小的方式，该属性可以取以下 <xref:System.Windows.ResizeMode> 枚举值之一：  
  
-   <xref:System.Windows.ResizeMode>  
  
-   <xref:System.Windows.ResizeMode>  
  
-   <xref:System.Windows.ResizeMode>（默认值）  
  
-   <xref:System.Windows.ResizeMode>  
  
 和 <xref:System.Windows.Window.WindowStyle%2A> 相同，窗口的大小调整模式在其生存期内不能更改，这意味着您很可能会通过 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 标记设置该模式。  
  
 [!code-xml[WindowsOverviewSnippets#ResizeModeWindowMARKUP1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/ResizeModeWindow.xaml#resizemodewindowmarkup1)]  
[!code-xml[WindowsOverviewSnippets#ResizeModeWindowMARKUP2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/ResizeModeWindow.xaml#resizemodewindowmarkup2)]  
  
 请注意，通过检查 <xref:System.Windows.Window.WindowState%2A> 属性可以检测窗口是否被最大化、最小化或还原。  
  
<a name="Window_Style"></a>   
### 窗口样式  
 从窗口的非工作区公开的边框适合大多数应用程序。  但是，在有些情况下，可能需要使用不同类型的边框，或根本不需要边框，这要取决于窗口的类型。  
  
 若要控制窗口的边框的类型，请将窗口的 <xref:System.Windows.Window.WindowStyle%2A> 属性设置为以下 <xref:System.Windows.WindowStyle> 枚举值之一：  
  
-   <xref:System.Windows.WindowStyle>  
  
-   <xref:System.Windows.WindowStyle>（默认值）  
  
-   <xref:System.Windows.WindowStyle>  
  
-   <xref:System.Windows.WindowStyle>  
  
 下图显示了这些窗口样式的效果。  
  
 ![窗口样式](../../../../docs/framework/wpf/app-development/media/windowoverviewfigure6.png "WindowOverviewFigure6")  
  
 可以使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 标记或代码设置 <xref:System.Windows.Window.WindowStyle%2A>；因为窗口样式不能在窗口的生存期内更改，所以您很可能会使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 标记对其进行配置。  
  
 [!code-xml[WindowsOverviewSnippets#WindowStyleWindowMARKUP1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowStyleWindow.xaml#windowstylewindowmarkup1)]  
[!code-xml[WindowsOverviewSnippets#WindowStyleWindowMARKUP2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowStyleWindow.xaml#windowstylewindowmarkup2)]  
  
#### 非矩形窗口样式  
 在另外一些情况下， <xref:System.Windows.Window.WindowStyle%2A> 允许使用的边框样式不足以满足需要。  例如，您可能希望创建一个带有非矩形边框的应用程序，如 [!INCLUDE[TLA#tla_wmp](../../../../includes/tlasharptla-wmp-md.md)] 所使用的边框。  
  
 下图中显示的对话气泡框就是一个例子。  
  
 ![非矩形窗口](../../../../docs/framework/wpf/app-development/media/nonrectangularwindowfigure.PNG "NonRectangularWindowFigure")  
  
 通过将 <xref:System.Windows.Window.WindowStyle%2A> 属性设置为 <xref:System.Windows.WindowStyle>，并利用 <xref:System.Windows.Window> 对透明度的特殊支持，可以创建此类型的窗口。  
  
 [!code-xml[WindowsOverviewSnippets#TransparentWindowMARKUP1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/TransparentWindow.xaml#transparentwindowmarkup1)]  
[!code-xml[WindowsOverviewSnippets#TransparentWindowMARKUP2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/TransparentWindow.xaml#transparentwindowmarkup2)]  
  
 不同值的这种组合使窗口呈现完全透明。  在此状态中，无法使用窗口的非工作区修饰（“关闭”菜单、“最小化”、“最大化”和“还原”按钮，等等）。  因此，您需要提供自己的修饰。  
  
<a name="Task_Bar_Presence"></a>   
### 任务栏显示  
 窗口的默认外观包括一个任务栏按钮，如下图中所示。  
  
 ![具有任务栏按钮的窗口](../../../../docs/framework/wpf/app-development/media/windowoverviewfigure7.png "WindowOverviewFigure7")  
  
 有些类型的窗口没有任务栏按钮，例如消息框和对话框（请参见 [对话框概述](../../../../docs/framework/wpf/app-development/dialog-boxes-overview.md)）。  通过设置 <xref:System.Windows.Window.ShowInTaskbar%2A> 属性（默认情况下为 `true`）可以控制是否显示窗口的任务栏按钮。  
  
 [!code-xml[WindowsOverviewSnippets#ShowInTaskbarWindowMARKUP1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/ShowInTaskbarWindow.xaml#showintaskbarwindowmarkup1)]  
[!code-xml[WindowsOverviewSnippets#ShowInTaskbarWindowMARKUP2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/ShowInTaskbarWindow.xaml#showintaskbarwindowmarkup2)]  
  
<a name="SecurityConsiderations"></a>   
## 安全注意事项  
 <xref:System.Windows.Window> 要求实例化 `UnmanagedCode` 安全权限。  对于从本地计算机安装和启动的应用程序而言，这在为应用程序授予的权限集的范围之内。  
  
 但是，它却在为使用 [!INCLUDE[TLA#tla_clickonce](../../../../includes/tlasharptla-clickonce-md.md)] 从 Internet 或本地 Intranet 区域启动的应用程序授予的权限集的范围之外。  因此，用户将接收到一个 [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] 安全警告，并需要将应用程序的权限集提升到完全信任。  
  
 此外，[!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 在默认情况下无法显示窗口或对话框。  有关独立应用程序安全注意事项的讨论，请参见 [WPF 安全策略 — 平台安全性](../../../../docs/framework/wpf/wpf-security-strategy-platform-security.md)。  
  
<a name="Other_Types_of_Windows"></a>   
## 其他类型的窗口  
 <xref:System.Windows.Navigation.NavigationWindow> 是一个用于承载可导航内容的窗口。  有关更多信息，请参见 [导航概述](../../../../docs/framework/wpf/app-development/navigation-overview.md)。  
  
 对话框是通常用于从用户收集信息以完成某项功能的窗口。  例如，当用户要打开一个文件时，应用程序通常会显示**“打开文件”**对话框，以从用户那里获取文件名。  有关更多信息，请参见[对话框概述](../../../../docs/framework/wpf/app-development/dialog-boxes-overview.md)。  
  
## 请参阅  
 <xref:System.Windows.Window>   
 <xref:System.Windows.MessageBox>   
 <xref:System.Windows.Navigation.NavigationWindow>   
 <xref:System.Windows.Application>   
 [对话框概述](../../../../docs/framework/wpf/app-development/dialog-boxes-overview.md)   
 [生成 WPF 应用程序](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md)