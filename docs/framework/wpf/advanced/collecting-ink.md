---
title: "收集墨迹 | Microsoft Docs"
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
  - "收集数字墨迹"
  - "DefaultDrawingAttributes 属性"
  - "数字墨迹, 收集"
  - "DrawingAttributes 属性"
  - "墨迹, 收集"
  - "InkCanvas 元素"
  - "属性, DefaultDrawingAttributes"
  - "属性, DrawingAttributes"
ms.assetid: 66a3129d-9577-43eb-acbd-56c147282016
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 收集墨迹
[Windows Presentation Foundation](../../../../docs/framework/wpf/index.md) 平台将收集数字墨迹作为其核心功能。  本主题讨论在 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 中收集墨迹的方法。  
  
## 必备组件  
 若要使用下面的示例，首先必须安装 [!INCLUDE[TLA#tla_visualstu2005](../../../../includes/tlasharptla-visualstu2005-md.md)] 和 [!INCLUDE[TLA2#tla_winfxsdk](../../../../includes/tla2sharptla-winfxsdk-md.md)]。  还应了解如何编写 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序。  有关 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 入门的更多信息，请参见 [演练：开始使用 WPF](../../../../docs/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application.md)。  
  
## 使用 InkCanvas 元素  
 <xref:System.Windows.Controls.InkCanvas> 元素提供了在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中收集墨迹的最简单方式。  <xref:System.Windows.Controls.InkCanvas> 元素类似于 [!INCLUDE[TLA2#tla_tpclssdk](../../../../includes/tla2sharptla-tpclssdk-md.md)] 及早期版本中的 <xref:Microsoft.Ink.InkOverlay> 对象。  
  
 使用 <xref:System.Windows.Controls.InkCanvas> 元素可接收和显示墨迹输入。  通常使用触笔（与数字化仪交互产生墨迹笔画）输入墨迹。  此外，还可以使用鼠标代替触笔。  创建的笔画表示为 <xref:System.Windows.Ink.Stroke> 对象，它们可以通过编程方式和用户输入方式进行操作。  <xref:System.Windows.Controls.InkCanvas> 允许用户选择、修改或删除现有的 <xref:System.Windows.Ink.Stroke>。  
  
 通过使用 XAML，可以像将 `InkCanvas` 元素添加到树中一样轻松地设置墨迹收集。  下面的示例将 <xref:System.Windows.Controls.InkCanvas> 添加到在 [!INCLUDE[TLA#tla_visualstu2005](../../../../includes/tlasharptla-visualstu2005-md.md)] 中创建的默认 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 项目。  
  
 [!code-xml[DigitalInkTopics#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#6)]  
  
 `InkCanvas` 元素也可以包含子元素，这样便可以将墨迹批注功能添加到几乎所有类型的 XAML 元素。  例如，若要将墨迹功能添加到文本元素，只需使其成为 <xref:System.Windows.Controls.InkCanvas> 的子元素即可。  
  
 [!code-xml[DigitalInkTopics#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#5)]  
  
 可轻松添加对使用墨迹标记图像的支持。  
  
 [!code-xml[DigitalInkTopics#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window2.xaml#7)]  
  
### InkCollection 模式  
 <xref:System.Windows.Controls.InkCanvas> 通过其 <xref:System.Windows.Controls.InkCanvas.EditingMode%2A> 属性对各种输入模式提供支持。  
  
### 操作墨迹  
 <xref:System.Windows.Controls.InkCanvas> 对多种墨迹编辑操作提供支持。  例如，<xref:System.Windows.Controls.InkCanvas> 支持笔清除功能，不需要其他代码来将该功能添加到该元素。  
  
#### Selection  
 设置选择模式与将 <xref:System.Windows.Controls.InkCanvasEditingMode> 属性设置为 **Select** 一样容易。  下面的代码根据 <xref:System.Windows.Forms.CheckBox> 的值来设置编辑模式。  
  
 [!code-csharp[DigitalInkTopics#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#8)]
 [!code-vb[DigitalInkTopics#8](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#8)]  
  
#### DrawingAttributes  
 使用 <xref:System.Windows.Ink.Stroke.DrawingAttributes%2A> 属性可更改墨迹笔画的外观。  例如，<xref:System.Windows.Ink.DrawingAttributes> 的 <xref:System.Windows.Ink.DrawingAttributes.Color%2A> 成员可设置呈现的 <xref:System.Windows.Ink.Stroke> 的颜色。  下面的示例将所选笔画的颜色更改为红色。  
  
 [!code-csharp[DigitalInkTopics#9](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DigitalInkTopics/CSharp/Window1.xaml.cs#9)]
 [!code-vb[DigitalInkTopics#9](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DigitalInkTopics/VisualBasic/Window1.xaml.vb#9)]  
  
### DefaultDrawingAttributes  
 <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A> 属性可提供对在 <xref:System.Windows.Controls.InkCanvas> 中创建的笔画的高度、宽度和颜色等属性的访问。  一旦更改 <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>，则以后输入 <xref:System.Windows.Controls.InkCanvas> 中的所有笔画都将使用新的属性值呈现。  
  
 除了在代码隐藏文件中修改 <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A> 外，还可以使用 XAML 语法指定 <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A> 属性。  下面的 XAML 代码演示如何设置 <xref:System.Windows.Ink.DrawingAttributes.Color%2A> 属性。  若要使用此代码，请在 Visual Studio 2005 中创建名为“HelloInkCanvas”的新 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 项目。  使用下面的代码替换 Window1.xaml 文件中的代码。  
  
 [!code-xml[HelloInkCanvas#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HelloInkCanvas/CSharp/Window1.xaml#1)]  
  
 然后，将以下按钮事件处理程序添加到 Window1 类中的代码隐藏文件。  
  
 [!code-csharp[HelloInkCanvas#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HelloInkCanvas/CSharp/Window1.xaml.cs#2)]  
  
 复制此代码后，在 Microsoft Visual Studio 2005 中按**“F5”**，在调试器中运行该程序。  
  
 请注意 <xref:System.Windows.Controls.StackPanel> 是如何将按钮放在 <xref:System.Windows.Controls.InkCanvas> 顶部的。  如果尝试收集这些按钮顶部的墨迹，那么 <xref:System.Windows.Controls.InkCanvas> 将收集并呈现按钮后面的墨迹。  这是因为这些按钮是 <xref:System.Windows.Controls.InkCanvas> 的同级，而不是子级。  此外，这些按钮的 Z 顺序较高，所以墨迹呈现在其后面。  
  
## 请参阅  
 <xref:System.Windows.Ink.DrawingAttributes>   
 <xref:System.Windows.InkCanvas.DefaultDrawingAttributes%2A>   
 <xref:System.Windows.Ink>