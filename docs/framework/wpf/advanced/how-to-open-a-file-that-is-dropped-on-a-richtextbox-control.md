---
title: "如何：打开放置在 RichTextBox 控件上的文件 | Microsoft Docs"
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
  - "拖放 [WPF], 打开放置的文件"
  - "拖放 [WPF], RichTextBox"
  - "RichTextBox [WPF], 拖放"
ms.assetid: 6bb8bb54-f576-41db-a9a7-24102ddeb490
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：打开放置在 RichTextBox 控件上的文件
在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中，<xref:System.Windows.Controls.TextBox>、<xref:System.Windows.Controls.RichTextBox> 和 <xref:System.Windows.Documents.FlowDocument> 控件都具有内置拖放功能。  通过该内置功能，可在控件内和控件之间拖放文本。  但是，该功能不支持通过将文件放到控件上来打开文件。  这些控件还会将拖放事件标记为已处理。  因此，在默认情况下，您无法添加自己的事件处理程序以提供用于打开所放置文件的功能。  
  
 若要为这些控件中的拖放事件添加其他处理，请使用 <xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> 方法为拖放事件添加事件处理程序。  将 `handledEventsToo` 参数设置为 `true`，以便为已标记为由其他元素在事件路由过程中处理的路由事件调用指定的处理程序。  
  
> [!TIP]
>  可通过处理预览版本的拖放事件并将预览事件标记为已处理来替换 <xref:System.Windows.Controls.TextBox>、<xref:System.Windows.Controls.RichTextBox> 和 <xref:System.Windows.Documents.FlowDocument> 的内置拖放功能。  但是，此操作会禁用内置拖放功能，因此不建议执行此操作。  
  
## 示例  
 下面的示例演示如何为 <xref:System.Windows.Controls.RichTextBox> 上的 <xref:System.Windows.DragDrop.DragOver> 和 <xref:System.Windows.DragDrop.Drop> 事件添加处理程序。  此示例使用 <xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> 方法并将 `handledEventsToo` 参数设置为 `true`，这样，即使 <xref:System.Windows.Controls.RichTextBox> 将这些事件标记为已处理，也会调用这些事件处理程序。  事件处理程序中的代码可添加功能，用于打开放置到 <xref:System.Windows.Controls.RichTextBox> 上的文本文件。  
  
 若要测试此示例，请将一个文本文件或 RTF 格式文件从 Windows 资源管理器拖动到 <xref:System.Windows.Controls.RichTextBox>。  该文件将在 <xref:System.Windows.Controls.RichTextBox> 中打开。  如果在放置该文件前按 Shift 键，则该文件将以纯文本形式打开。  
  
 [!code-xml[DragDropSnippets#RtbXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml#rtbxaml)]  
  
 [!code-csharp[DragDropSnippets#RtbHandlers](../../../../samples/snippets/csharp/VS_Snippets_Wpf/dragdropsnippets/cs/mainwindow.xaml.cs#rtbhandlers)]
 [!code-vb[DragDropSnippets#RtbHandlers](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/dragdropsnippets/vb/mainwindow.xaml.vb#rtbhandlers)]