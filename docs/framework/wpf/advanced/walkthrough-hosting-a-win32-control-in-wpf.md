---
title: "演练：在 WPF 中承载 Win32 控件 | Microsoft Docs"
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
  - "在 WPF 中承载 Win32 控件"
  - "Win32 代码, WPF 互操作"
ms.assetid: a676b1eb-fc55-4355-93ab-df840c41cea0
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 演练：在 WPF 中承载 Win32 控件
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供用于创建应用程序的丰富环境。  但是，如果您在 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 代码中有大量投资，则在您的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中至少重用该代码的一部分而非完全重写代码可能会更加有效。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了一种简单易懂的机制，用于在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 页上承载一个 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口。  
  
 本主题指导您编写一个应用程序 [Hosting a Win32 ListBox Control in WPF Sample](http://go.microsoft.com/fwlink/?LinkID=159998)（在 WPF 中承载 Win32 列表框控件示例），该应用程序承载一个 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 列表框控件。  可以对该一般性过程进行扩展以承载任何 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口。  
  
   
  
<a name="requirements"></a>   
## 要求  
 本主题假定您基本熟悉 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 编程。  有关 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 编程的基本介绍，请参见 [入门](../../../../docs/framework/wpf/getting-started/index.md)。  有关 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 编程的介绍，请参见关于此主题的众多书籍中的任何一本，特别推荐由 Charles Petzold 编写的 Programming Windows（《Windows 编程》）。  
  
 因为本主题附带的示例是用 [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] 实现的，所以该示例利用[!INCLUDE[TLA#tla_pinvoke](../../../../includes/tlasharptla-pinvoke-md.md)] 来访问 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)]。  稍微熟悉一下 [!INCLUDE[TLA2#tla_pinvoke](../../../../includes/tla2sharptla-pinvoke-md.md)] 是有用的，但不是必需的。  
  
> [!NOTE]
>  本主题包含关联示例中的一些代码示例。  但是，为了易读起见，本教程并不包含完整的代码示例。  可以从 [Hosting a Win32 ListBox Control in WPF Sample](http://go.microsoft.com/fwlink/?LinkID=159998)（在 WPF 中承载 Win32 列表框控件示例）获取或查看完整代码。  
  
<a name="basic_procedure"></a>   
## 基本过程  
 本节概述在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 页中承载 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口的基本过程。  其余各节将详细讨论每个步骤。  
  
 基本承载过程是：  
  
1.  实现一个用来承载窗口的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 页。  一种方法是创建一个 <xref:System.Windows.Controls.Border> 元素，以便为所承载的窗口保留该页的一部分。  
  
2.  实现一个从 <xref:System.Windows.Interop.HwndHost> 继承的类以承载控件。  
  
3.  在该类中，重写 <xref:System.Windows.Interop.HwndHost> 类成员 <xref:System.Windows.Interop.HwndHost.BuildWindowCore%2A>。  
  
4.  将所承载的窗口创建为包含 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 页的窗口的子窗口。  尽管传统 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 编程不需要显式利用承载页，但需要指出的是，承载页是一个带有句柄 \(HWND\) 的窗口。  通过 <xref:System.Windows.Interop.HwndHost.BuildWindowCore%2A> 方法的 `hwndParent` 参数接收页 HWND。  应该将所承载的窗口创建为此 HWND 的子窗口。  
  
5.  在创建宿主窗口之后，返回所承载的窗口的 HWND。  如果要承载一个或多个 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 控件，通常需要将宿主窗口创建为该 HWND 的子窗口，并且使这些控件成为该宿主窗口的子窗口。  通过将控件包装在宿主窗口中，可以提供一种让 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 页从这些控件接收通知的简单方式，该方式可以处理一些与跨 HWND 边界的通知有关的特定 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 问题。  
  
6.  处理发送到宿主窗口的选定消息，例如，来自子控件的通知。  有两种方法可以实现此目的。  
  
    -   如果您希望在承载类中处理消息，请重写 <xref:System.Windows.Interop.HwndHost> 类的 <xref:System.Windows.Interop.HwndHost.WndProc%2A> 方法。  
  
    -   如果您希望让 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 处理消息，请在代码隐藏文件中处理 <xref:System.Windows.Interop.HwndHost> 类 <xref:System.Windows.Interop.HwndHost.MessageHook> 事件。  对于所承载的窗口收到的每个消息，都将发生此事件。  如果您选择此选项，仍然必须重写 <xref:System.Windows.Interop.HwndHost.WndProc%2A>，但只需要最小实现。  
  
7.  重写 <xref:System.Windows.Interop.HwndHost> 的 <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A> 和 <xref:System.Windows.Interop.HwndHost.WndProc%2A> 方法。  必须重写这些方法以满足 <xref:System.Windows.Interop.HwndHost> 协定的要求，但可能只需要提供最小实现。  
  
8.  在代码隐藏文件中，创建控件承载类的一个实例，并使其成为用于承载窗口的 <xref:System.Windows.Controls.Border> 元素的子元素。  
  
9. 通过向所承载的窗口发送 [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] 消息以及处理来自其子窗口的消息（例如由控件发送的通知），与该窗口进行通信。  
  
<a name="page_layout"></a>   
## 实现页布局  
 承载 ListBox 控件的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 页的布局由两个区域组成。  该页的左侧承载了几个 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件，这些控件提供了一个 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 以使您可以操作 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 控件。  该页的右上角具有一个正方形区域，用于放置所承载的 ListBox 控件。  
  
 用于实现此布局的代码非常简单。  根元素是一个 <xref:System.Windows.Controls.DockPanel>，它具有两个子元素。  第一个子元素是一个用于承载 ListBox 控件的 <xref:System.Windows.Controls.Border> 元素。  它在该页的右上角占据了一个大小为 200x200 的正方形。  第二个子元素是一个 <xref:System.Windows.Controls.StackPanel> 元素，它包含一组 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件，这些控件显示信息，并使您可以通过设置已公开的互操作属性来操作 ListBox 控件。  对于 <xref:System.Windows.Controls.StackPanel> 的每个子元素，请参见有关所使用的各种元素的参考资料，以了解有关这些元素是什么以及它们有哪些功能的详细信息。下面的代码示例中列出了这些元素，但这里不对其进行说明（基本互操作模型不需要它们中的任何一个，提供它们的目的是为该示例增加一些交互性）。  
  
 [!code-xml[WPFHostingWin32Control#WPFUI](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/Page1.xaml#wpfui)]  
  
<a name="host_class"></a>   
## 实现类以承载 Microsoft Win32 控件  
 本示例的核心是实际承载控件的类 — ControlHost.cs。  它继承自 <xref:System.Windows.Interop.HwndHost>。  构造函数接受两个参数 — height 和 width，它们分别对应于承载 ListBox 控件的 <xref:System.Windows.Controls.Border> 元素的高度和宽度。  这些值将在以后用于确保控件的大小与 <xref:System.Windows.Controls.Border> 元素相匹配。  
  
 [!code-csharp[WPFHostingWin32Control#ControlHostClass](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#controlhostclass)]
 [!code-vb[WPFHostingWin32Control#ControlHostClass](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#controlhostclass)]  
  
 还有一组常量。  这些常量主要取自 Winuser.h，它们使您可以在调用 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 函数时使用传统名称。  
  
 [!code-csharp[WPFHostingWin32Control#ControlHostConstants](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#controlhostconstants)]
 [!code-vb[WPFHostingWin32Control#ControlHostConstants](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#controlhostconstants)]  
  
<a name="buildwindowcore"></a>   
### 重写 BuildWindowCore 以创建 Microsoft Win32 窗口  
 重写此方法以创建将由页承载的 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口，并且在窗口和页之间建立连接。  因为本示例涉及到承载 ListBox 控件，所以创建了两个窗口。  第一个窗口是由 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 页实际承载的窗口。  ListBox 控件被创建为该窗口的子窗口。  
  
 采用此方法的原因是为了简化从控件接收通知的过程。  使用 <xref:System.Windows.Interop.HwndHost> 类可以处理发送到它承载的窗口的消息。  如果直接承载 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 控件，您将收到被发送到该控件的内部消息循环的消息。  您可以显示控件并向其发送消息，但您不会收到该控件发送到它的父窗口的通知。  这意味着很多事情，其中一件事情便是您没有办法检测用户何时与该控件进行交互。  可改为创建一个宿主窗口，并使控件成为该窗口的子窗口。  这使您可以处理宿主窗口的消息，包括由控件发送给它的通知。  既然宿主窗口只是控件的简单包装而已，那么为了方便起见，以后将把该包装称为 ListBox 控件。  
  
<a name="create_the_window_and_listbox"></a>   
#### 创建宿主窗口和 ListBox 控件  
 使用 [!INCLUDE[TLA2#tla_pinvoke](../../../../includes/tla2sharptla-pinvoke-md.md)] 可以创建控件的宿主窗口，方法是创建并注册一个窗口类，然后执行其他相关操作。  但是，一种简单得多的方法是用预定义的“静态”窗口类创建一个窗口。  这将为您提供所需的窗口过程，以便从控件接收通知，并且只需完成最少的编码工作。  
  
 控件的 HWND 通过一个只读属性公开，以便宿主页可以使用它向控件发送消息。  
  
 [!code-csharp[WPFHostingWin32Control#IntPtrProperty](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#intptrproperty)]
 [!code-vb[WPFHostingWin32Control#IntPtrProperty](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#intptrproperty)]  
  
 ListBox 控件被创建为宿主窗口的子窗口。  这两个窗口的高度和宽度被设置为传递给构造函数的值，这在前面进行了讨论。  这可以确保宿主窗口和控件的大小与页上的保留区域相同。  在创建窗口之后，该示例将返回一个 <xref:System.Runtime.InteropServices.HandleRef> 对象，其中包含宿主窗口的 HWND。  
  
 [!code-csharp[WPFHostingWin32Control#BuildWindowCore](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#buildwindowcore)]
 [!code-vb[WPFHostingWin32Control#BuildWindowCore](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#buildwindowcore)]  
  
 [!code-csharp[WPFHostingWin32Control#BuildWindowCoreHelper](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#buildwindowcorehelper)]
 [!code-vb[WPFHostingWin32Control#BuildWindowCoreHelper](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#buildwindowcorehelper)]  
  
<a name="destroywindow_wndproc"></a>   
### 实现 DestroyWindow 和 WndProc  
 除了 <xref:System.Windows.Interop.HwndHost.BuildWindowCore%2A> 以外，您还必须重写 <xref:System.Windows.Interop.HwndHost> 的 <xref:System.Windows.Interop.HwndHost.WndProc%2A> 和 <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A> 方法。  在本示例中，控件的消息由 <xref:System.Windows.Interop.HwndHost.MessageHook> 处理程序处理，因而 <xref:System.Windows.Interop.HwndHost.WndProc%2A> 和 <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A> 的实现是最小实现。  在 <xref:System.Windows.Interop.HwndHost.WndProc%2A> 的情况下，请将 `handled` 设置为 `false` 以指示消息未处理，并且返回 0。  对于 <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A>，销毁窗口即可。  
  
 [!code-csharp[WPFHostingWin32Control#WndProcDestroy](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#wndprocdestroy)]
 [!code-vb[WPFHostingWin32Control#WndProcDestroy](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#wndprocdestroy)]  
  
 [!code-csharp[WPFHostingWin32Control#WndProcDestroyHelper](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#wndprocdestroyhelper)]
 [!code-vb[WPFHostingWin32Control#WndProcDestroyHelper](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#wndprocdestroyhelper)]  
  
<a name="host_the_control"></a>   
## 在页上承载控件  
 若要在页上承载控件，首先需要创建 `ControlHost` 类的新实例。  将包含该控件的边框元素 \(`ControlHostElement`\) 的高度和宽度传递给 `ControlHost` 构造函数。  这可以确保 ListBox 具有正确的大小。  然后，通过将 `ControlHost` 对象赋给宿主 <xref:System.Windows.Controls.Border> 的 <xref:System.Windows.Controls.Decorator.Child%2A> 属性，在页上承载该控件。  
  
 本示例将一个处理程序附加到 `ControlHost` 的 <xref:System.Windows.Interop.HwndHost.MessageHook> 事件，以便从控件接收消息。  对于发送到所承载的窗口的每个消息，都将引发此事件。  在此情况下，这些消息是发送给包装了实际 ListBox 控件的窗口的消息，包括来自控件的通知。  本示例调用 SendMessage 以便从控件获取信息以及修改它的内容。  下一节将详细讨论页如何与控件进行通信。  
  
> [!NOTE]
>  请注意，SendMessage 有两个 [!INCLUDE[TLA2#tla_pinvoke](../../../../includes/tla2sharptla-pinvoke-md.md)] 声明。  这是因为其中一个声明使用 `wParam` 参数传递字符串，而另一个声明使用该参数传递整数。  对于每个签名，都需要一个单独的声明，以确保正确封送数据。  
  
 [!code-csharp[WPFHostingWin32Control#HostWindowClass](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/Page1.xaml.cs#hostwindowclass)]
 [!code-vb[WPFHostingWin32Control#HostWindowClass](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/Page1.xaml.vb#hostwindowclass)]  
  
 [!code-csharp[WPFHostingWin32Control#ControlMsgFilterSendMessage](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/Page1.xaml.cs#controlmsgfiltersendmessage)]
 [!code-vb[WPFHostingWin32Control#ControlMsgFilterSendMessage](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/Page1.xaml.vb#controlmsgfiltersendmessage)]  
  
<a name="communication"></a>   
## 在控件和页之间实现通信  
 可以通过向控件发送 [!INCLUDE[TLA2#tla_win](../../../../includes/tla2sharptla-win-md.md)] 消息来操作控件。  当用户与控件交互时，控件会通过向其宿主窗口发送通知来通知您。  [Hosting a Win32 ListBox Control in WPF Sample](http://go.microsoft.com/fwlink/?LinkID=159998)（在 WPF 中承载 Win32 列表框控件示例）示例中包括一个 UI，它提供了演示这一机制的工作方式的几个示例：  
  
-   向列表中追加项。  
  
-   从列表中删除选定项。  
  
-   显示当前选定项的文本。  
  
-   显示列表中的项数。  
  
 用户还可以通过单击列表中的项来选择它，就像在传统 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 应用程序中一样。  每当用户通过选择、添加或追加项来更改列表框的状态时，都将更新所显示的数据。  
  
 若要追加项，请向列表框发送一个 LB\_ADDSTRING 消息。  若要删除项，请发送 LB\_GETCURSEL 以获取当前选定内容的索引，然后发送 LB\_DELETESTRING 以删除该项。  本示例还发送 LB\_GETCOUNT，并且使用返回的值更新所显示的项数。  这两个 SendMessage 实例都使用上一节中讨论的 [!INCLUDE[TLA2#tla_pinvoke](../../../../includes/tla2sharptla-pinvoke-md.md)] 声明之一。  
  
 [!code-csharp[WPFHostingWin32Control#AppendDeleteText](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/Page1.xaml.cs#appenddeletetext)]
 [!code-vb[WPFHostingWin32Control#AppendDeleteText](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/Page1.xaml.vb#appenddeletetext)]  
  
 当选择项的用户更改其选择时，控件将通过向宿主窗口发送 WM\_COMMAND 消息来通知该窗口，而该消息将为页面引发 <xref:System.Windows.Interop.HwndHost.MessageHook> 事件。  处理程序与宿主窗口的主窗口过程收到相同的信息。  它还会传递对布尔值 `handled` 的引用。  通过将 `handled` 设置为 `true` 可以指示您已经处理该消息并且无需进行其他处理。  
  
 发送 WM\_COMMAND 的原因多种多样，因此您必须检查通知 ID 以确定它是否是您希望处理的事件。  该 ID 包含在 `wParam` 参数的高位字中。  因为 [!INCLUDE[TLA#tla_net](../../../../includes/tlasharptla-net-md.md)] 不具有 HIWORD 宏，所以本示例使用按位运算符来提取该 ID。  如果用户已经进行选择或更改选择，该 ID 将为 LBN\_SELCHANGE。  
  
 在收到 LBN\_SELCHANGE 之后，本示例将通过向控件发送一个 LB\_GETCURSEL 消息来获取选定项的索引。  若要获取文本，首先需要创建一个 <xref:System.Text.StringBuilder>。  然后，向控件发送一个 LB\_GETTEXT 消息。  将空的 <xref:System.Text.StringBuilder> 对象作为 `wParam` 参数传递。  当 SendMessage 返回时，<xref:System.Text.StringBuilder> 将包含选定项的文本。  此处对 SendMessage 的使用还需要另外一个 [!INCLUDE[TLA2#tla_pinvoke](../../../../includes/tla2sharptla-pinvoke-md.md)] 声明。  
  
 最后，将 `handled` 设置为 `true` 以指示该消息已得到处理。  
  
## 请参阅  
 <xref:System.Windows.Interop.HwndHost>   
 [WPF 和 Win32 互操作](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)   
 [演练：开始使用 WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)