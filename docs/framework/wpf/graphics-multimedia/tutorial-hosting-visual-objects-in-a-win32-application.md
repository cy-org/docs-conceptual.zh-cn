---
title: "教程：在 Win32 应用程序中承载 Visual 对象 | Microsoft Docs"
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
  - "Hosting — 承载, Win32 代码中的可视化对象"
  - "Win32 代码中的可视化对象"
  - "Win32 代码, 可视化对象"
ms.assetid: f0e1600c-3217-43d5-875d-1864fa7fe628
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 教程：在 Win32 应用程序中承载 Visual 对象
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供用于创建应用程序的丰富环境。  但是，如果您在 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 代码上有大量的投资，则将 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 功能添加到应用程序而不是重写代码的做法或许会更有效。  为了为应用程序中并发使用的 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 图形子系统提供支持，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了一种承载 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口中的对象的机制。  
  
 本教程介绍如何编写示例应用程序 [Hit Test with Win32 Interoperation Sample](http://go.microsoft.com/fwlink/?LinkID=159995)（Win32 互操作命中测试示例），该应用程序在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口中承载 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 可使对象。  
  
   
  
<a name="requirements"></a>   
## 要求  
 本教程假定您基本熟悉 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 编程。  有关 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 编程的基本介绍，请参见 [演练：开始使用 WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)。  有关对 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 编程的介绍，请参见众多关于此主题书籍中的任何一本，特别推荐由 Charles Petzold 编写的 Programming Windows（《Windows 编程》）。  
  
> [!NOTE]
>  本教程包含关联示例中的一些代码示例。  但是，为了易读起见，本教程并不包含完整的代码示例。  有关完整代码示例，请参见 [Hit Test with Win32 Interoperation Sample](http://go.microsoft.com/fwlink/?LinkID=159995)（Win32 互操作命中测试示例）。  
  
<a name="creating_the_host_win32_window"></a>   
## 创建宿主 Win32 窗口  
 在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口中承载 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 对象的关键是 <xref:System.Windows.Interop.HwndSource> 类。  此类在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口中包装 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 对象，允许将它们作为子级窗口合并到[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 中。  
  
 下面的示例演示将 <xref:System.Windows.Interop.HwndSource> 对象作为 Visual 对象的 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 容器窗口进行创建的代码。  若要为 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口设置窗口的样式、位置和其他参数，请使用 <xref:System.Windows.Interop.HwndSourceParameters> 对象。  
  
 [!code-csharp[VisualsHitTesting#101](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#101)]
 [!code-vb[VisualsHitTesting#101](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#101)]  
  
> [!NOTE]
>  不能将 <xref:System.Windows.Interop.HwndSourceParameters.ExtendedWindowStyle%2A> 属性的值设置为 WS\_EX\_TRANSPARENT。  这意味着宿主 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口不能是透明的。  因此，宿主 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口的背景色将设置为与其父窗口相同的背景色。  
  
<a name="adding_visual_objects_to_the_host_win32_window"></a>   
## 将 Visual 对象添加到宿主 Win32 窗口  
 为 Visual 对象创建宿主 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 容器窗口后，可向其添加 Visual 对象。  如果需要确保如动画等的 Visual 对象的任何转换，扩展时请勿超出宿主 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口的边框。  
  
 下面的示例演示创建 <xref:System.Windows.Interop.HwndSource> 对象并向其中添加 Visual 对象的代码。  
  
> [!NOTE]
>  将 <xref:System.Windows.Interop.HwndSource> 对象的 <xref:System.Windows.Interop.HwndSource.RootVisual%2A> 属性设置为添加到宿主 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口的第一个 Visual 对象。  根 Visual 对象定义 Visual 对象树最顶层的节点。  任何添加到宿主 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口的后续 Visual 对象都作为子对象进行添加。  
  
 [!code-csharp[VisualsHitTesting#100](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#100)]
 [!code-vb[VisualsHitTesting#100](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#100)]  
  
<a name="implementing_the_win32_message_filter"></a>   
## 实现 Win32 消息筛选器  
 Visual 对象的宿主 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口需要窗口消息筛选器过程来处理从应用程序队列发送到该窗口的消息。  窗口过程接收来自 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 系统的消息。  这些消息可以为输入消息或窗口管理消息。  可以选择在窗口过程中处理消息或将消息传递到系统进行默认处理。  
  
 定义为 Visual 对象的父级的 <xref:System.Windows.Interop.HwndSource> 对象必须引用提供的窗口消息筛选器过程。  创建 <xref:System.Windows.Interop.HwndSource> 对象时，请将 <xref:System.Windows.Interop.HwndSourceParameters.HwndSourceHook%2A> 属性设置为引用窗口过程。  
  
 [!code-csharp[VisualsHitTesting#102](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#102)]
 [!code-vb[VisualsHitTesting#102](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#102)]  
  
 下面的示例演示处理释放鼠标左键和右键消息的代码。  鼠标命中位置的坐标值包含在 `lParam` 参数的值中。  
  
 [!code-csharp[VisualsHitTesting#103](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#103)]
 [!code-vb[VisualsHitTesting#103](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#103)]  
  
<a name="processing_the_win32_messages"></a>   
## 处理 Win32 消息  
 下面示例中的代码演示如何对包含在宿主 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口中的 Visual 对象的层次结构执行命中测试。  可以确定一个点是否处于 Visual 对象的几何图形之内，其方法是使用 <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> 方法指定进行命中测试的根 Visual 对象和坐标值。  在本例中，根 Visual 对象是 <xref:System.Windows.Interop.HwndSource> 对象的 <xref:System.Windows.Interop.HwndSource.RootVisual%2A> 属性的值。  
  
 [!code-csharp[VisualsHitTesting#104](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyCircle.cs#104)]
 [!code-vb[VisualsHitTesting#104](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyCircle.vb#104)]  
  
 有关对 Visual 对象进行命中测试的更多信息，请参见[可视化层中的命中测试](../../../../docs/framework/wpf/graphics-multimedia/hit-testing-in-the-visual-layer.md)。  
  
## 请参阅  
 <xref:System.Windows.Interop.HwndSource>   
 [Hit Test with Win32 Interoperation Sample](http://go.microsoft.com/fwlink/?LinkID=159995)   
 [可视化层中的命中测试](../../../../docs/framework/wpf/graphics-multimedia/hit-testing-in-the-visual-layer.md)