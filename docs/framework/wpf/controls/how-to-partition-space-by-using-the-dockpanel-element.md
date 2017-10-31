---
title: "如何：使用 DockPanel 元素对空间进行分区 | Microsoft Docs"
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
  - "DockPanel 控件, 空间分区"
  - "空间分区"
ms.assetid: a219b9e5-b205-4438-89b5-0a137ac463ab
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用 DockPanel 元素对空间进行分区
下面的示例使用 <xref:System.Windows.Controls.DockPanel> 元素创建一个简单的[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 框架。  <xref:System.Windows.Controls.DockPanel> 将可用空间分给其子元素。  
  
## 示例  
 此示例使用 <xref:System.Windows.Controls.DockPanel.Dock%2A> 属性（该属性为[附加属性](GTMT)）将两个相同的 <xref:System.Windows.Controls.Border> 元素停靠在已分区空间的 <xref:System.Windows.Controls.Dock> 处。  第三个 <xref:System.Windows.Controls.Border> 元素停靠在 <xref:System.Windows.Controls.Dock>，其宽度设置为 200 像素。  第四个 <xref:System.Windows.Controls.Border> 停靠在屏幕的 <xref:System.Windows.Controls.Dock>。  最后一个 <xref:System.Windows.Controls.Border> 元素自动填满剩余的空间。  
  
 [!code-cpp[DockPanelOvwSample#1](../../../../samples/snippets/cpp/VS_Snippets_Wpf/DockPanelOvwSample/CPP/DockPanel_Ovw_Sample.cpp#1)]
 [!code-csharp[DockPanelOvwSample#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DockPanelOvwSample/CSharp/DockPanel_Ovw_Sample.cs#1)]
 [!code-vb[DockPanelOvwSample#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DockPanelOvwSample/VisualBasic/dockpanel_vb.vb#1)]
 [!code-xml[DockPanelOvwSample#1](../../../../samples/snippets/xaml/VS_Snippets_Wpf/DockPanelOvwSample/XAML/default.xaml#1)]  
  
> [!NOTE]
>  默认情况下，<xref:System.Windows.Controls.DockPanel> 元素的最后一个子项将填满剩余的未分配空间。  如果不希望出现此行为，请设置 `LastChildFill="False"`。  
  
 编译后的应用程序将生成如下所示的新 UI。  
  
 ![典型的 DockPanel 方案。](../../../../docs/framework/wpf/controls/media/panel-intro-dockpanel.png "panel\_intro\_dockpanel")  
  
## 请参阅  
 <xref:System.Windows.Controls.DockPanel>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)