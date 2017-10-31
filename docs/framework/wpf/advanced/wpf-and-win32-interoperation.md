---
title: "WPF 和 Win32 互操作 | Microsoft Docs"
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
  - "在 Win32 窗口中承载 WPF 内容"
  - "HWND 互操作 [WPF]"
  - "互操作性 [WPF], Win32"
  - "Win32 代码, WPF 互操作"
ms.assetid: 0ffbde0d-701d-45a3-a6fa-dd71f4d9772e
caps.latest.revision: 26
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 25
---
# WPF 和 Win32 互操作
本主题概述如何对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 代码进行互操作。  [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供用于创建应用程序的丰富环境。  但是，如果您对 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 代码的投入较大，那么更有效的办法是重用该代码的一部分。  
  
   
  
<a name="basics"></a>   
## WPF 和 Win32 互操作基础  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 代码互操作中有两项基本的技术。  
  
-   在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口中承载 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容。  使用此技术，您可以在标准 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口和应用程序的框架内使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的高级图形功能。  
  
-   在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容中承载 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口。  使用此技术，您可以在其他 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的上下文中使用现有的自定义 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 控件，并跨边界传递数据。  
  
 本主题将概念性地介绍每个技术。  有关在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 中承载 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的更侧重代码的演示，请参见[演练：在 Win32 中承载 WPF 内容](../../../../docs/framework/wpf/advanced/walkthrough-hosting-wpf-content-in-win32.md)。  有关在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中承载 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 的更侧重代码的演示，请参见[演练：在 WPF 中承载 Win32 控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-win32-control-in-wpf.md)。  
  
<a name="projects"></a>   
## WPF 互操作项目  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 是托管代码，但是大部分现有 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 程序以非托管 [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)] 的形式编写。  您不能从真正的非托管程序中调用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]。  但是，通过将 `/clr` 选项与 [!INCLUDE[TLA#tla_visualcpp](../../../../includes/tlasharptla-visualcpp-md.md)] 编译器配合使用，可以创建托管\/非托管混合程序，其中可以无缝地混合托管和非托管 [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 调用。  
  
 一个需要考虑的项目级问题是您不能将[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 文件编译到 [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)] 项目中。  有几项项目分离技术可以弥补这一点。  
  
-   创建一个 [!INCLUDE[TLA2#tla_cshrp](../../../../includes/tla2sharptla-cshrp-md.md)] DLL（其中以编译程序集的形式包含所有 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 页面），然后让 [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)] 可执行文件以引用的形式包括该 [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)]。  
  
-   为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容创建 [!INCLUDE[TLA2#tla_cshrp](../../../../includes/tla2sharptla-cshrp-md.md)] 可执行文件，然后让其引用包含 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 内容的 [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)] [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)]。  
  
-   使用 <xref:System.Windows.Markup.XamlReader.Load%2A> 在运行时加载任意 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，而不是编译您的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]。  
  
-   请勿使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]，并以代码方式编写所有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，从而从 <xref:System.Windows.Application> 生成元素树。  
  
 使用最适于您的任意方法。  
  
> [!NOTE]
>  如果未使用 [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)] 过，您可能注意到一些“新”关键字例如 `gcnew` 和 `nullptr` 在互操作代码示例所示。这些关键字取代旧双下划线语法\(`__gc`\)可为 [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)]的托管代码提供了更自然的语法。  若要了解 [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)] 托管功能的更多信息，请参见[适用于运行时平台的组件扩展](../Topic/Component%20Extensions%20for%20Runtime%20Platforms.md)和 [Hello, C\+\+\/CLI](http://go.microsoft.com/fwlink/?LinkId=98739)（欢迎使用 C\+\+\/CLI）。  
  
<a name="hwnds"></a>   
## WPF 如何使用 HWND  
 为了充分利用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]“HWND 互操作”，您需要了解 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 如何使用 HWND。  对于任何 HWND，您不能将 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 呈现与 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 呈现或 [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)]\/[!INCLUDE[TLA2#tla_gdiplus](../../../../includes/tla2sharptla-gdiplus-md.md)] 呈现混合。  这其中有许多含义。  首先，为了完全混合这些呈现模型，您必须创建互操作解决方案，并为您选择使用的每个呈现模型使用指定的互操作段。  同时，呈现行为为您的互操作解决方案可完成的任务创建“空间”限制。  “空间”概念会在主题 [技术区概述](../../../../docs/framework/wpf/advanced/technology-regions-overview.md)中详细介绍。  
  
 HWND 最终会支持屏幕上的所有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素。  当您创建 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Window> 时，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 会创建顶级 HWND，并使用 <xref:System.Windows.Interop.HwndSource> 将 <xref:System.Windows.Window> 及其 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容放入 HWND 中。  应用程序中其余的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容共享此单个 HWND。  不过，菜单、组合框下拉列表和其他弹出窗口例外。  这些元素创建它们自己的顶级窗口，这正是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 菜单能跳出包含它的窗口 HWND 之外的原因。  当您使用 <xref:System.Windows.Interop.HwndHost> 将 HWND 放入 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 时，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 通知 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 如何相对于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Window> HWND 定位新的子 HWND。  
  
 HWND 的相关概念是在每个 HWND 中和每个 HWND 之间是透明的。  主题 [技术区概述](../../../../docs/framework/wpf/advanced/technology-regions-overview.md)中也会对此进行讨论。  
  
<a name="hosting_a_wpf_page"></a>   
## 在 Microsoft Win32 窗口中承载 WPF 内容  
 在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口中承载 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的关键是使用 <xref:System.Windows.Interop.HwndSource> 类。  此类在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口中包装 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容，这样 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容可以作为子窗口并入到您的[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 中。  以下方法在单个应用程序中结合使用了 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]。  
  
1.  将您的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容（内容根元素）实现为托管类。  通常，该类继承自可包含多个子元素和\/或用作根元素的类之一，例如 <xref:System.Windows.Controls.DockPanel> 或 <xref:System.Windows.Controls.Page>。  在后面的步骤中，该类称为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容类，而该类的实例称为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容对象。  
  
2.  使用 [!INCLUDE[TLA2#tla_cppcli](../../../../includes/tla2sharptla-cppcli-md.md)] 实现 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 应用程序。  如果您要从现有的非托管 [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)] 应用程序开始操作，您通常可以通过将项目设置更改为包含 `/clr` 编译器标志来使该非托管应用程序可以调用托管代码（支持 `/clr` 编译所必需内容的完整范围没有在本主题中描述）。  
  
3.  将线程模型设置为单线程单元 \(STA\)。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用此线程模型。  
  
4.  在您的窗口过程中处理 WM\_CREATE 通知。  
  
5.  在处理程序（或处理程序调用的函数）中，执行以下操作：  
  
    1.  创建一个新 <xref:System.Windows.Interop.HwndSource> 对象，并使用父窗口 HWND 作为其 `parent` 参数。  
  
    2.  创建 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容类的一个实例。  
  
    3.  将对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容对象的引用分配给 <xref:System.Windows.Interop.HwndSource> 对象的 <xref:System.Windows.Interop.HwndSource.RootVisual%2A> 属性。  
  
    4.  <xref:System.Windows.Interop.HwndSource> 对象的 <xref:System.Windows.Interop.HwndSource.Handle%2A> 属性包含窗口句柄 \(HWND\)。  若要获得可在应用程序的非托管部分中使用的 HWND，请将 `Handle.ToPointer()` 强制转换为 HWND。  
  
6.  实现包含静态字段（该字段保留对您的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容对象的引用）的托管类。  此类允许您从您的 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 代码获得对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容对象的引用，但是更为重要的是它可以防止无意中对您的 <xref:System.Windows.Interop.HwndSource> 进行垃圾回收。  
  
7.  通过将一个处理程序附加到一个或多个 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容对象事件，从 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容对象接收通知。  
  
8.  与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的对象通信使用引用您在静态字段存储设置属性，调用方法等.  
  
> [!NOTE]
>  ，如果您生成一个单独的程序集引用它，然后使用内容选件类的默认节选件类，可以执行某些或所有第一步的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容类定义在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 。尽管您通常由一 <xref:System.Windows.Application> 对象作为生成 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 一部分到程序集中，作为互操作一部分，则不结果使用该 <xref:System.Windows.Application> ，为应用程序引用的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 文件使用一个或多个根选件类和引用它们的节选件类。  此过程的其余部分实际上类似于以上列出的过程。  
>   
>  主题[演练：在 Win32 中承载 WPF 内容](../../../../docs/framework/wpf/advanced/walkthrough-hosting-wpf-content-in-win32.md)中的代码演示了每个步骤。  
  
<a name="hosting_an_hwnd"></a>   
## 在 WPF 中承载 Microsoft Win32 窗口  
 在其他 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容中承载 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口的关键是使用 <xref:System.Windows.Interop.HwndHost> 类。  此类在可添加到 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素树的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素中包装该窗口。  <xref:System.Windows.Interop.HwndHost> 还支持 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]，它允许您为被承载的窗口执行处理消息之类的任务。  基本过程是：  
  
1.  为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序创建一个元素树（可以通过代码或标记创建）。  在可将 <xref:System.Windows.Interop.HwndHost> 实现添加为子元素的元素树中找出一个合适且允许的位置。  在这些步骤的剩余步骤中，此元素称为保留元素。  
  
2.  从 <xref:System.Windows.Interop.HwndHost> 派生以创建包含 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 内容的对象。  
  
3.  在该承载类中，重写 <xref:System.Windows.Interop.HwndHost> 方法 <xref:System.Windows.Interop.HwndHost.BuildWindowCore%2A>。  返回所承载的窗口的 HWND。  您可能希望将实际控件包装为所返回窗口的子窗口；包装宿主窗口中的控件为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容接收控件的通知提供了一种简单的方法。  此技术有助于更正一些有关在承载的控件边界处进行消息处理的 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 问题。  
  
4.  重写 <xref:System.Windows.Interop.HwndHost> 的 <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A> 方法和 <xref:System.Windows.Interop.HwndHost.WndProc%2A> 方法。  此处的目的是处理清理和移除对承载的内容的引用（特别是如果您创建了对非托管对象的引用）。  
  
5.  在代码隐藏文件中，创建承载类的控件的实例，然后使其成为保留元素的子元素。  通常，您将使用事件处理程序，例如 <xref:System.Windows.FrameworkElement.Loaded>，或使用分部类构造函数。  但是您也可以通过运行时行为添加互操作内容。  
  
6.  处理选定的窗口消息，例如控件通知。  有两种处理方法。  这两种方法提供对消息流的相同访问，因此您的选择很大程度上依赖于您的编程习惯。  
  
    -   在重写 <xref:System.Windows.Interop.HwndHost> 方法 <xref:System.Windows.Interop.HwndHost.WndProc%2A> 时，实现对所有消息（而不只是关闭消息）的消息处理。  
  
    -   让承载 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素通过处理 <xref:System.Windows.Interop.HwndHost.MessageHook> 事件来处理消息。  对于发送到承载的窗口的主窗口过程的每个消息，都会引发该事件。  
  
    -   您不能使用 <xref:System.Windows.Interop.HwndHost.WndProc%2A> 来处理位于进程外的窗口中的消息。  
  
7.  通过使用平台调用来调用非托管 `SendMessage` 函数来与承载的窗口进行通信。  
  
 按照以下这些步骤创建处理鼠标输入的应用程序。  您可以通过实现 <xref:System.Windows.Interop.IKeyboardInputSink> 接口来为承载的窗口添加 Tab 键支持。  
  
 主题[演练：在 WPF 中承载 Win32 控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-win32-control-in-wpf.md)中的代码演示了每个步骤。  
  
### WPF 中的 HWND  
 可以将 <xref:System.Windows.Interop.HwndHost> 想像为一个特殊控件。  （技术上讲，<xref:System.Windows.Interop.HwndHost> 是 <xref:System.Windows.FrameworkElement> 派生的类，不是 <xref:System.Windows.Controls.Control> 派生的类，但可以将其视为以互操作为用途的控件。）<xref:System.Windows.Interop.HwndHost> 对所承载内容的基础 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 性质进行抽象，以使 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的余下部分将所承载内容视为另一个类似于控件的对象，而此类对象应呈现并处理输入。  <xref:System.Windows.Interop.HwndHost> 的行为通常类似于任何其他 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.FrameworkElement>，但受基础 HWND 支持程度的限制，在输出（绘图和图形）和输入（鼠标和键盘）方面有一些重大的差异。  
  
#### 输出行为的显著差异  
  
-   <xref:System.Windows.FrameworkElement> 是 <xref:System.Windows.Interop.HwndHost> 基类，它具有很多能表示对 UI 的更改的属性。  这些属性包括 <xref:System.Windows.FrameworkElement.FlowDirection%2A?displayProperty=fullName> 之类的属性，该属性能更改父元素内的元素布局。  但是，大部分此类属性不能映射到可能存在的 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 等效项，即使这些等效项可能存在也是如此。  这些属性及其意义太多会使得呈现技术过于具体，以致于无法产生实际的映射。  因此，在 <xref:System.Windows.Interop.HwndHost> 上设置属性（例如 <xref:System.Windows.FrameworkElement.FlowDirection%2A>）没有效果。  
  
-   Transform 无法旋转、缩放、扭曲或影响 <xref:System.Windows.Interop.HwndHost>。  
  
-   <xref:System.Windows.Interop.HwndHost> 不支持 <xref:System.Windows.UIElement.Opacity%2A> 属性（Alpha 混合）。  如果 <xref:System.Windows.Interop.HwndHost> 中的内容执行 <xref:System.Drawing> 操作（这些操作包含 Alpha 信息），它自身不会产生冲突，但是 <xref:System.Windows.Interop.HwndHost> 作为一个整体仅支持 Opacity \= 1.0 \(100%\)。  
  
-   <xref:System.Windows.Interop.HwndHost> 将显示在同一顶级窗口中的其他 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素的上边。  但是，<xref:System.Windows.Controls.ToolTip> 或 <xref:System.Windows.Controls.ContextMenu> 生成的菜单是单独的顶级窗口，因此将正确处理 <xref:System.Windows.Interop.HwndHost>。  
  
-   <xref:System.Windows.Interop.HwndHost> 与其父 <xref:System.Windows.UIElement> 的剪辑区域不相关。  如果您尝试将 <xref:System.Windows.Interop.HwndHost> 类放入滚动区域或 <xref:System.Windows.Controls.Canvas>，则可能造成问题。  
  
#### 输入行为的显著差异  
  
-   通常，输入设备的范围限定在 <xref:System.Windows.Interop.HwndHost> 承载的 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 区域内，输入事件直接进入 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)]。  
  
-   当鼠标悬停在 <xref:System.Windows.Interop.HwndHost> 上时，您的应用程序不会收到 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 鼠标事件，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性 <xref:System.Windows.UIElement.IsMouseOver%2A> 的值将为 `false`。  
  
-   当 <xref:System.Windows.Interop.HwndHost> 拥有键盘焦点时，您的应用程序不会收到 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 键盘事件，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 属性 <xref:System.Windows.UIElement.IsKeyboardFocusWithin%2A> 的值将为 `false`。  
  
-   当焦点位于 <xref:System.Windows.Interop.HwndHost> 内，并更改为 <xref:System.Windows.Interop.HwndHost> 中的其他控件时，您的应用程序不会收到 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 事件 <xref:System.Windows.UIElement.GotFocus> 或 <xref:System.Windows.UIElement.LostFocus>。  
  
-   相关触笔属性和事件是相似的，当触笔悬浮于 <xref:System.Windows.Interop.HwndHost> 上时不会报告信息。  
  
<a name="tabbing_mnemonics_accelerators"></a>   
## Tab 键、助记键和快捷键  
 <xref:System.Windows.Interop.IKeyboardInputSink> 和 <xref:System.Windows.Interop.IKeyboardInputSite> 接口使您可以为混合的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 应用程序创建无缝键盘体验：  
  
-   在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 组件之间进行 Tab 键切换  
  
-   当焦点位于 Win32 组件中，以及位于 WPF 组件中时，助记键和快捷键都会起作用。  
  
 <xref:System.Windows.Interop.HwndHost> 和 <xref:System.Windows.Interop.HwndSource> 类都提供 <xref:System.Windows.Interop.IKeyboardInputSink> 的实现，但是它们可能不会处理更高级情况下所需的所有输入消息。  重写适当的方法以获取所需的键盘行为。  
  
 接口仅提供对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 区域之间的过渡上发生的事件的支持。  在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 区域内，Tab 键行为完全由 Tab 键的 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 实现的逻辑（如果有）来控制。  
  
## 请参阅  
 <xref:System.Windows.Interop.HwndHost>   
 <xref:System.Windows.Interop.HwndSource>   
 <xref:System.Windows.Interop>   
 [演练：在 WPF 中承载 Win32 控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-win32-control-in-wpf.md)   
 [演练：在 Win32 中承载 WPF 内容](../../../../docs/framework/wpf/advanced/walkthrough-hosting-wpf-content-in-win32.md)