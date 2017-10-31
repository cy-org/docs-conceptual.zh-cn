---
title: "Windows 窗体和 WPF 互操作性输入体系结构 | Microsoft Docs"
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
  - "ElementHost 键盘和消息"
  - "输入体系结构 [WPF 互操作性]"
  - "互操作性 [WPF], Windows 窗体"
  - "键盘互操作 [WPF]"
  - "消息 [WPF]"
  - "无模式对话框 [WPF]"
  - "无模式窗体"
  - "Windows 窗体 [WPF], 互操作性"
  - "Windows 窗体, WPF 互操作"
  - "WindowsFormsHost 键盘和消息"
ms.assetid: 0eb6f137-f088-4c5e-9e37-f96afd28f235
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Windows 窗体和 WPF 互操作性输入体系结构
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 与 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]之间的互操作要求这两项技术都有相应的键盘输入处理。  本主题介绍这两项技术如何实现键盘和消息处理，以在混合应用程序中启用平稳的互操作。  
  
 本主题包含以下小节：  
  
-   无模式窗体和对话框  
  
-   WindowsFormsHost 键盘和消息处理  
  
-   ElementHost 键盘和消息处理  
  
## 无模式窗体和对话框  
 调用 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素上的 <xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A> 方法可以从基于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的应用程序打开无模式窗体或对话框。  
  
 调用 <xref:System.Windows.Forms.Integration.ElementHost> 控件上的 <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A> 方法可以在基于 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]的应用程序中打开无模式的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 页面。  
  
## WindowsFormsHost 键盘和消息处理  
 当由基于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的应用程序承载时，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]键盘和消息处理将由以下各项组成：  
  
-   <xref:System.Windows.Forms.Integration.WindowsFormsHost> 类获取来自 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 消息循环的消息，这由 <xref:System.Windows.Interop.ComponentDispatcher> 类实现。  
  
-   <xref:System.Windows.Forms.Integration.WindowsFormsHost> 类创建代理项 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]消息循环，以确保 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]的例常键盘处理的进行。  
  
-   <xref:System.Windows.Forms.Integration.WindowsFormsHost> 类实现 <xref:System.Windows.Interop.IKeyboardInputSink> 接口，以便与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 协调焦点管理。  
  
-   <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件注册其自身并启动其消息循环。  
  
 后面几节更详细地介绍了该过程中的这些部分。  
  
### 从 WPF 消息循环获取消息  
 <xref:System.Windows.Interop.ComponentDispatcher> 类为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 实现消息循环管理器。  <xref:System.Windows.Interop.ComponentDispatcher> 类提供挂钩以使外部客户端可以在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 处理消息之前对这些消息进行筛选。  
  
 实现的互操作可处理 <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=fullName> 事件，从而允许 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件先于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件处理消息。  
  
### 代理项 Windows 窗体消息循环  
 默认情况下，<xref:System.Windows.Forms.Application?displayProperty=fullName> 类包含 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]应用程序的主消息循环。  在互操作过程中，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]消息循环不会处理消息。  因此，必须重新生成此逻辑。  <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=fullName> 事件的处理程序执行下面的步骤：  
  
1.  使用 <xref:System.Windows.Forms.IMessageFilter> 接口筛选消息。  
  
2.  调用 <xref:System.Windows.Forms.Control.PreProcessMessage%2A?displayProperty=fullName> 方法。  
  
3.  如果需要，转换并调度该消息。  
  
4.  如果没有其他控件处理该消息，将该消息传递给承载控件。  
  
### IKeyboardInputSink 实现  
 代理项消息循环处理键盘管理。  因此，<xref:System.Windows.Interop.IKeyboardInputSink.TabInto%2A?displayProperty=fullName> 方法是 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 类中唯一需要实现的 <xref:System.Windows.Interop.IKeyboardInputSink> 成员。  
  
 默认情况下，<xref:System.Windows.Interop.HwndHost> 类对其 <xref:System.Windows.Interop.HwndHost.System%23Windows%23Interop%23IKeyboardInputSink%23TabInto%2A> 实现返回 `false`。  这会阻止使用 Tab 键从 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件导航到 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。  
  
 <xref:System.Windows.Interop.IKeyboardInputSink.TabInto%2A?displayProperty=fullName> 方法的 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 实现执行下面的步骤：  
  
1.  查找 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件包含的并且可以接收焦点的第一个或最后一个 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件。  该控件选择取决于遍历信息。  
  
2.  将焦点设置到该控件并返回 `true`。  
  
3.  如果控件收不到焦点，则返回 `false`。  
  
### WindowsFormsHost 注册  
 在创建 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件的窗口句柄时，<xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件将调用为消息循环注册其存在的内部静态方法。  
  
 在注册过程中，<xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件将检查消息循环。  如果消息循环尚未启动，则将创建 <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=fullName> 事件处理程序。  消息循环被视为在附加 <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage?displayProperty=fullName> 事件处理程序时运行。  
  
 如果窗口句柄被损坏，则 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件将从注册中移除其自身。  
  
## ElementHost 键盘和消息处理  
 当由 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]应用程序承载时，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 键盘和消息处理将由以下各项组成：  
  
-   <xref:System.Windows.Interop.HwndSource>、<xref:System.Windows.Interop.IKeyboardInputSink> 和 <xref:System.Windows.Interop.IKeyboardInputSite> 接口实现。  
  
-   Tab 键导航和箭头键。  
  
-   命令键和对话框键。  
  
-   [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]快捷键处理。  
  
 以下几节更详细地介绍了这些部分。  
  
### 接口实现  
 在 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]中，键盘消息将路由到获得焦点的控件的窗口句柄。  在 <xref:System.Windows.Forms.Integration.ElementHost> 控件中，这些消息将路由到承载的元素。  为实现此目标，<xref:System.Windows.Forms.Integration.ElementHost> 控件提供了一个 <xref:System.Windows.Interop.HwndSource> 实例。  如果 <xref:System.Windows.Forms.Integration.ElementHost> 控件获得焦点，则 <xref:System.Windows.Interop.HwndSource> 实例会路由大多数键盘输入，以使其可以由 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.InputManager> 类处理。  
  
 <xref:System.Windows.Interop.HwndSource> 类实现 <xref:System.Windows.Interop.IKeyboardInputSink> 和 <xref:System.Windows.Interop.IKeyboardInputSite> 接口。  
  
 键盘互操作依赖于 <xref:System.Windows.Interop.IKeyboardInputSite.OnNoMoreTabStops%2A> 方法的实现来处理将焦点移出承载的元素的 Tab 键和箭头键输入。  
  
### Tab 键导航和箭头键  
 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]选择逻辑将映射到 <xref:System.Windows.Interop.HwndSource.System%23Windows%23Interop%23IKeyboardInputSink%23TabInto%2A> 和 <xref:System.Windows.Interop.IKeyboardInputSite.OnNoMoreTabStops%2A> 方法以实现 Tab 和箭头键导航。  重写 <xref:System.Windows.Forms.Integration.ElementHost.Select%2A> 方法即可实现此映射。  
  
### 命令键和对话框键  
 为了向 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供处理命令键和对话框键的第一次机会，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]命令预处理连接到 <xref:System.Windows.Interop.IKeyboardInputSink.TranslateAccelerator%2A> 方法。  重写 <xref:System.Windows.Forms.Control.ProcessCmdKey%2A?displayProperty=fullName> 方法会连接两项技术。  
  
 使用 <xref:System.Windows.Interop.IKeyboardInputSink.TranslateAccelerator%2A> 方法，承载的元素可以处理任何按键消息（如 WM\_KEYDOWN、WM\_KEYUP、WM\_SYSKEYDOWN 或 WM\_SYSKEYUP），包括命令键（如 Tab、Enter、Esc 以及箭头键）。  如果按键消息未被处理，则将其向上发送到 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]的上级层次结构进行处理。  
  
### 快捷键处理  
 若要正确处理快捷键，[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]快捷键处理必须连接到 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.AccessKeyManager>类。  另外，所有 WM\_CHAR 消息都必须正确路由到承载的元素。  
  
 由于 <xref:System.Windows.Interop.IKeyboardInputSink.TranslateChar%2A> 方法的默认 <xref:System.Windows.Interop.HwndSource> 实现返回 `false`，因此将使用以下逻辑处理 WM\_CHAR 消息：  
  
-   重写 <xref:System.Windows.Forms.Control.IsInputChar%2A?displayProperty=fullName> 方法，以确保所有 WM\_CHAR 消息转发到承载的元素。  
  
-   如果按下 Alt 键，则显示 WM\_SYSCHAR 消息。  [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 不会通过 <xref:System.Windows.Forms.Control.IsInputChar%2A> 方法预处理此消息。  因此，重写 <xref:System.Windows.Forms.Control.ProcessMnemonic%2A> 方法，以在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.AccessKeyManager> 中查询已注册的快捷键。  如果找到已注册的快捷键，则 <xref:System.Windows.Input.AccessKeyManager> 将对其进行处理。  
  
-   如果未按 Alt 键，则 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Input.InputManager> 类将处理尚未处理的输入。  如果输入为快捷键，则 <xref:System.Windows.Input.AccessKeyManager> 将对其进行处理。  为尚未处理的 WM\_CHAR 消息处理 <xref:System.Windows.Input.InputManager.PostProcessInput> 事件。  
  
 在用户按下 Alt 键时，快捷键的可视化提示将显示在整个窗体上。  若要支持此行为，活动窗体上的所有 <xref:System.Windows.Forms.Integration.ElementHost> 控件都需要接收 WM\_SYSKEYDOWN 消息，而不考虑哪个控件获得了焦点。  
  
 消息将仅发送给活动窗体中的 <xref:System.Windows.Forms.Integration.ElementHost> 控件。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A>   
 <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A>   
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [演练：在 WPF 中承载 Windows 窗体复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)   
 [演练：在 Windows 窗体中承载 WPF 复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)   
 [WPF 和 Win32 互操作](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)