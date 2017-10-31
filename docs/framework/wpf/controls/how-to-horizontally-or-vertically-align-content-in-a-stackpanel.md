---
title: "如何：在 StackPanel 中水平或垂直对齐内容 | Microsoft Docs"
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
  - "对齐, 内容"
  - "内容对齐"
  - "StackPanel 控件, 内容对齐"
ms.assetid: c1e8f962-72c8-4e7a-8670-7a2d7e021791
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：在 StackPanel 中水平或垂直对齐内容
此示例演示如何调整 <xref:System.Windows.Controls.StackPanel> 元素中内容的 <xref:System.Windows.Controls.StackPanel.Orientation%2A>，以及如何调整子内容的 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 和 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>。  
  
## 示例  
 下面的示例在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中创建三个 <xref:System.Windows.Controls.ListBox> 元素。  每个 <xref:System.Windows.Controls.ListBox> 都代表 <xref:System.Windows.Controls.StackPanel> 的 <xref:System.Windows.Controls.StackPanel.Orientation%2A>、<xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 和 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A> 属性的可能值。  如果用户选择了任何一个 <xref:System.Windows.Controls.ListBox> 元素中的值，则 <xref:System.Windows.Controls.StackPanel> 的关联属性及其子 <xref:System.Windows.Controls.Button> 元素将会发生变化。  
  
 [!code-xml[StackPanelIntroSamp#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StackPanelIntroSamp/CSharp/Window1.xaml#1)]  
  
 以下代码隐藏文件定义了与 <xref:System.Windows.Controls.ListBox> 所选内容更改关联的事件更改。  <xref:System.Windows.Controls.StackPanel> 由 <xref:System.Windows.FrameworkElement.Name%2A> `sp1` 标识。  
  
 [!code-csharp[StackPanelIntroSamp#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StackPanelIntroSamp/CSharp/Window1.xaml.cs#2)]
 [!code-vb[StackPanelIntroSamp#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanelIntroSamp/VisualBasic/Window1.xaml.vb#2)]  
  
## 请参阅  
 <xref:System.Windows.Controls.StackPanel>   
 <xref:System.Windows.Controls.ListBox>   
 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>   
 <xref:System.Windows.FrameworkElement.VerticalAlignment%2A>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)