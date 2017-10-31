---
title: "如何：在 StackPanel 和 DockPanel 之间进行选择 | Microsoft Docs"
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
  - "控件 [WPF], DockPanel"
  - "控件 [WPF], StackPanel"
  - "DockPanel 控件, StackPanel 控件相较于"
  - "StackPanel 控件, DockPanel 控件相较于"
ms.assetid: f9239086-451f-42e6-81f7-ef89ef349742
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：在 StackPanel 和 DockPanel 之间进行选择
此示例演示在 <xref:System.Windows.Controls.Panel> 中堆叠内容时如何在使用 <xref:System.Windows.Controls.StackPanel> 或使用 <xref:System.Windows.Controls.DockPanel> 之间进行选择。  
  
## 示例  
 虽然可以使用 <xref:System.Windows.Controls.DockPanel> 或 <xref:System.Windows.Controls.StackPanel> 来堆叠子元素，但这两个控件并不总是会产生相同的结果。  例如，子元素的放置顺序可能会影响 <xref:System.Windows.Controls.DockPanel> 中子元素的大小，但不会影响 <xref:System.Windows.Controls.StackPanel> 中子元素的大小。  之所以会发生这种不同的行为，是因为 <xref:System.Windows.Controls.StackPanel> 在 <xref:System.Double>.<xref:System.Double.PositiveInfinity> 处朝着堆叠方向测量大小，但是，<xref:System.Windows.Controls.DockPanel> 只测量可用大小。  
  
 下面的示例演示 <xref:System.Windows.Controls.DockPanel> 和 <xref:System.Windows.Controls.StackPanel> 之间的此主要差异。  
  
 [!code-cpp[StackPanelOvw4#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/StackPanelOvw4/CPP/StackPanel_Ovw_Sample4.cpp#1)]
 [!code-csharp[StackPanelOvw4#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StackPanelOvw4/CSharp/StackPanel_Ovw_Sample4.cs#1)]
 [!code-vb[StackPanelOvw4#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StackPanelOvw4/VisualBasic/StackPanelSamp.vb#1)]
 [!code-xml[StackPanelOvw4#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/StackPanelOvw4/XAML/default.xaml#1)]  
  
## 请参阅  
 <xref:System.Windows.Controls.StackPanel>   
 <xref:System.Windows.Controls.DockPanel>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)