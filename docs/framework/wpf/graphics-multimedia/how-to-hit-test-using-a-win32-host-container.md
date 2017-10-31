---
title: "如何：使用 Win32 宿主容器执行命中测试 | Microsoft Docs"
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
  - "命中测试, 使用 Win32 宿主容器"
  - "可视化对象, 命中测试"
  - "Win32 宿主容器, 命中测试使用"
ms.assetid: 9491f7f3-d8ba-4573-a888-2f064d1349dc
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：使用 Win32 宿主容器执行命中测试
可以通过为可视化对象提供宿主窗口容器在 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 中创建可视化对象。  若要为包含的可视化对象提供事件处理，需要处理传递到宿主窗口容器的消息筛选器循环的消息。  有关如何在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口中承载可视化对象的更多信息，请参见[教程：在 Win32 应用程序中承载 Visual 对象](../../../../docs/framework/wpf/graphics-multimedia/tutorial-hosting-visual-objects-in-a-win32-application.md)。  
  
## 示例  
 下面的代码演示如何为用作可视化对象的宿主容器的 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 窗口设置鼠标事件处理程序。  
  
 [!code-csharp[VisualsHitTesting#103](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#103)]
 [!code-vb[VisualsHitTesting#103](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#103)]  
  
 下面的示例演示如何设置[命中测试](GTMT)来响应捕获特定的鼠标事件。  
  
 [!code-csharp[VisualsHitTesting#104](../../../../samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyCircle.cs#104)]
 [!code-vb[VisualsHitTesting#104](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyCircle.vb#104)]  
  
 <xref:System.Windows.Interop.HwndSource> 对象表示 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 窗口中的 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 内容。<xref:System.Windows.Interop.HwndSource> 对象的 <xref:System.Windows.Interop.HwndSource.RootVisual%2A> 属性的值表示[可视化树](GTMT)层次结构中的最顶层节点。  
  
 有关使用 Win32 宿主容器对对象进行命中测试的完整示例，请参见 [Hit Test with Win32 Interoperation Sample](http://go.microsoft.com/fwlink/?LinkID=159995)（Win32 交互命中测试示例）。  
  
## 请参阅  
 <xref:System.Windows.Interop.HwndSource>   
 [可视化层中的命中测试](../../../../docs/framework/wpf/graphics-multimedia/hit-testing-in-the-visual-layer.md)   
 [教程：在 Win32 应用程序中承载 Visual 对象](../../../../docs/framework/wpf/graphics-multimedia/tutorial-hosting-visual-objects-in-a-win32-application.md)