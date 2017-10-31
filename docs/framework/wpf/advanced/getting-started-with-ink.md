---
title: "墨迹入门 | Microsoft Docs"
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
  - "动画, 渐变画笔颜色"
  - "画笔, 对颜色进行动画处理"
  - "渐变画笔, 对颜色进行动画处理"
  - "替代 XAML 的程序代码"
  - "XAML, 程序代码替代"
ms.assetid: 760332dd-594a-475d-865b-01659db8cab7
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 墨迹入门
将数字墨迹集成到应用程序要比以往更容易。  墨迹已从 COM 和 Windows 窗体编程方法的必然结果，发展到实现与 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的完全集成。  您无需安装单独的 SDK 或运行库。  
  
## 必备组件  
 若要使用下面的示例，首先必须安装 Microsoft Visual Studio 2005 和 [!INCLUDE[TLA2#tla_winfxsdk](../../../../includes/tla2sharptla-winfxsdk-md.md)]。  还应了解如何编写 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序。  有关 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 入门的更多信息，请参见 [演练：开始使用 WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)。  
  
## 快速入门  
 本节帮助您编写一个简单的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序以收集墨迹。  
  
 如果您尚未安装 Microsoft Visual Studio 2005 和 [!INCLUDE[TLA#tla_winfxsdk](../../../../includes/tlasharptla-winfxsdk-md.md)]，请先安装。  通常，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序必须先编译才能查看，即使应用程序完全由[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 构成也应如此。  但是，[!INCLUDE[TLA#tla_winfxsdk](../../../../includes/tlasharptla-winfxsdk-md.md)] 包括一个专为加快基于 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 的 UI 的实现过程而设计的应用程序 XamlPad。  您可以使用该应用程序来查看和修补本文档中的前几个示例。  本文档后面将介绍如何从 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 创建已编译应用程序。  
  
 若要启动 XAMLPad，请单击**“开始”**菜单，依次指向**“所有程序”**、**“Microsoft Winndows SDK”**、**“工具”**，然后单击**“XAMLPad”**。  在呈现窗格中，XAMLPad 会呈现在代码窗格中编写的 XAML 代码。  您可以编辑 XAML 代码，更改会立即显示在呈现窗格中。  
  
#### 如何获取墨迹  
 若要启动支持墨迹的第一个 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序，请执行以下操作：  
  
1.  打开 Microsoft Visual Studio 2005。  
  
2.  创建一个新的**“Windows 应用程序 \(WPF\)”**。  
  
3.  在 `<Grid>` 标记之间键入 `<InkCanvas/>`。  
  
4.  按**“F5”**在调试器中启动应用程序。  
  
5.  使用触笔或鼠标，在窗口中写下 hello world。  
  
 您仅用 12 次击键就编写了与“hello world”应用程序等效的墨迹！  
  
#### 增强您的应用程序  
 下面来使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的某些功能。  用以下标记替换开始标记 \<Window\> 和结束标记 \<\/Window\> 之间的所有内容，以在墨迹图面上取得渐变画笔背景。  
  
 [!code-xml[DigitalInkTopics#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml#1)]  
[!code-xml[DigitalInkTopics#1a](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml#1a)]  
  
#### 使用动画  
 为了提高趣味性，下面我们对渐变画笔的颜色进行动画处理。  在结束标记 `</InkCanvas>` 之后，结束标记 `</Page>` 之前添加以下 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]。  
  
 [!code-xml[DigitalInkTopics#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml#2)]  
  
#### 在 XAML 后添加一些代码  
 虽然 XAML 使设计用户界面变得非常简单，但任何实际的应用程序都需要添加代码来处理事件。  以下是一个简单的示例，用于在用户右击鼠标时放大墨迹：  
  
 在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中设置 `MouseRightButtonUp` 处理程序：  
  
 [!code-xml[DigitalInkTopics#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#3)]  
  
 在 Visual Studio 的解决方案资源管理器中，展开 Windows1.xaml 并打开代码隐藏文件 Window1.xaml.cs 或 Window1.xaml.vb（如果使用 Visual Basic）。  添加以下事件处理程序代码：  
  
 [!code-csharp[DigitalInkTopics#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml.cs#4)]
 [!code-vb[DigitalInkTopics#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window2.xaml.vb#4)]  
  
 现在，运行应用程序。  添加一些墨迹，然后右击鼠标或执行与触笔等效的按压操作。  
  
#### 使用过程代码替代 XAML  
 可以从过程代码访问所有 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 功能。  以下是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的“Hello Ink World”应用程序，其中未使用任何 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]。  将以下代码粘贴到 Visual Studio 中空的控制台应用程序。  添加对 PresentationCore、PresentationFramework 和 WindowsBase 程序集的引用，然后按**“F5”**生成应用程序：  
  
 [!code-csharp[InkCanvasConsoleApp#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasConsoleApp/CSharp/Program.cs#1)]
 [!code-vb[InkCanvasConsoleApp#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/InkCanvasConsoleApp/VisualBasic/Module1.vb#1)]  
  
## 请参阅  
 [数字墨迹](../../../../docs/framework/wpf/advanced/digital-ink.md)   
 [收集墨迹](../../../../docs/framework/wpf/advanced/collecting-ink.md)   
 [手写识别](../../../../docs/framework/wpf/advanced/handwriting-recognition.md)   
 [存储墨迹](../../../../docs/framework/wpf/advanced/storing-ink.md)