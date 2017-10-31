---
title: "混合应用程序疑难解答 | Microsoft Docs"
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
  - "混合应用程序 [WPF 互操作性]"
  - "互操作性 [WPF], Windows 窗体"
  - "消息循环 [WPF]"
  - "重叠控件"
  - "Windows 窗体 [WPF], 互操作性"
  - "Windows 窗体, WPF 互操作"
ms.assetid: f440c23f-fa5d-4d5a-852f-ba61150e6405
caps.latest.revision: 26
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 25
---
# 混合应用程序疑难解答
<a name="introduction"></a> 本主题列出了在创作同时使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]技术的混合应用程序时可能发生的一些常见问题。  
  
   
  
<a name="overlapping_controls"></a>   
## 重叠控件  
 控件可能不按预期的方式重叠。  [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]为每个控件使用一个单独的 HWND。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 为一个页面上的所有内容使用一个 HWND。  这一实现差异导致意外的重叠行为。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中承载的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件总是出现在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容之上。  
  
 <xref:System.Windows.Forms.Integration.ElementHost> 控件中承载的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容出现在 <xref:System.Windows.Forms.Integration.ElementHost> 控件的 Z 顺序中。  可以重叠 <xref:System.Windows.Forms.Integration.ElementHost> 控件，但所承载的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容不能组合或交互。  
  
<a name="child_property"></a>   
## 子属性  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 和 <xref:System.Windows.Forms.Integration.ElementHost> 类只能承载单个子控件或元素。  若要承载多个控件或元素，必须使用容器作为子内容。  例如，可以向 <xref:System.Windows.Forms.Panel?displayProperty=fullName> 控件添加 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]按钮和复选框控件，然后将该面板分配给 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件的 <xref:System.Windows.Forms.Integration.WindowsFormsHost.Child%2A> 属性。  但是，不能将按钮和复选框控件分别添加到相同的 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件。  
  
<a name="scaling"></a>   
## 缩放  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]具有不同的缩放模型。  一些 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 缩放变换对于 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件是有意义的，但其他变换是无意义的。  例如，将 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] 控件缩放到 0 是可行的，但如果您尝试将同一控件重新缩放回非零值，则该控件的大小仍然为 0。  有关更多信息，请参见[WindowsFormsHost 元素的布局注意事项](../../../../docs/framework/wpf/advanced/layout-considerations-for-the-windowsformshost-element.md)。  
  
<a name="adapter"></a>   
## 适配器  
 在使用 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 和 <xref:System.Windows.Forms.Integration.ElementHost> 类时可能会发生混乱，因为它们包含一个隐藏容器。  <xref:System.Windows.Forms.Integration.WindowsFormsHost> 和 <xref:System.Windows.Forms.Integration.ElementHost> 类都具有一个名为“适配器”的隐藏容器，它用来承载内容。  对于 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素，该适配器派生自 <xref:System.Windows.Forms.ContainerControl?displayProperty=fullName> 类。  对于 <xref:System.Windows.Forms.Integration.ElementHost> 控件，该适配器派生自 <xref:System.Windows.Controls.DockPanel> 元素。  如果您发现其他互操作主题中提到了适配器，那么所讨论的就是这个容器。  
  
<a name="nesting"></a>   
## 嵌套  
 不支持在 <xref:System.Windows.Forms.Integration.ElementHost> 控件内部嵌套 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素。  也不支持在 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素内部嵌套 <xref:System.Windows.Forms.Integration.ElementHost> 控件。  
  
<a name="focus"></a>   
## 焦点  
 焦点在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]中的工作方式是不同的，这意味着在混合应用程序中可能发生焦点问题。  例如，如果 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素内部具有焦点，那么，当最小化并还原页面，或者显示模式对话框时，<xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素内部的焦点可能会丢失。  <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素仍然具有焦点，但该元素内部的控件可能不具有焦点。  
  
 数据验证也受到焦点的影响。  验证在 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素中有效，但当您按 Tab 键离开 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素或者在两个不同的 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素之间切换时，验证将无效。  
  
<a name="property_mapping"></a>   
## 属性映射  
 某些属性映射需要先进行大量的转译，才能将 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]技术之间不同的实现桥接起来。  通过属性映射，可以使您的编码对字体、颜色和其他属性方面的更改做出反应。  通常，属性映射的工作方式是侦听*属性*Changed 事件或 On*属性*Changed 调用，然后在子控件或其适配器上设置适当的属性。  有关更多信息，请参见 [Windows 窗体和 WPF 属性映射](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md)。  
  
<a name="layoutrelated_properties_on_hosted_content"></a>   
## 所承载内容上的布局相关属性  
 在分配 <xref:System.Windows.Forms.Integration.WindowsFormsHost.Child%2A?displayProperty=fullName> 或 <xref:System.Windows.Forms.Integration.ElementHost.Child%2A?displayProperty=fullName> 属性后，将自动设置所承载内容上的几个布局相关属性。  更改这些内容属性会导致意外的布局行为。  
  
 将停靠所承载的内容，以便填充 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 和 <xref:System.Windows.Forms.Integration.ElementHost> 父级。  为了启用此填充行为，在设置子属性时，将设置多个属性。  下表列出了由 <xref:System.Windows.Forms.Integration.ElementHost> 和 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 类设置的内容属性。  
  
|宿主类|内容属性|  
|---------|----------|  
|<xref:System.Windows.Forms.Integration.ElementHost>|<xref:System.Windows.FrameworkElement.Height%2A><br /><br /> <xref:System.Windows.FrameworkElement.Width%2A><br /><br /> <xref:System.Windows.FrameworkElement.Margin%2A><br /><br /> <xref:System.Windows.FrameworkElement.VerticalAlignment%2A><br /><br /> <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>|  
|<xref:System.Windows.Forms.Integration.WindowsFormsHost>|<xref:System.Windows.Forms.Control.Margin%2A><br /><br /> <xref:System.Windows.Forms.Control.Dock%2A><br /><br /> <xref:System.Windows.Forms.Control.AutoSize%2A><br /><br /> <xref:System.Windows.Forms.Control.Location%2A><br /><br /> <xref:System.Windows.Forms.Control.MaximumSize%2A>|  
  
 不要在所承载的内容上直接设置这些属性。  有关更多信息，请参见[WindowsFormsHost 元素的布局注意事项](../../../../docs/framework/wpf/advanced/layout-considerations-for-the-windowsformshost-element.md)。  
  
<a name="navigation_applications"></a>   
## 导航应用程序  
 导航应用程序不能维护用户状态。  在导航应用程序中使用 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素时，该元素将重新创建其控件。  当用户通过导航操作离开承载 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素的页面，然后又返回到该页面时，将发生重新创建子控件的操作。  用户已经键入的任何内容都将丢失。  
  
<a name="message_loop_interoperation"></a>   
## 消息循环互操作  
 在使用 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]消息循环时，可能无法按照预期方式处理消息。  <xref:System.Windows.Forms.Integration.WindowsFormsHost.EnableWindowsFormsInterop%2A> 方法由 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 构造函数调用。  此方法向 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 消息循环中添加一个消息筛选器。  如果 <xref:System.Windows.Forms.Control?displayProperty=fullName> 是消息的目标，此筛选器会调用 <xref:System.Windows.Forms.Control.PreProcessMessage%2A?displayProperty=fullName> 方法并且转换\/调度该消息。  
  
 如果您在 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]消息循环中使用 <xref:System.Windows.Forms.Application.Run%2A?displayProperty=fullName> 显示了一个 <xref:System.Windows.Window>，那么除非调用 <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A> 方法，否则不能键入任何内容。  <xref:System.Windows.Forms.Integration.ElementHost.EnableModelessKeyboardInterop%2A> 方法接受一个 <xref:System.Windows.Window>，并且添加一个 <xref:System.Windows.Forms.IMessageFilter?displayProperty=fullName>，后者将与键相关的消息重新传送到 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 消息循环。  有关更多信息，请参见 [Windows 窗体和 WPF 互操作性输入体系结构](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-interoperability-input-architecture.md)。  
  
<a name="opacity_and_layering"></a>   
## 不透明度和分层  
 <xref:System.Windows.Interop.HwndHost> 类不支持分层。  这意味着在 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素上设置 <xref:System.Windows.UIElement.Opacity%2A> 属性不起作用，并且不会与 <xref:System.Windows.Window.AllowsTransparency%2A> 设置为 `true` 的其他 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 窗口产生混合效果。  
  
<a name="dispose"></a>   
## 释放  
 如果未正确释放类，则会泄漏资源。  在混合应用程序中，请确保释放 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 和 <xref:System.Windows.Forms.Integration.ElementHost> 类，否则会泄漏资源。  [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]在 <xref:System.Windows.Forms.Integration.ElementHost> 控件的非模式 <xref:System.Windows.Forms.Form> 父级关闭时释放该控件。[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 在应用程序关闭时释放 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素。  可以在 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]消息循环的 <xref:System.Windows.Window> 中显示 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素。  在这种情况下，代码将无法收到有关正在关闭应用程序的通知。  
  
<a name="enabling_visual_styles"></a>   
## 启用视觉样式  
 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件上的 [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] 视觉样式可能未启用。  <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=fullName> 方法在 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]应用程序的模板中调用。  尽管默认情况下不会调用此方法，因此，如果您使用 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 创建项目，则会获得控件的 [!INCLUDE[TLA#tla_winxp](../../../../includes/tlasharptla-winxp-md.md)] 视觉样式，因此，如果Comctl32.dll版本6.0的可用。，在处理在线程之前，创建您必须调用 <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> 方法。  有关更多信息，请参见[如何：在混合应用程序中启用视觉样式](../../../../docs/framework/wpf/advanced/how-to-enable-visual-styles-in-a-hybrid-application.md)。  
  
<a name="licensed_controls"></a>   
## 授权控件  
 授权的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件会在消息框中向用户显示许可信息，对于混合应用程序，这可能会导致意外行为。  某些授权控件会显示一个对话框来响应创建句柄的操作。  例如，授权控件可能会通知用户需要许可证，或者用户还可以试用该控件三次。  
  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素派生自 <xref:System.Windows.Interop.HwndHost> 类，而子控件的句柄是在 <xref:System.Windows.Forms.Integration.WindowsFormsHost.BuildWindowCore%2A> 方法内部创建的。  <xref:System.Windows.Interop.HwndHost> 类不允许在 <xref:System.Windows.Forms.Integration.WindowsFormsHost.BuildWindowCore%2A> 方法中处理消息，但显示对话框会导致发送消息。  若要启用此许可方案，请在将该控件分配为 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素的子级之前，在该控件上调用 <xref:System.Windows.Forms.Control.CreateControl%2A?displayProperty=fullName> 方法。  
  
<a name="wpf_designer"></a>   
## WPF 设计器  
 通过使用 [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)]可以设计您的 WPF 内容。  以下各节将列出在使用 [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]创作混合应用程序时可能发生的一些常见问题。  
  
### 在设计时忽略 BackColorTransparent  
 <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> 属性可能不会起到设计时所预期的作用。  
  
 如果 WPF 控件不在可见的父级上，则 WPF 运行时将忽略 <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> 值。  忽略 <xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> 可能是因为在单独的 <xref:System.AppDomain> 中创建了 <xref:System.Windows.Forms.Integration.ElementHost> 对象。  但是，运行应用程序时，<xref:System.Windows.Forms.Integration.ElementHost.BackColorTransparent%2A> 不会起到预期的作用。  
  
### 删除 obj 文件夹时将出现设计时错误列表  
 如果删除 obj 文件夹，则将出现设计时错误列表。  
  
 使用 <xref:System.Windows.Forms.Integration.ElementHost> 进行设计时，Windows 窗体设计器将使用对象的 obj 文件夹内 Debug 或 Release 文件夹中所生成的文件。  如果删除这些文件，则将出现设计时错误列表。  若要解决此问题，请重新生成项目。  有关更多信息，请参见[Windows 窗体设计器中的设计时错误](../../../../docs/framework/winforms/controls/design-time-errors-in-the-windows-forms-designer.md)。  
  
<a name="elementhost_and_ime"></a>   
## ElementHost 和 IME  
 在 <xref:System.Windows.Forms.Integration.ElementHost> 中承载的 WPF 控件当前不支持 <xref:System.Windows.Forms.Control.ImeMode%2A> 属性。  所承载的控件将忽略对 <xref:System.Windows.Forms.Control.ImeMode%2A> 的更改。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [WPF 设计器中的互操作性](http://msdn.microsoft.com/zh-cn/2cb7c1ca-2a75-463b-8801-fba81e2b7042)   
 [Windows 窗体和 WPF 互操作性输入体系结构](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-interoperability-input-architecture.md)   
 [如何：在混合应用程序中启用视觉样式](../../../../docs/framework/wpf/advanced/how-to-enable-visual-styles-in-a-hybrid-application.md)   
 [WindowsFormsHost 元素的布局注意事项](../../../../docs/framework/wpf/advanced/layout-considerations-for-the-windowsformshost-element.md)   
 [Windows 窗体和 WPF 属性映射](../../../../docs/framework/wpf/advanced/windows-forms-and-wpf-property-mapping.md)   
 [Windows 窗体设计器中的设计时错误](../../../../docs/framework/winforms/controls/design-time-errors-in-the-windows-forms-designer.md)   
 [迁移和互操作性](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)