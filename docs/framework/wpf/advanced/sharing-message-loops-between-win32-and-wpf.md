---
title: "在 Win32 和 WPF 之间共享消息循环 | Microsoft Docs"
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
  - "互操作性 [WPF], Win32"
  - "消息循环 [WPF]"
  - "共享消息循环"
  - "Win32 代码, 共享消息循环"
ms.assetid: 39ee888c-e5ec-41c8-b11f-7b851a554442
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 在 Win32 和 WPF 之间共享消息循环
本主题介绍如何通过使用 <xref:System.Windows.Threading.Dispatcher> 中公开的现有消息循环，或者通过在互操作代码的 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 一端创建单独的消息循环来实现消息循环，以便与 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 进行互操作。  
  
## ComponentDispatcher 和消息循环  
 互操作和键盘事件支持的一般方案是实现 <xref:System.Windows.Interop.IKeyboardInputSink>，或者从已经实现 <xref:System.Windows.Interop.IKeyboardInputSink> 的类（如 <xref:System.Windows.Interop.HwndSource> 和 <xref:System.Windows.Interop.HwndHost>）创建子类。  但是，键盘接收器支持不能解决您在通过互操作边界发送和接收消息时产生的所有可能的消息循环需要。  为了帮助规范化应用程序消息循环体系结构，[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供了 <xref:System.Windows.Interop.ComponentDispatcher> 类，它为消息循环定义了一个必须遵循的简单协议。  
  
 <xref:System.Windows.Interop.ComponentDispatcher> 是一个可公开若干成员的静态类。  每个方法的范围都隐式依赖于调用线程。  消息循环必须在关键时刻（如下一节所定义）调用某些 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)]。  
  
 <xref:System.Windows.Interop.ComponentDispatcher> 提供了其他组件（如键盘接收器）可以侦听的事件。  <xref:System.Windows.Threading.Dispatcher> 类按照正确的顺序调用所有适用的 <xref:System.Windows.Interop.ComponentDispatcher> 方法。  如果您要实现自己的消息循环，您的代码需要以类似的方式调用 <xref:System.Windows.Interop.ComponentDispatcher> 方法。  
  
 在线程上调用 <xref:System.Windows.Interop.ComponentDispatcher> 方法将只会调用在该线程上注册的事件处理程序。  
  
## 编写消息循环  
 下面是编写您自己的消息循环时将要使用的 <xref:System.Windows.Interop.ComponentDispatcher> 成员检查表：  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.PushModal%2A>：您的消息循环应调用此成员，以指明线程是模式线程。  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.PopModal%2A>：您的消息循环应调用此成员，以指明线程已还原为非模式线程。  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.RaiseIdle%2A>：消息循环应调用此成员，以指明 <xref:System.Windows.Interop.ComponentDispatcher> 应引发 <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle> 事件。  如果 <xref:System.Windows.Interop.ComponentDispatcher.IsThreadModal%2A> 为 `true`，<xref:System.Windows.Interop.ComponentDispatcher> 将不会引发 <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle>，但即使 <xref:System.Windows.Interop.ComponentDispatcher> 无法在模式状态下响应该事件，消息循环也可以选择调用 <xref:System.Windows.Interop.ComponentDispatcher.RaiseIdle%2A>。  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.RaiseThreadMessage%2A>：您的消息循环应调用此成员，以指明具有新消息。  返回值指明 <xref:System.Windows.Interop.ComponentDispatcher> 事件的侦听器是否处理了该消息。  如果 <xref:System.Windows.Interop.ComponentDispatcher.RaiseThreadMessage%2A> 返回 `true`（已处理），则调度程序不应再对消息进行任何进一步的处理。  如果返回值为 `false`，则调度程序应调用 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 函数 `TranslateMessage`，然后调用 `DispatchMessage`。  
  
## 使用 ComponentDispatcher 和现有消息处理  
 如果您依赖固有的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 消息循环，下面是您要使用的 <xref:System.Windows.Interop.ComponentDispatcher> 成员检查表。  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.IsThreadModal%2A>：返回应用程序是否已进入模式状态（例如，已推入模式消息循环）。  <xref:System.Windows.Interop.ComponentDispatcher> 可以跟踪此状态，因为该类维护来自消息循环的 <xref:System.Windows.Interop.ComponentDispatcher.PushModal%2A> 和 <xref:System.Windows.Interop.ComponentDispatcher.PopModal%2A> 调用的计数。  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage> 和 <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> 事件按照标准规则进行委托调用。  委托按照未指定的顺序进行调用，而所有委托都将得到调用，即使第一个委托将消息标记为已处理时也将如此。  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle>：指示执行闲置处理（线程没有其他挂起的消息）的适当有效的时间。  如果线程是模式线程，将不会引发 <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle>。  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage>：针对消息泵处理的所有消息引发。  
  
-   <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage>：为 <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage> 期间尚未处理的所有消息引发。  
  
 如果在 <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage> 事件和 <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> 事件后，事件数据中的引用传递的 `handled` 参数为 `true`，即认为消息已被处理。  如果 `handled` 为 `true`，事件处理程序应忽略该消息，因为这表示不同的处理程序已首先处理该消息。  两个事件的事件处理程序都可以修改该消息。  调度程序应调度修改后的消息，而不是未修改的原始消息。  <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> 虽然提供给所有侦听器，但体系结构的意图是，只有包含消息针对的 HWND 的顶级窗口才应调用代码以响应该消息。  
  
## HwndSource 如何处理 ComponentDispatcher 事件  
 如果 <xref:System.Windows.Interop.HwndSource> 是顶级窗口（没有父 HWND），它将在 <xref:System.Windows.Interop.ComponentDispatcher> 中注册。  如果引发了 <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage>，并且如果该消息针对的是 <xref:System.Windows.Interop.HwndSource> 或子窗口，则 <xref:System.Windows.Interop.HwndSource> 将调用其 <xref:System.Windows.Interop.HwndSource.System%23Windows%23Interop%23IKeyboardInputSink%23TranslateAccelerator%2A>、<xref:System.Windows.Interop.IKeyboardInputSink.TranslateChar%2A> 和 <xref:System.Windows.Interop.IKeyboardInputSink.OnMnemonic%2A> 键盘接收器序列。  
  
 如果 <xref:System.Windows.Interop.HwndSource> 不是顶级窗口（具有父 HWND），则将不会进行任何处理。  只有顶级窗口应执行处理，而任何互操作方案中都应该存在一个具有键盘接收器支持的顶级窗口。  
  
 如果在未调用相应的键盘接收器方法之前对 <xref:System.Windows.Interop.HwndSource> 调用了 <xref:System.Windows.Interop.HwndHost.WndProc%2A>，您的应用程序将收到更高级别的键盘事件，如 <xref:System.Windows.UIElement.KeyDown>。  但是，不会调用任何键盘接收器方法，从而避开了所需的键盘输入模型功能，如快捷键支持。  发生这种情况可能是因为消息循环未正确通知 <xref:System.Windows.Interop.ComponentDispatcher> 上的相关线程，或者父 HWND 未调用相应的键盘接收器响应。  
  
 如果您使用 <xref:System.Windows.Interop.HwndSource.AddHook%2A> 方法为传递给键盘接收器的消息添加了挂钩，该消息可能不会发送给 HWND。  该消息可能已直接在消息泵级进行了处理，而未提交给 `DispatchMessage` 函数。  
  
## 请参阅  
 <xref:System.Windows.Interop.ComponentDispatcher>   
 <xref:System.Windows.Interop.IKeyboardInputSink>   
 [WPF 和 Win32 互操作](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)   
 [线程处理模型](../../../../docs/framework/wpf/advanced/threading-model.md)   
 [输入概述](../../../../docs/framework/wpf/advanced/input-overview.md)