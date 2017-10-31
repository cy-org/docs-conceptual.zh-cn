---
title: "如何：获取或设置画布定位属性 | Microsoft Docs"
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
  - "Canvas 控件, 设置定位属性"
ms.assetid: 1636b950-2b5a-4507-8a10-c5034cc58b1c
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：获取或设置画布定位属性
下面的示例演示如何使用 <xref:System.Windows.Controls.Canvas> 元素的定位方法来定位子内容。  此示例使用 <xref:System.Windows.Controls.ListBoxItem> 中的内容来表示定位值，并将这些值转换为 <xref:System.Double>（定位时必需的参数）的实例。  然后，使用 <xref:System.Windows.Controls.Canvas.GetLeft%2A> 方法将这些值重新转换为字符串，并在 <xref:System.Windows.Controls.TextBlock> 元素中将其显示为文本。  
  
## 示例  
 下面的示例将创建具有十一个可选 <xref:System.Windows.Controls.ListBoxItem> 元素的 <xref:System.Windows.Controls.ListBox> 元素。  <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> 事件触发 `ChangeLeft` 自定义方法，后续代码块将定义该方法。  
  
 每个 <xref:System.Windows.Controls.ListBoxItem> 都表示一个 <xref:System.Double> 值，该值是 <xref:System.Windows.Controls.Canvas> 的 <xref:System.Windows.Controls.Canvas.SetLeft%2A> 方法可接受的参数之一。  要使用 <xref:System.Windows.Controls.ListBoxItem> 来表示 <xref:System.Double> 的实例，必须先将 <xref:System.Windows.Controls.ListBoxItem> 转换为正确的数据类型。  
  
 [!code-xml[CanvasPositioningProperties#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CanvasPositioningProperties/CSharp/Window1.xaml#1)]  
  
 当用户更改 <xref:System.Windows.Controls.ListBox> 选择时，将会调用 `ChangeLeft` 自定义方法。  此方法会将 <xref:System.Windows.Controls.ListBoxItem> 传递给 <xref:System.Windows.LengthConverter> 对象，该对象会将 <xref:System.Windows.Controls.ListBoxItem> 的 <xref:System.Windows.Controls.ContentControl.Content%2A> 转换为 <xref:System.Double> 的实例（请注意，已使用 <xref:System.Windows.Controls.Control.ToString%2A> 方法将此值转换为 <xref:System.String>）。  此值随后将回传给 <xref:System.Windows.Controls.Canvas> 的 <xref:System.Windows.Controls.Canvas.SetLeft%2A> 和 <xref:System.Windows.Controls.Canvas.GetLeft%2A> 方法，以便更改 `text1` 对象的位置。  
  
 [!code-csharp[CanvasPositioningProperties#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CanvasPositioningProperties/CSharp/Window1.xaml.cs#2)]
 [!code-vb[CanvasPositioningProperties#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasPositioningProperties/VisualBasic/Window1.xaml.vb#2)]  
  
## 请参阅  
 <xref:System.Windows.Controls.Canvas>   
 <xref:System.Windows.Controls.ListBoxItem>   
 <xref:System.Windows.LengthConverter>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)