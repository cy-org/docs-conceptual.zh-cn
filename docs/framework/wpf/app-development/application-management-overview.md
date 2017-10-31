---
title: "应用程序管理概述 | Microsoft Docs"
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
  - "应用程序管理 [WPF]"
ms.assetid: 32b1c054-5aca-423b-b4b5-ed8dc4dc637d
caps.latest.revision: 56
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 52
---
# 应用程序管理概述
所有应用程序往往共享通用应用于应用程序实现和管理功能的集合。  本主题提供创建和管理应用程序提供在 <xref:System.Windows.Application> 类的功能的概述。  
  
   
  
## 应用程序类  
 在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]，常见的应用程序范围的功能在 <xref:System.Windows.Application> 类中封装。  <xref:System.Windows.Application> 类包含以下功能:  
  
-   跟踪应用程序的生存期并与之交互。  
  
-   检索和处理命令行参数。  
  
-   检测和响应未经处理的异常。  
  
-   共享应用程序范围的属性和资源。  
  
-   管理独立应用程序中的窗口。  
  
-   跟踪和管理导航。  
  
<a name="The_Application_Class"></a>   
## 如何执行常规任务使用应用程序类  
 如果不是对所有 <xref:System.Windows.Application> 类的详细信息感兴趣，下表列出了一些 <xref:System.Windows.Application> 的常规任务以及如何完成它们。  通过查看相关 API 和主题中，您可以找到更多信息和代码示例。  
  
|任务|方法|  
|--------|--------|  
|获取表示当前应用程序的对象|使用 <xref:System.Windows.Application.Current%2A?displayProperty=fullName> 属性。|  
|添加一个启动屏幕到应用程序|请参见 [将初始屏幕添加到 WPF 应用程序](../../../../docs/framework/wpf/app-development/how-to-add-a-splash-screen-to-a-wpf-application.md)。|  
|启动应用程序|请使用 <xref:System.Windows.Application.Run%2A?displayProperty=fullName> 方法。|  
|停止应用程序|使用 <xref:System.Windows.Application.Current%2A> 对象的 <xref:System.Windows.Application.Shutdown%2A?displayProperty=fullName> 方法。|  
|从命令行获取参数|处理 <xref:System.Windows.Application.Startup?displayProperty=fullName> 事件和使用 <xref:System.Windows.StartupEventArgs.Args%2A?displayProperty=fullName> 属性。  有关示例，请参见 <xref:System.Windows.Application.Startup?displayProperty=fullName> 事件。|  
|获取和设置应用程序退出代码|将 <xref:System.Windows.Application.Exit?displayProperty=fullName> 事件处理程序的 <xref:System.Windows.ExitEventArgs.ApplicationExitCode%2A?displayProperty=fullName> 属性或调用 <xref:System.Windows.Application.Shutdown%2A> 方法并传入整数。|  
|检测和响应未经处理的异常|处理 <xref:System.Windows.Application.DispatcherUnhandledException> 事件。|  
|get 和 set 应用程序范围资源|使用 <xref:System.Windows.Application.Resources%2A?displayProperty=fullName> 属性。|  
|使用一个应用程序范围资源字典|请参见 [使用应用程序范围的资源字典](../../../../docs/framework/wpf/app-development/how-to-use-an-application-scope-resource-dictionary.md)。|  
|get 和 set 应用程序范围的属性|使用 <xref:System.Windows.Application.Properties%2A?displayProperty=fullName> 属性。|  
|获取和保存应用程序的状态|请参见 [跨应用程序会话保持和还原应用程序范围的属性](../../../../docs/framework/wpf/app-development/persist-and-restore-application-scope-properties.md)。|  
|管理非代码数据文件，包括资源文件、内容文件和源站点文件。|请参见 [WPF 应用程序资源、内容和数据文件](../../../../docs/framework/wpf/app-development/wpf-application-resource-content-and-data-files.md)。|  
|管理在独立应用程序的窗口|请参见 [WPF Windows 概述](../../../../docs/framework/wpf/app-development/wpf-windows-overview.md)。|  
|跟踪和管理导航|请参见 [导航概述](../../../../docs/framework/wpf/app-development/navigation-overview.md)。|  
  
<a name="The_Application_Definition"></a>   
## 应用程序定义  
 若要使用 <xref:System.Windows.Application> 类的功能，则必须实现应用程序定义。  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序定义是一个从 <xref:System.Windows.Application> 派生的类，并且使用特殊的 [!INCLUDE[TLA#tla_msbuild](../../../../includes/tlasharptla-msbuild-md.md)] 设置进行配置。  
  
### 实现应用程序定义  
 典型的 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序定义通过结合使用标记和代码隐藏来实现。  这使您能够使用标记以声明方式设置应用程序的属性、资源以及注册事件，同时在代码隐藏中处理事件并实现特定于应用程序的行为。  
  
 下面的示例演示如何结合使用标记与代码隐藏来实现应用程序定义：  
  
 [!code-xml[ApplicationSnippets#ApplicationXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationSnippets/CSharp/App.xaml#applicationxaml)]  
  
 [!code-csharp[ApplicationSnippets#ApplicationCODEBEHIND](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationSnippets/CSharp/App.xaml.cs#applicationcodebehind)]
 [!code-vb[ApplicationSnippets#ApplicationCODEBEHIND](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationSnippets/visualbasic/application.xaml.vb#applicationcodebehind)]  
  
 若要使标记文件和代码隐藏文件能够配合工作，需要满足下列条件：  
  
-   在标记中，`Application` 元素必须包含 `x:Class` 特性。  生成应用程序时，标记文件中如果存在 `x:Class`，则 [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] 将创建一个从 <xref:System.Windows.Application> 派生的 `partial` 类，并且该类的名称由 `x:Class` 特性指定。  这要求添加 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 架构的 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 命名空间声明 \(`xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`\)。  
  
-   在代码隐藏中，该类必须是 `partial` 类，其名称由标记中的 `x:Class` 特性指定，并且该类必须从 <xref:System.Windows.Application> 派生。  这样，代码隐藏文件就与应用程序生成时为标记文件生成的 `partial` 类相关联（请参见[生成 WPF 应用程序](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md)）。  
  
> [!NOTE]
>  在使用 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 创建新的 WPF 应用程序项目或 WPF 浏览器应用程序项目时，默认情况下会将应用程序定义包括在内并结合使用标记和代码隐藏来对其进行定义。  
  
 此类代码是实现应用程序定义的最低要求。  但是，若要生成并运行应用程序，需要对应用程序定义进行额外的 [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] 配置。  
  
### 针对 MSBuild 配置应用程序定义  
 独立应用程序和 [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] 要求实现某种级别的基础结构才能运行。  该基础结构最重要的部分是入口点。  当用户启动应用程序时，操作系统会调用入口点，入口点是一个用于启动应用程序的众所周知的函数。  
  
 传统上，根据所用技术的不同，开发人员一直需要自己编写部分或全部此类代码。  但是，当应用程序定义的标记文件被配置为 [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] `ApplicationDefinition` 项时，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 将为您生成此类代码，如下面的 [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] 项目文件中所示：  
  
```  
<Project   
  DefaultTargets="Build"  
  xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  ...  
  <ApplicationDefinition Include="App.xaml" />  
  <Compile Include="App.xaml.cs" />  
  ...  
</Project>  
```  
  
 由于代码隐藏文件包含代码，因此按照惯例将它标记为 [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] `Compile` 项。  
  
 对应用程序定义的标记和代码隐藏文件应用这些 [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] 配置会使 [!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)] 生成如下所示的代码：  
  
 [!code-csharp[AppDefAugSnippets#AppDefAugCODE1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AppDefAugSnippets/CSharp/App.cs#appdefaugcode1)]
 [!code-vb[AppDefAugSnippets#AppDefAugCODE1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AppDefAugSnippets/VisualBasic/App.vb#appdefaugcode1)]  
[!code-csharp[AppDefAugSnippets#AppDefAugCODE2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AppDefAugSnippets/CSharp/App.cs#appdefaugcode2)]
[!code-vb[AppDefAugSnippets#AppDefAugCODE2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AppDefAugSnippets/VisualBasic/App.vb#appdefaugcode2)]  
  
 生成的代码使用附加的基础结构代码扩充了应用程序定义，这些代码包括入口点方法 `Main`。  <xref:System.STAThreadAttribute> 属性被应用于 `Main` 方法以指示 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序的主 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 线程是一个 STA 线程，此线程是 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序所必需的。当 `Main` 被调用时，它将创建 `App` 的一个新实例，然后调用 `InitializeComponent` 方法来注册事件并设置在标记中实现的属性。  因为系统已为您生成 `InitializeComponent`，所以您无需像对 <xref:System.Windows.Controls.Page> 和 <xref:System.Windows.Window> 实现所做的那样从应用程序定义中显式调用 `InitializeComponent`。  最后，调用 <xref:System.Windows.Application.Run%2A> 方法以启动应用程序。  
  
<a name="Getting_the_Current_Application"></a>   
## 获取当前的应用程序  
 由于 <xref:System.Windows.Application> 类的功能在应用程序之间共享，因此只能有 <xref:System.Windows.Application> 类的一个实例每 <xref:System.AppDomain>。  为了实施这一点，系统将 <xref:System.Windows.Application> 类实现为单一实例类（请参见 [Implementing Singleton in C\#](http://go.microsoft.com/fwlink/?LinkId=100567)（在 C\# 中实现单一实例），该类使用 `static` <xref:System.Windows.Application.Current%2A> 属性创建自身的单一实例并提供对该实例的共享访问。  
  
 下面的代码显示对于当前的 <xref:System.AppDomain>，如何获得对 <xref:System.Windows.Application> 对象的引用。  
  
 [!code-csharp[ApplicationManagementOverviewSnippets#GetCurrentAppCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationManagementOverviewSnippets/CSharp/MainWindow.xaml.cs#getcurrentappcode)]
 [!code-vb[ApplicationManagementOverviewSnippets#GetCurrentAppCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationManagementOverviewSnippets/VisualBasic/MainWindow.xaml.vb#getcurrentappcode)]  
  
 <xref:System.Windows.Application.Current%2A> 返回对 <xref:System.Windows.Application> 类的实例的引用。  如果需要对 <xref:System.Windows.Application> 派生类的引用，必须强制转换 <xref:System.Windows.Application.Current%2A> 属性的值，如下面的示例中所示。  
  
 [!code-csharp[ApplicationManagementOverviewSnippets#GetSTCurrentAppCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationManagementOverviewSnippets/CSharp/MainWindow.xaml.cs#getstcurrentappcode)]
 [!code-vb[ApplicationManagementOverviewSnippets#GetSTCurrentAppCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationManagementOverviewSnippets/VisualBasic/MainWindow.xaml.vb#getstcurrentappcode)]  
  
 可以在 <xref:System.Windows.Application> 对象生存期中的任何时刻检查 <xref:System.Windows.Application.Current%2A> 的值。  但您应该十分谨慎。  在实例化 <xref:System.Windows.Application> 类之后， <xref:System.Windows.Application> 对象的状态会在一段时间内不一致。  在此时间段内，<xref:System.Windows.Application> 执行代码运行所需的各种初始化任务，其中包括建立应用程序基础结构、设置属性以及注册事件。  如果您在此期间尝试使用 <xref:System.Windows.Application> 对象，代码可能会有意外的结果，特别是当代码依赖于设置各种 <xref:System.Windows.Application> 属性时。  
  
 当 <xref:System.Windows.Application> 完成其初始化任务后，其生存期才真正开始。  
  
<a name="Application_Lifetime"></a>   
## 应用程序生存期  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序生存期由 <xref:System.Windows.Application> 所引发的几个事件来标记，这些事件告诉您应用程序何时启动、何时激活和停用以及何时关闭。  
  
   
  
<a name="Splash_Screen"></a>   
### 初始屏幕  
 当在 [!INCLUDE[net_v35SP1_short](../../../../includes/net-v35sp1-short-md.md)] 中启动时，您可以指定要在启动窗口中使用的图像或“初始屏幕”。  通过使用 <xref:System.Windows.SplashScreen> 类，可以在应用程序加载时轻松地显示启动窗口。  调用 <xref:System.Windows.Application.Run%2A> 之前将创建和显示 <xref:System.Windows.SplashScreen> 窗口。  有关更多信息，请参见[应用程序启动时间](../../../../docs/framework/wpf/advanced/application-startup-time.md)和[将初始屏幕添加到 WPF 应用程序](../../../../docs/framework/wpf/app-development/how-to-add-a-splash-screen-to-a-wpf-application.md)。  
  
<a name="Starting_an_Application"></a>   
### 启动应用程序  
 在调用 <xref:System.Windows.Application.Run%2A> 并且初始化应用程序之后，就可以运行应用程序了。  此时刻表示 <xref:System.Windows.Application.Startup> 事件的引发时间：  
  
 [!code-csharp[ApplicationStartupSnippets#StartupCODEBEHIND1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationStartupSnippets/CSharp/App.xaml.cs#startupcodebehind1)]
 [!code-vb[ApplicationStartupSnippets#StartupCODEBEHIND1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationStartupSnippets/visualbasic/application.xaml.vb#startupcodebehind1)]  
[!code-csharp[ApplicationStartupSnippets#StartupCODEBEHIND2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationStartupSnippets/CSharp/App.xaml.cs#startupcodebehind2)]
[!code-vb[ApplicationStartupSnippets#StartupCODEBEHIND2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationStartupSnippets/visualbasic/application.xaml.vb#startupcodebehind2)]  
  
 在应用程序生存期中的这一时刻，所要做的最常见的一件事情是显示 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]。  
  
<a name="Showing_a_User_Interface"></a>   
### 显示用户界面  
 大多数独立 [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)] 应用程序在开始运行时会打开一个 <xref:System.Windows.Window>。  可以在 <xref:System.Windows.Application.Startup> 事件处理程序中执行此操作，如下面的代码所示。  
  
 [!code-xml[AppShowWindowHardSnippets#StartupEventMARKUP](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AppShowWindowHardSnippets/CSharp/App.xaml#startupeventmarkup)]  
  
 [!code-csharp[AppShowWindowHardSnippets#StartupEventCODEBEHIND](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AppShowWindowHardSnippets/CSharp/App.xaml.cs#startupeventcodebehind)]
 [!code-vb[AppShowWindowHardSnippets#StartupEventCODEBEHIND](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/AppShowWindowHardSnippets/VisualBasic/Application.xaml.vb#startupeventcodebehind)]  
  
> [!NOTE]
>  默认情况下，在独立应用程序中实例化的第一个 <xref:System.Windows.Window> 成为主应用程序窗口。  此 <xref:System.Windows.Window> 对象由 <xref:System.Windows.Application.MainWindow%2A?displayProperty=fullName> 属性引用。  如果要使用与实例化的第一个 <xref:System.Windows.Window> 不同的窗口作为主窗口，可以使用编程方式更改 <xref:System.Windows.Application.MainWindow%2A> 属性的值。  
  
 当 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 首次启动时，它很可能导航到 <xref:System.Windows.Controls.Page>。  下面的代码对此进行演示。  
  
 [!code-xml[XBAPAppStartupSnippets#StartupXBAPMARKUP](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XBAPAppStartupSnippets/CSharp/App.xaml#startupxbapmarkup)]  
  
 [!code-csharp[XBAPAppStartupSnippets#StartupXBAPCODEBEHIND](../../../../samples/snippets/csharp/VS_Snippets_Wpf/XBAPAppStartupSnippets/CSharp/App.xaml.cs#startupxbapcodebehind)]
 [!code-vb[XBAPAppStartupSnippets#StartupXBAPCODEBEHIND](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/XBAPAppStartupSnippets/VisualBasic/Application.xaml.vb#startupxbapcodebehind)]  
  
 如果您处理 <xref:System.Windows.Application.Startup> 的目的只是为了打开 <xref:System.Windows.Window> 或导航到 <xref:System.Windows.Controls.Page>，则可以改为在标记中设置 `StartupUri` 特性。  
  
 下面的示例演示如何从独立应用程序中使用 <xref:System.Windows.Application.StartupUri%2A> 以打开 <xref:System.Windows.Window>。  
  
 [!code-xml[ApplicationManagementOverviewSnippets#OverviewStartupUriMARKUP](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationManagementOverviewSnippets/CSharp/App.xaml#overviewstartupurimarkup)]  
  
 下面的示例演示如何从 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 中使用 <xref:System.Windows.Application.StartupUri%2A> 以导航到 <xref:System.Windows.Controls.Page>。  
  
 [!code-xml[PageSnippets#XBAPStartupUriMARKUP](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PageSnippets/CSharp/App.xaml#xbapstartupurimarkup)]  
  
 此标记与前面用于打开窗口的代码具有相同的效果。  
  
> [!NOTE]
>  有关导航的更多信息，请参见[导航概述](../../../../docs/framework/wpf/app-development/navigation-overview.md)。  
  
 如果需要使用非默认的构造函数来实例化 <xref:System.Windows.Window>，或者需要在显示它之前设置它的属性或订阅它的事件，则需要处理 <xref:System.Windows.Application.Startup> 事件来打开它。  
  
<a name="Processing_Command_Line_Arguments"></a>   
### 处理命令行参数  
 在 [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)] 中，可以从命令提示符处或桌面启动独立应用程序。  在这两种情况下，都可以将命令行参数传递到应用程序。下面的示例演示一个使用单个命令行参数“\/StartMinimized”启动的应用程序：  
  
 `wpfapplication.exe /StartMinimized`  
  
 在应用程序初始化过程中，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 从操作系统检索命令行参数，然后通过 <xref:System.Windows.StartupEventArgs> 参数的 <xref:System.Windows.StartupEventArgs.Args%2A> 属性将这些命令行参数传递到 <xref:System.Windows.Application.Startup> 事件处理程序。  可以使用以下代码来检索和存储命令行参数。  
  
 [!code-xml[ApplicationStartupSnippets#HandleStartupXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationStartupSnippets/CSharp/App.xaml#handlestartupxaml)]  
  
 [!code-csharp[ApplicationStartupSnippets#HandleStartupCODEBEHIND](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationStartupSnippets/CSharp/App.xaml.cs#handlestartupcodebehind)]
 [!code-vb[ApplicationStartupSnippets#HandleStartupCODEBEHIND](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationStartupSnippets/visualbasic/application.xaml.vb#handlestartupcodebehind)]  
  
 这段代码处理 <xref:System.Windows.Application.Startup> 以检查是否提供了 **\/StartMinimized** 命令行参数；如果提供了此参数，则打开 <xref:System.Windows.WindowState> 为 <xref:System.Windows.WindowState> 的主窗口。  请注意，由于 <xref:System.Windows.Window.WindowState%2A> 属性必须以编程方式进行设置，因此必须在代码中显式打开主 <xref:System.Windows.Window>。  
  
 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 无法检索和处理命令行参数，因为它们是使用 [!INCLUDE[TLA#tla_clickonce](../../../../includes/tlasharptla-clickonce-md.md)] 部署（请参见[部署 WPF 应用程序](../../../../docs/framework/wpf/app-development/deploying-a-wpf-application-wpf.md)）启动的。  但是，这些应用程序可以通过用于启动它们的 URL 来获取和处理查询字符串形参。  
  
<a name="Application_Activation_and_Deactivation"></a>   
### 激活与停用应用程序  
 用户使用 [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)] 可以在应用程序之间进行切换。最常用的方法是使用 Alt\+Tab 组合键。  仅当应用程序具有用户可选择的可见的 <xref:System.Windows.Window> 时，才能切换到该应用程序。  当前选定的 <xref:System.Windows.Window> 是“活动窗口”（也称为前台窗口），并且是接收用户输入的 <xref:System.Windows.Window>。具有活动窗口的应用程序为“活动应用程序”（即前台应用程序）。在下列情况下，应用程序将成为活动应用程序：  
  
-   应用程序启动并显示一个 <xref:System.Windows.Window>。  
  
-   用户通过在应用程序中选择一个 <xref:System.Windows.Window> 从另一个应用程序切换过来。  
  
 可以通过处理 <xref:System.Windows.Application.Activated?displayProperty=fullName> 事件来检测应用程序何时成为活动应用程序。  
  
 与此类似，在下列情况下，应用程序成为非活动应用程序：  
  
-   用户从当前应用程序切换到另一个应用程序。  
  
-   应用程序关闭。  
  
 可以通过处理 <xref:System.Windows.Application.Deactivated?displayProperty=fullName> 事件来检测应用程序何时成为非活动应用程序。  
  
 下面的代码演示如何处理 <xref:System.Windows.Application.Activated> 和 <xref:System.Windows.Application.Deactivated> 事件以确定应用程序是否为活动应用程序。  
  
 [!code-xml[ApplicationActivationSnippets#DetectActivationStateXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationActivationSnippets/CSharp/App.xaml#detectactivationstatexaml)]  
  
 [!code-csharp[ApplicationActivationSnippets#DetectActivationStateCODEBEHIND](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationActivationSnippets/CSharp/App.xaml.cs#detectactivationstatecodebehind)]
 [!code-vb[ApplicationActivationSnippets#DetectActivationStateCODEBEHIND](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationActivationSnippets/visualbasic/application.xaml.vb#detectactivationstatecodebehind)]  
  
 还可以激活和停用 <xref:System.Windows.Window>。  有关更多信息，请参见<xref:System.Windows.Window.Activated?displayProperty=fullName>和<xref:System.Windows.Window.Deactivated?displayProperty=fullName>。  
  
> [!NOTE]
>  <xref:System.Windows.Application.Activated?displayProperty=fullName> 和 <xref:System.Windows.Application.Deactivated?displayProperty=fullName> 都不会对 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 引发。  
  
<a name="Application_Shutdown"></a>   
### 应用程序关闭  
 应用程序关闭时，其生存期就结束了。应用程序可能由于下列原因而关闭：  
  
-   用户关闭了所有 <xref:System.Windows.Window>。  
  
-   用户关闭了主 <xref:System.Windows.Window>。  
  
-   用户通过注销或关闭来终止 [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)] 会话。  
  
-   满足特定于应用程序的条件。  
  
 为了帮助您管理应用程序关闭，<xref:System.Windows.Application> 提供了 <xref:System.Windows.Application.Shutdown%2A> 方法、<xref:System.Windows.Application.ShutdownMode%2A> 属性以及 <xref:System.Windows.Application.SessionEnding> 和 <xref:System.Windows.Application.Exit> 事件。  
  
> [!NOTE]
>  只能从具有 <xref:System.Security.Permissions.UIPermission> 的应用程序调用 <xref:System.Windows.Application.Shutdown%2A>。  独立 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序始终具有该权限。  但是，在 Internet 区域中的部分信任安全沙盒中运行的 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 不具有该权限。  
  
#### 关闭模式  
 大多数应用程序在所有窗口关闭或主窗口关闭时都会关闭。  但有时其他特定于应用程序的条件可能决定应用程序何时关闭。  可以通过使用以下 <xref:System.Windows.ShutdownMode> 枚举值之一设置 <xref:System.Windows.Application.ShutdownMode%2A> 来指定应用程序关闭的条件：  
  
-   <xref:System.Windows.ShutdownMode>  
  
-   <xref:System.Windows.ShutdownMode>  
  
-   <xref:System.Windows.ShutdownMode>  
  
 <xref:System.Windows.Application.ShutdownMode%2A> 的默认值为 <xref:System.Windows.ShutdownMode>，该值表示应用程序将在用户关闭应用程序中的最后一个窗口时自动关闭。  但是，如果应用程序应当在主窗口关闭时关闭，并且您将 <xref:System.Windows.Application.ShutdownMode%2A> 设置为 <xref:System.Windows.ShutdownMode>，那么 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 会自动关闭。  这将在下面的示例中显示。  
  
 [!code-xml[ApplicationShutdownModeSnippets#OnMainWindowCloseMARKUP](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationShutdownModeSnippets/CS/Page1.xaml#onmainwindowclosemarkup)]  
  
 如果您具有特定于应用程序的关闭条件，请将 <xref:System.Windows.Application.ShutdownMode%2A> 设置为 <xref:System.Windows.ShutdownMode>。  在这种情况下，您应当通过显式调用 <xref:System.Windows.Application.Shutdown%2A> 方法来关闭应用程序；否则，即使所有窗口都已关闭，应用程序仍将继续运行。  请注意，当 <xref:System.Windows.Application.ShutdownMode%2A> 为 <xref:System.Windows.ShutdownMode> 或 <xref:System.Windows.ShutdownMode> 时，将会隐式调用 <xref:System.Windows.Application.Shutdown%2A>。  
  
> [!NOTE]
>  可以从 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 中设置 <xref:System.Windows.Application.ShutdownMode%2A>，但此设置将被忽略；当在浏览器中通过导航而离开 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 时，或者当承载 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 的浏览器关闭时，将总是关闭该应用程序。  有关更多信息，请参见[导航概述](../../../../docs/framework/wpf/app-development/navigation-overview.md)。  
  
#### 会话终止  
 <xref:System.Windows.Application.ShutdownMode%2A> 属性所描述的关闭条件是特定于应用程序的。  但在某些情况下，应用程序可能会由于外部条件而关闭。  最常见的外部条件出现在用户通过以下操作终止 [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)] 会话时：  
  
-   注销  
  
-   关机  
  
-   重新启动  
  
-   休眠  
  
 若要检测 [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)] 会话的终止时间，可以处理 <xref:System.Windows.Application.SessionEnding> 事件，如下面的示例所示。  
  
 [!code-xml[ApplicationSessionEndingSnippets#HandlingSessionEndingXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationSessionEndingSnippets/CSharp/App.xaml#handlingsessionendingxaml)]  
  
 [!code-csharp[ApplicationSessionEndingSnippets#HandlingSessionEndingCODEBEHIND](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationSessionEndingSnippets/CSharp/App.xaml.cs#handlingsessionendingcodebehind)]
 [!code-vb[ApplicationSessionEndingSnippets#HandlingSessionEndingCODEBEHIND](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationSessionEndingSnippets/visualbasic/application.xaml.vb#handlingsessionendingcodebehind)]  
  
 在此示例中，代码检查 <xref:System.Windows.SessionEndingCancelEventArgs.ReasonSessionEnding%2A> 属性以确定 [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)] 会话的结束方式。  代码使用该值向用户显示一个确认消息。  如果用户不希望终止会话，则代码会将 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 设置为 `true` 以阻止 [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)] 会话终止。  
  
> [!NOTE]
>  <xref:System.Windows.Application.SessionEnding> 不会对 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 引发。  
  
#### Exit  
 当应用程序关闭时，它可能需要执行一些最终处理，例如保存应用程序状态。  对于这些情况，您可以处理 <xref:System.Windows.Application.Exit> 事件。  
  
 [!code-xml[HOWTOApplicationModelSnippets#PersistRestoreAppScopePropertiesXAML1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/CSharp/App.xaml#persistrestoreappscopepropertiesxaml1)]  
[!code-xml[HOWTOApplicationModelSnippets#PersistRestoreAppScopePropertiesXAML2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/CSharp/App.xaml#persistrestoreappscopepropertiesxaml2)]  
  
 [!code-csharp[HOWTOApplicationModelSnippets#PersistAppScopePropertiesCODEBEHIND1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/CSharp/App.xaml.cs#persistappscopepropertiescodebehind1)]
 [!code-vb[HOWTOApplicationModelSnippets#PersistAppScopePropertiesCODEBEHIND1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/visualbasic/application.xaml.vb#persistappscopepropertiescodebehind1)]  
[!code-csharp[HOWTOApplicationModelSnippets#PersistAppScopePropertiesCODEBEHIND2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/CSharp/App.xaml.cs#persistappscopepropertiescodebehind2)]
[!code-vb[HOWTOApplicationModelSnippets#PersistAppScopePropertiesCODEBEHIND2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/visualbasic/application.xaml.vb#persistappscopepropertiescodebehind2)]  
  
 有关完整的示例，请参见[跨应用程序会话保持和还原应用程序范围的属性](../../../../docs/framework/wpf/app-development/persist-and-restore-application-scope-properties.md)。  
  
 独立应用程序和 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 都可以处理 <xref:System.Windows.Application.Exit>。  对于 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)]，在下列情况下会引发 <xref:System.Windows.Application.Exit>：  
  
-   离开一个 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]。  
  
-   在 [!INCLUDE[TLA2#tla_ie7](../../../../includes/tla2sharptla-ie7-md.md)] 中，关闭了承载 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 的选项卡。  
  
-   关闭了浏览器。  
  
#### 退出代码  
 应用程序通常由操作系统响应用户请求而启动。  但是，应用程序也可以由执行某个特定任务的其他应用程序启动。  当被启动的应用程序关闭时，启动它的应用程序可能想知道被启动的应用程序的关闭条件。  在这些情况下，[!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)] 允许应用程序在关闭时返回应用程序退出代码。  默认情况下，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 应用程序返回一个值为 0 的退出代码。  
  
> [!NOTE]
>  如果您在 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 中进行调试，应用程序退出代码会在应用程序关闭时显示在**“输出”**窗口中的如下所示的消息中：  
>   
>  `The program '[5340] AWPFApp.vshost.exe: Managed' has exited with code 0 (0x0).`  
>   
>  通过单击**“视图”**菜单上的**“输出”**可打开**“输出”**窗口。  
  
 若要更改输出代码，可以调用 <xref:System.Windows.Application.Shutdown%28System.Int32%29> 重载，该重载接受整数参数作为退出代码：  
  
 [!code-csharp[ApplicationExitSnippets#AppExitCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationExitSnippets/CSharp/MainWindow.xaml.cs#appexitcode)]
 [!code-vb[ApplicationExitSnippets#AppExitCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationExitSnippets/visualbasic/mainwindow.xaml.vb#appexitcode)]  
  
 可以通过处理 <xref:System.Windows.Application.Exit> 事件来检测和更改退出代码的值。  <xref:System.Windows.Application.Exit> 事件处理程序接受一个传递给它的 <xref:System.Windows.ExitEventArgs>，该参数通过 <xref:System.Windows.ExitEventArgs.ApplicationExitCode%2A> 属性提供对退出代码的访问。  有关更多信息，请参见 <xref:System.Windows.Application.Exit>。  
  
> [!NOTE]
>  在独立应用程序和 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 中都可以设置退出代码。  但是，[!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 将忽略退出代码值。  
  
<a name="Unhandled_Exceptions"></a>   
### 未经处理的异常  
 有时，应用程序可能在非正常条件下关闭，例如当引发意外的异常时。  在此情况下，应用程序可能没有代码来检测和处理异常。  这种类型的异常是未经处理的异常；在应用程序关闭之前，将显示一个如下图所示的通知。  
  
 ![未经处理的异常通知](../../../../docs/framework/wpf/app-development/media/applicationmanagementoverviewfigure2.png "ApplicationManagementOverviewFigure2")  
  
 从用户体验的角度来说，应用程序最好通过执行以下部分或全部操作来避免这一默认行为：  
  
-   显示用户友好的信息。  
  
-   尝试使应用程序继续运行。  
  
-   在 [!INCLUDE[TLA2#tla_mswin](../../../../includes/tla2sharptla-mswin-md.md)] 事件日志中以开发人员易于理解的方式详细记录异常信息。  
  
 实现此支持的前提是能够检测到未经处理的异常（对于该异常将引发 <xref:System.Windows.Application.DispatcherUnhandledException> 事件）。  
  
 [!code-xml[ApplicationDispatcherUnhandledExceptionSnippets#HandleDispatcherUnhandledExceptionXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationDispatcherUnhandledExceptionSnippets/CSharp/App.xaml#handledispatcherunhandledexceptionxaml)]  
  
 [!code-csharp[ApplicationDispatcherUnhandledExceptionSnippets#HandleDispatcherUnhandledExceptionCODEBEHIND1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationDispatcherUnhandledExceptionSnippets/CSharp/App.xaml.cs#handledispatcherunhandledexceptioncodebehind1)]
 [!code-vb[ApplicationDispatcherUnhandledExceptionSnippets#HandleDispatcherUnhandledExceptionCODEBEHIND1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationDispatcherUnhandledExceptionSnippets/visualbasic/application.xaml.vb#handledispatcherunhandledexceptioncodebehind1)]  
[!code-csharp[ApplicationDispatcherUnhandledExceptionSnippets#HandleDispatcherUnhandledExceptionCODEBEHIND2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ApplicationDispatcherUnhandledExceptionSnippets/CSharp/App.xaml.cs#handledispatcherunhandledexceptioncodebehind2)]
[!code-vb[ApplicationDispatcherUnhandledExceptionSnippets#HandleDispatcherUnhandledExceptionCODEBEHIND2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationDispatcherUnhandledExceptionSnippets/visualbasic/application.xaml.vb#handledispatcherunhandledexceptioncodebehind2)]  
  
 <xref:System.Windows.Application.DispatcherUnhandledException> 事件处理程序接受一个传递给它的 <xref:System.Windows.Threading.DispatcherUnhandledExceptionEventArgs> 参数，该参数包含关于未经处理的异常的上下文信息，其中包括异常本身 \(<xref:System.Windows.Threading.DispatcherUnhandledExceptionEventArgs.Exception%2A?displayProperty=fullName>\)。  使用该信息可以确定如何处理异常。  
  
 在处理 <xref:System.Windows.Application.DispatcherUnhandledException> 时，应当将 <xref:System.Windows.Threading.DispatcherUnhandledExceptionEventArgs.Handled%2A?displayProperty=fullName> 属性设置为 `true`；否则，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 仍会将异常视为未经处理的异常，并恢复前面描述的默认行为。  如果引发未经处理的异常，并且或者 <xref:System.Windows.Application.DispatcherUnhandledException> 事件未被处理，或者该事件被处理但 <xref:System.Windows.Threading.DispatcherUnhandledExceptionEventArgs.Handled%2A> 被设置为 `false`，则应用程序会立即关闭。  而且，不会再引发其他 <xref:System.Windows.Application> 事件。  因此，如果应用程序具有必须在应用程序关闭之前运行的代码，则需要处理 <xref:System.Windows.Application.DispatcherUnhandledException>。  
  
 尽管应用程序可能会由于未经处理的异常而关闭，但应用程序通常是为响应用户请求而关闭的，如下一节所述。  
  
<a name="Application_Lifetime_Events"></a>   
### 应用程序生存期事件  
 独立应用程序和 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)] 的生存期不完全相同。下图说明了独立应用程序的生存期中的关键事件，并显示这些事件的引发顺序。  
  
 ![独立应用程序 &#45; 应用程序对象事件](../../../../docs/framework/wpf/app-development/media/applicationmodeloverview-applicationobjectevents.png "ApplicationModelOverview\_ApplicationObjectEvents")  
  
 同样，下图说明了 [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] 的生存期中的关键事件，并显示这些事件的引发顺序。  
  
 ![XBAP &#45; 应用程序对象事件](../../../../docs/framework/wpf/app-development/media/applicationmodeloverview-applicationobjectevents-xbap.png "ApplicationModelOverview\_ApplicationObjectEvents\_xbap")  
  
## 请参阅  
 <xref:System.Windows.Application>   
 [WPF Windows 概述](../../../../docs/framework/wpf/app-development/wpf-windows-overview.md)   
 [导航概述](../../../../docs/framework/wpf/app-development/navigation-overview.md)   
 [WPF 应用程序资源、内容和数据文件](../../../../docs/framework/wpf/app-development/wpf-application-resource-content-and-data-files.md)   
 [WPF 中的 Pack URI](../../../../docs/framework/wpf/app-development/pack-uris-in-wpf.md)   
 [Application Model: How\-to Topics](http://msdn.microsoft.com/zh-cn/76771b09-3688-4d1c-8818-9b3f4cf39a30)   
 [应用程序开发](../../../../docs/framework/wpf/app-development/index.md)