---
title: "演练：在 Win32 中承载 WPF 内容 | Microsoft Docs"
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
ms.assetid: 38ce284a-4303-46dd-b699-c9365b22a7dc
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# 演练：在 Win32 中承载 WPF 内容
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供了用于创建应用程序的丰富环境。  但是，当你对 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 代码有大量投入时，向应用程序添加 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 功能（而不是重写原始代码）可能更有效。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了一个简单的机制，用于在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口中承载 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容。  
  
 本教程介绍如何编写示例应用程序，[在 Win32 窗口示例中承载 WPF 内容](http://go.microsoft.com/fwlink/?LinkID=160004)，该应用程序可在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口中承载 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]内容。  你可以扩展此示例，使其可托管任何 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口。  由于涉及混合托管代码和非托管代码，应用程序是在 [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)] 中编写的。  
  
   
  
<a name="requirements"></a>   
## 要求  
 本教程假定你已基本熟悉 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 编程。  有关 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 编程的基本简介，请参阅 [入门](../../../../docs/framework/wpf/getting-started/index.md)。  有关 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 编程的简介，可参考有关该主题的众多书籍，尤其是 Charles Petzold 所著的 *Programming Windows*（《Windows 编程》）。  
  
 由于此教程随附的示例是在 [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)] 中实现的，因而本教程假定你熟悉使用 [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)] 进行 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 编程，并且了解托管代码编程。  熟悉 [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)] 将有所帮助，但并非必备条件。  
  
> [!NOTE]
>  本教程包括来自相关示例的一些代码示例。  但是，出于可读性考虑，不包括完整的示例代码。  有关完整示例代码的信息，请参阅[在 Win32 窗口示例中承载 WPF 内容](http://go.microsoft.com/fwlink/?LinkID=160004)。  
  
<a name="basic_procedure"></a>   
## 基本过程  
 本节概括介绍了用于在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口中承载 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的基本过程。  其余章节说明每个步骤的详细内容。  
  
 在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口中承载 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的关键是 <xref:System.Windows.Interop.HwndSource> 类。  此类在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口中包装 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容，从而使其可以作为子窗口并入你的 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 中。  以下方法在单个应用程序中合并 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]。  
  
1.  将你的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容作为托管类实现。  
  
2.  使用 [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)] 实现 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 应用程序。  如果从现有应用程序和非托管 [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)] 代码开始，你通常可以通过更改项目设置以包括 `/clr` 编译器标志来使其可以调用托管代码。  
  
3.  将线程处理模型设置为单线程单元 \(STA\)。  
  
4.  处理窗口过程中的 [WM\_CREATE](http://msdn.microsoft.com/library/ms632619.aspx) 通知并执行以下操作：  
  
    1.  创建一个新的 <xref:System.Windows.Interop.HwndSource> 对象，将父窗口用作其 `parent` 参数。  
  
    2.  创建 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容类的一个实例。  
  
    3.  向 <xref:System.Windows.Interop.HwndSource> 的 <xref:System.Windows.Interop.HwndSource.RootVisual%2A> 属性分配对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容对象的引用。  
  
    4.  获取该内容的 HWND。  <xref:System.Windows.Interop.HwndSource> 对象的 <xref:System.Windows.Interop.HwndSource.Handle%2A> 属性包含窗口句柄 \(HWND\)。  要获取可在应用程序的非托管部分中使用的 HWND，需将 `Handle.ToPointer()` 强制装换为 HWND。  
  
5.  实现一个托管类，该类包含一个用于保存对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的引用的静态字段。  该类使你可以从 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 代码获取对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的引用。  
  
6.  向静态字段分配 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容。  
  
7.  通过将处理程序附加到一个或多个 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 事件来从 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容接收通知。  
  
8.  通过使用存储在静态字段中用于设置属性等的引用来与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容通信。  
  
> [!NOTE]
>  还可以使用 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 来实现 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容。  但是，你必须将其作为 [!INCLUDE[TLA#tla_dll](../../../../includes/tlasharptla-dll-md.md)] 单独编译并从 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 应用程序引用 [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)]。  该过程的其余部分与上述相似。  
  
<a name="implementing_the_application"></a>   
## 实现主机应用程序  
 本节介绍如何在基本的 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 应用程序中托管 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容。  该内容本身是在 [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)] 中作为托管类实现的。  大多数情况下，它是简单的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 编程。  在[实现 WPF 内容](#implementing_the_wpf_page)中对内容实现的主要方面进行了探讨。  
  
<a name="autoNestedSectionsOUTLINE1"></a>   
-   [基本应用程序](#the_basic_application)  
  
-   [承载 WPF 内容](#hosting_the_wpf_page)  
  
-   [保存对 WPF 内容的引用](#holding_a_reference)  
  
-   [与 WPF 内容通信](#communicating_with_the_page)  
  
<a name="the_basic_application"></a>   
### 基本应用程序  
 主机应用程序的起点是创建 [!INCLUDE[TLA#tla_visualstu2005](../../../../includes/tlasharptla-visualstu2005-md.md)] 模板。  
  
1.  打开 [!INCLUDE[TLA2#tla_visualstu2005](../../../../includes/tla2sharptla-visualstu2005-md.md)]，然后在“文件”菜单中选择“新建项目”。  
  
2.  在 [!INCLUDE[TLA2#tla_visualcpp](../../../../includes/tla2sharptla-visualcpp-md.md)] 项目类型列表中选择“Win32”。  如果默认语言不是 [!INCLUDE[TLA2#tla_cpp](../../../../includes/tla2sharptla-cpp-md.md)]，你可以在“其他语言”下找到这些项目类型。  
  
3.  选择“Win32 项目”模板，为项目分配一个名称，然后单击“确定”以启动“Win32 应用程序向导”。  
  
4.  接受向导的默认设置，然后单击“完成”以启动项目。  
  
 该模板将创建一个基本的 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 应用程序，包括：  
  
-   应用程序的入口点。  
  
-   一个窗口和关联的窗口过程 \(WndProc\)。  
  
-   带有“文件”和“帮助”标题的菜单。  “文件”菜单具有用于关闭应用程序的“退出”项。  “帮助”菜单具有用于启动一个简单对话框的“关于”项。  
  
 在开始编写用于托管 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的代码之前，需要对基本模板做两项修改。  
  
 第一项是将项目作为托管代码进行编译。  默认情况下，项目将作为非托管代码进行编译。  但是，由于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 是在托管代码中实现的，因此必须将项目进行相应编译。  
  
1.  在“解决方案资源管理器”中右键单击项目名，然后从上下文菜单中选择“属性”以启动“属性页”对话框。  
  
2.  从左窗格中的树状视图中选择“配置属性”。  
  
3.  从右窗格中的“项目默认值”列表中选择“公共语言运行时”支持。  
  
4.  从下拉列表框中选择“公共语言运行时支持\(\/clr\)”。  
  
> [!NOTE]
>  此编译器标志使你能够在应用程序中使用托管代码，但非托管代码将仍将像以前一样进行编译。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 使用单线程单元 \(STA\) 线程处理模型。  为了正常使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容代码，必须通过对入口点应用特性，从而将应用程序的线程模型设置为 STA。  
  
 [!code-cpp[Win32HostingWPFPage#WinMain](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#winmain)]  
  
<a name="hosting_the_wpf_page"></a>   
### 承载 WPF 内容  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容是简单的地址条目应用程序。  它包含若干个 <xref:System.Windows.Controls.TextBox> 控件，这些控件用于获得用户名称、地址等。  还有两个 <xref:System.Windows.Controls.Button> 控件，即“确定”和“取消”。  用户单击“确定”时，该按钮的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件处理程序将收集来自 <xref:System.Windows.Controls.TextBox> 控件的数据，将其分配给相应的属性，并引发自定义事件 `OnButtonClicked`。  用户单击“取消”时，该处理程序只引发 `OnButtonClicked`。  `OnButtonClicked` 的事件参数对象包含布尔型字段，用于指示被单击的按钮。  
  
 用于托管 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的代码在主机窗口上的 [WM\_CREATE](http://msdn.microsoft.com/library/ms632619.aspx) 通知的处理程序中实现。  
  
 [!code-cpp[Win32HostingWPFPage#WMCreate](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#wmcreate)]  
  
 `GetHwnd` 方法使用大小和位置信息以及父窗口句柄并返回托管的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的窗口句柄。  
  
> [!NOTE]
>  无法对 `System::Windows::Interop` 命名空间使用 `#using` 指令。  如果进行此操作，将造成该命名空间中的 <xref:System.Windows.Interop.MSG> 结构和在 winuser.h 中声明的 MSG 结构之间的名称冲突。  必须使用完全限定名来访问该命名空间的内容。  
  
 [!code-cpp[Win32HostingWPFPage#GetHwnd](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#gethwnd)]  
  
 无法直接在应用程序窗口中托管 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容。  从而，首先创建 <xref:System.Windows.Interop.HwndSource> 对象以包装 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容。  此对象基本上是一个专门用于托管 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的窗口。  通过将 <xref:System.Windows.Interop.HwndSource> 对象创建为 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口（应用程序的一部分）的子级而将其托管于父窗口中。  <xref:System.Windows.Interop.HwndSource> 构造函数参数所包含的信息与创建 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 子窗口时要传递给 CreateWindow 的信息基本相同。  
  
 接下来，创建 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容对象的实例。  在此情况下，通过使用 [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)]，将 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容作为单独的类 `WPFPage` 实现。  还可以使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 实现 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容。  但需要为此设置一个单独的项目，并将 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容构建为 [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)]。  可以向项目添加对 [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)] 的引用，并使用该引用创建 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的实例。  
  
 通过向 <xref:System.Windows.Interop.HwndSource> 的 <xref:System.Windows.Interop.HwndSource.RootVisual%2A> 属性分配一个对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的引用，在子窗口中显示 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容。  
  
 代码的下一行将一个事件处理程序 `WPFButtonClicked` 附加到 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容 `OnButtonClicked` 事件。  用户单击“确定”或“取消”按钮时，该处理程序将被调用。  有关对此事件处理程序的深入探讨，请参阅[与 wpf 内容通信](#communicating_with_the_page)。  
  
 代码显示的最后一行返回与 <xref:System.Windows.Interop.HwndSource> 对象关联的窗口句柄 \(HWND\)。  可以从 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 代码使用此句柄，将消息发送到托管窗口，尽管该示例并未执行这一操作。  每当 <xref:System.Windows.Interop.HwndSource> 对象收到一条消息时就会引发一个事件。  若要处理消息，请调用 <xref:System.Windows.Interop.HwndSource.AddHook%2A> 方法来附加消息处理程序，然后在此处理程序中处理消息。  
  
<a name="holding_a_reference"></a>   
### 保存对 WPF 内容的引用  
 对于许多应用程序，你将需要稍后与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容进行通信。  例如，可能需要修改 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容属性，或可能让 <xref:System.Windows.Interop.HwndSource> 对象托管不同的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容。  执行此操作需要对 <xref:System.Windows.Interop.HwndSource> 对象或 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的引用。  <xref:System.Windows.Interop.HwndSource> 对象及其关联 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容保留在内存中，直到销毁窗口句柄。  但是，一旦从窗口过程返回，分配给 <xref:System.Windows.Interop.HwndSource> 对象的变量就将超出范围。  用来处理 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 应用程序的这一问题的惯用方法是使用静态或全局变量。  遗憾的是，你无法向这些类型的变量分配托管对象。  可以向全局或静态变量分配与 <xref:System.Windows.Interop.HwndSource> 对象关联的窗口句柄，但这一操作不会提供对对象本身的访问。  
  
 针对这一问题最简单的解决方案是实现一个托管类，该类包含一组静态字段，这些字段保存对需要访问的任何托管对象的引用。  此示例使用 `WPFPageHost` 类来保存对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的引用，以及对该内容某些属性的初始值的引用（用户以后可能会对这些属性进行更改）。  这在标头中进行定义。  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageHost](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.h#wpfpagehost)]  
  
 `GetHwnd` 函数的后半部分将值分配给这些字段以供以后使用（在 `myPage` 仍处于范围内时）。  
  
<a name="communicating_with_the_page"></a>   
### 与 WPF 内容通信  
 与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的通信有两种类型。  用户单击“确定”或“取消”按钮时，应用程序收到来自 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的信息。  该应用程序还具有 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]，使用户可以更改各种 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容属性，例如背景色或默认字体大小。  
  
 如上所述，用户单击任一按钮时，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容将引发 `OnButtonClicked` 事件。  该应用程序将一个处理程序附加到此事件以接收这些通知。  如果单击“确定”按钮，该处理程序将从 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容获得用户信息并将其显示在一组静态控件中。  
  
 [!code-cpp[Win32HostingWPFPage#WPFButtonClicked](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#wpfbuttonclicked)]  
  
 该处理程序从 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容接收到一个自定义事件参数对象 `MyPageEventArgs`。  如果单击“确定”按钮，对象的 `IsOK` 属性被设置为 `true`如果单击“取消”按钮，该属性被设置为 `false`。  
  
 如果单击“确定”按钮，该处理程序从容器类获取对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的引用。  然后它会收集由关联的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容属性保存的用户信息，并使用静态控件在父窗口上显示该信息。  由于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容数据的形式为托管字符串，因此必须对其进行封送处理以供 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 控件使用。  如果单击“取消”按钮，处理程序将清除静态控件中的数据。  
  
 应用程序 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 提供一组单选按钮，允许用户修改 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的背景色和若干与字体相关的属性。  下面的示例是应用程序的窗口过程 \(WndProc\) 的一段摘录及其消息处理功能，通过该功能可设置不同消息上的各种属性，包括背景色。  其他内容与此类似，将不进行展示。  请查看完整示例了解详细信息和上下文。  
  
 [!code-cpp[Win32HostingWPFPage#WMCommandToBG](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/Win32HostingWPFPage.cpp#wmcommandtobg)]  
  
 若要设置背景色，请从 `WPFPageHost` 获取对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容 \(`hostedPage`\) 的引用并将背景色属性设置为适当的颜色。  此示例使用三种颜色选项：原始颜色、浅绿色或浅橙红色。  原始背景色作为静态字段存储在 `WPFPageHost` 类中。  若要设置其他两种颜色，请创建一个新的 <xref:System.Windows.Media.SolidColorBrush> 对象，并从 <xref:System.Windows.Media.Colors> 对象向构造函数传递一个静态颜色值。  
  
<a name="implementing_the_wpf_page"></a>   
## 实现 WPF 页  
 可以托管和使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容而无需任何有关实际实现的知识。  如果 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容打包到一个单独的 [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)] 中，则可将其内置于任何 [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 语言中。  以下是在该示例中使用的 [!INCLUDE[TLA#tla_cppcli](../../../../includes/tlasharptla-cppcli-md.md)] 实现的简短演练。  本节包含下列子节。  
  
<a name="autoNestedSectionsOUTLINE2"></a>   
-   [布局](#page_layout)  
  
-   [将数据返回到主机窗口](#returning_data_to_window)  
  
-   [设置 WPF 属性](#set_page_properties)  
  
<a name="page_layout"></a>   
### 布局  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容中的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素由五个 <xref:System.Windows.Controls.TextBox> 控件（以及关联的 <xref:System.Windows.Controls.Label> 控件）构成：名称、地址、城市、州和邮编。  还有两个 <xref:System.Windows.Controls.Button> 控件，即“确定”和“取消”  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容在 `WPFPage` 类中实现。  布局通过 <xref:System.Windows.Controls.Grid> 布局元素进行处理。  该类继承自实际使其成为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容根元素的 <xref:System.Windows.Controls.Grid>。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容构造函数采用所需的宽度和高度，并相应地调整 <xref:System.Windows.Controls.Grid> 的大小。  然后，它通过创建一组 <xref:System.Windows.Controls.ColumnDefinition> 和 <xref:System.Windows.Controls.RowDefinition> 对象并将它们分别添加到 <xref:System.Windows.Controls.Grid> 对象基 <xref:System.Windows.Controls.Grid.ColumnDefinitions%2A> 和 <xref:System.Windows.Controls.Grid.RowDefinitions%2A> 集合来定义基本布局。  这将定义具有 5 行和 7 列的网格，该网格具有单元内容定义的维度。  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageCtorToGridDef](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagectortogriddef)]  
  
 接下来，此构造函数将 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素添加到 <xref:System.Windows.Controls.Grid>。  第一个元素是标题文本，这是一个在网格首行居中的 <xref:System.Windows.Controls.Label> 控件。  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageCtorTitle](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagectortitle)]  
  
 下一行包含名称 <xref:System.Windows.Controls.Label> 控制及其关联的 <xref:System.Windows.Controls.TextBox> 控件。  由于对每个标签\/文本框对使用同一代码，因而该代码被置于一对专用方法内并用于所有五个标签\/文本框对。  该方法创建相应的控件，并调用 <xref:System.Windows.Controls.Grid> 类静态 <xref:System.Windows.Controls.Grid.SetColumn%2A> 和 <xref:System.Windows.Controls.Grid.SetRow%2A> 方法，以将控件置于相应单元格内。  创建控件后，该示例对 <xref:System.Windows.Controls.Grid> 的 <xref:System.Windows.Controls.Panel.Children%2A> 属性调用 <xref:System.Windows.Controls.UIElementCollection.Add%2A> 方法，以便将控件添加到网格。  用于添加剩余标签\/文本框对的代码相似。  请参阅示例代码了解详细信息。  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageCtorName](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagectorname)]  
  
 这两种方法的实现如下所示：  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageCreateHelpers](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagecreatehelpers)]  
  
 最后，该示例添加“确定”和“取消”按钮，然后将一个事件处理程序附加到它们的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件。  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageCtorButtonsEvents](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagectorbuttonsevents)]  
  
<a name="returning_data_to_window"></a>   
### 将数据返回到主机窗口  
 单击任一按钮后，将引发其 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件。  主机窗口只需将处理程序附加到这些事件，然后直接从 <xref:System.Windows.Controls.TextBox> 控件获取数据。  此示例使用的是不太直接的方法。  它处理 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容内的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click>，然后引发自定义事件 `OnButtonClicked` 来通知 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容。  这使 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容能够在通知主机之前执行某些参数验证。  该处理程序从 <xref:System.Windows.Controls.TextBox> 控件获取文本，然后将其分配给公共属性（主机可从其中检索信息）。  
  
 WPFPage.h 中的事件声明：  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageEventDecl](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.h#wpfpageeventdecl)]  
  
 WPFPage.cpp 中的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件处理程序：  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageButtonClicked](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagebuttonclicked)]  
  
<a name="set_page_properties"></a>   
### 设置 WPF 属性  
 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 主机使用户可以更改若干 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容属性。  就 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 端而言，这只是更改属性的问题。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容类中的实现从某种意义上来说更加复杂，因为不存在控制所有控件的字体的单个全局属性。  相反，每个控件的相应属性均是在属性的 set 访问器中进行更改的。  下面的示例显示 `DefaultFontFamily` 属性的代码。  设置属性将调用专用方法，该方法依次又将为各控件设置 <xref:System.Windows.Controls.Control.FontFamily%2A> 属性。  
  
 从 WPFPage.h：  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageFontFamilyProperty](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.h#wpfpagefontfamilyproperty)]  
  
 从 WPFPage.cpp：  
  
 [!code-cpp[Win32HostingWPFPage#WPFPageSetFontFamily](../../../../samples/snippets/cpp/VS_Snippets_Wpf/Win32HostingWPFPage/CPP/WPFPage.cpp#wpfpagesetfontfamily)]  
  
## 请参阅  
 <xref:System.Windows.Interop.HwndSource>   
 [WPF 和 Win32 互操作](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)