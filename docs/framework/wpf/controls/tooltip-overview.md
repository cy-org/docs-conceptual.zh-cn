---
title: "ToolTip 概述 | Microsoft Docs"
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
  - "控件, ToolTip"
  - "ToolTip 控件, 关于 ToolTip 控件"
ms.assetid: f06c1603-e9cb-4809-8a62-234607fc52f7
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# ToolTip 概述
工具提示是用户将鼠标指针暂停在元素上（例如暂停在 <xref:System.Windows.Controls.Button> 上）时出现的小型弹出窗口。  本主题介绍工具提示并讨论如何创建和自定义工具提示内容。  
  
   
  
<a name="what_is_a_tooltip"></a>   
## 什么是工具提示？  
 当用户将鼠标指针移到具有工具提示的元素上时，包含工具提示内容（如描述控件功能的文本内容）的窗口将会出现，该窗口在经过指定的时间后将会消失。  如果用户从控件中移走鼠标指针，则该窗口将会消失，因为工具提示内容无法接收焦点。  
  
 工具提示的内容可以包含一个或多个文本行、图像、图形或其他可视内容。  通过将以下属性之一设置为工具提示内容，您可以为控件定义工具提示。  
  
-   <xref:System.Windows.FrameworkContentElement.ToolTip%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.FrameworkElement.ToolTip%2A?displayProperty=fullName>  
  
 所使用的属性取决于用于定义工具提示的控件是继承自 <xref:System.Windows.FrameworkContentElement> 类还是继承自 <xref:System.Windows.FrameworkElement> 类。  
  
<a name="create_tooltip"></a>   
## 创建工具提示  
 下面的示例演示如何通过将 <xref:System.Windows.Controls.Button> 控件的 <xref:System.Windows.FrameworkElement.ToolTip%2A> 属性设置为文本字符串来创建一个简单的工具提示。  
  
 [!code-xml[GroupBoxSnippet#ToolTipString](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GroupBoxSnippet/CS/Window1.xaml#tooltipstring)]  
  
 您也可以将工具提示定义为 <xref:System.Windows.Controls.ToolTip> 对象。  下面的示例使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 将 <xref:System.Windows.Controls.ToolTip> 对象指定为 <xref:System.Windows.Controls.TextBox> 元素的工具提示。  请注意，该示例通过设置 <xref:System.Windows.FrameworkElement.ToolTip%2A?displayProperty=fullName> 属性来指定 <xref:System.Windows.Controls.ToolTip>。  
  
 [!code-xml[ToolTipSimple#ToolTip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipSimple/CSharp/Pane1.xaml#tooltip)]  
  
 下面的示例使用代码来生成 <xref:System.Windows.Controls.ToolTip> 对象。  此示例创建一个 <xref:System.Windows.Controls.ToolTip> \(`tt`\) 并将它与 <xref:System.Windows.Controls.Button> 关联。  
  
 [!code-csharp[ToolTipSimple#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipSimple/CSharp/Pane1.xaml.cs#2)]
 [!code-vb[ToolTipSimple#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ToolTipSimple/VisualBasic/Window1.xaml.vb#2)]  
  
 通过将工具提示内容包括在布局元素（如 <xref:System.Windows.Controls.DockPanel>）中，您也可以创建未定义为 <xref:System.Windows.Controls.ToolTip> 对象的工具提示内容。  下面的示例演示如何将 <xref:System.Windows.Controls.TextBox> 的 <xref:System.Windows.FrameworkElement.ToolTip%2A> 属性设置为 <xref:System.Windows.Controls.DockPanel> 控件中所包含的内容。  
  
 [!code-xml[GroupBoxSnippet#ToolTipDockPanel](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GroupBoxSnippet/CS/Window1.xaml#tooltipdockpanel)]  
  
<a name="Using_the_ToolTip_and_ToolTipService_Properties"></a>   
## 使用 ToolTip 和 ToolTipService 类的属性  
 您可以通过设置可视属性并应用样式来自定义工具提示内容。  如果将工具提示内容定义为 <xref:System.Windows.Controls.ToolTip> 对象，则可以设置 <xref:System.Windows.Controls.ToolTip> 对象的可视属性。  否则，必须在 <xref:System.Windows.Controls.ToolTipService> 类上设置等效的[附加属性](GTMT)。  
  
 关于如何设置属性以使用 <xref:System.Windows.Controls.ToolTip> 和 <xref:System.Windows.Controls.ToolTipService> 属性指定工具提示内容的位置的示例，请参见[定位 ToolTip](../../../../docs/framework/wpf/controls/how-to-position-a-tooltip.md)。  
  
<a name="StylingToolTip"></a>   
## 设置 ToolTip 的样式  
 您可以通过定义一个自定义的 <xref:System.Windows.Style> 来设置 <xref:System.Windows.Controls.ToolTip> 的样式。  下面的示例定义了一个名为 `Simple` 的 <xref:System.Windows.Style>，它说明如何偏移 <xref:System.Windows.Controls.ToolTip> 的位置以及如何通过设置 <xref:System.Windows.Controls.Control.Background%2A>、<xref:System.Windows.Controls.Control.Foreground%2A>、<xref:System.Windows.Controls.Control.FontSize%2A> 和 <xref:System.Windows.Controls.Control.FontWeight%2A> 来更改其外观。  
  
 [!code-xml[ToolTipSimple#Style](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipSimple/CSharp/Pane1.xaml#style)]  
  
<a name="UsingtheToolTipServiceTimeIntervalProperties"></a>   
## 使用 ToolTipService 的时间间隔属性  
 <xref:System.Windows.Controls.ToolTipService> 类提供以下属性供您设置工具提示的显示时间：<xref:System.Windows.Controls.ToolTipService.InitialShowDelay%2A>、<xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A> 和 <xref:System.Windows.Controls.ToolTipService.ShowDuration%2A>。  
  
 使用 <xref:System.Windows.Controls.ToolTipService.InitialShowDelay%2A> 和 <xref:System.Windows.Controls.ToolTipService.ShowDuration%2A> 属性指定 <xref:System.Windows.Controls.ToolTip> 出现之前的延迟时间（通常很短），并指定 <xref:System.Windows.Controls.ToolTip> 保持可见的时间长度。  有关更多信息，请参见[How to: Delay the Display of a ToolTip](http://msdn.microsoft.com/zh-cn/618e05ef-f2bf-4a53-a0f4-aacb49918bd7)。  
  
 <xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A> 属性决定了在不同控件之间快速移动鼠标指针时，是否不经历初始延迟便可显示这些控件的工具提示。  有关 <xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A> 属性的更多信息，请参见 [使用 BetweenShowDelay 属性](../../../../docs/framework/wpf/controls/how-to-use-the-betweenshowdelay-property.md)。  
  
 下面的示例演示如何设置工具提示的这些属性。  
  
 [!code-xml[ToolTipService#ToolTip](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#tooltip)]  
  
## 请参阅  
 <xref:System.Windows.Controls.ToolTipService>   
 <xref:System.Windows.Controls.ToolTip>   
 <xref:System.Windows.Controls.ToolTipEventArgs>   
 <xref:System.Windows.Controls.ToolTipEventHandler>   
 [帮助主题](../../../../docs/framework/wpf/controls/tooltip-how-to-topics.md)