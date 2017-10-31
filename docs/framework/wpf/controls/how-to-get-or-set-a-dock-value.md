---
title: "如何：获取或设置 Dock 值 | Microsoft Docs"
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
  - "Dock 值, 获取"
  - "Dock 值, 设置"
ms.assetid: fcf4ab8a-c7cd-4835-8d04-de1c999ab4a8
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：获取或设置 Dock 值
下面的示例演示如何为对象赋予 <xref:System.Windows.Controls.Dock> 值。  此示例使用 <xref:System.Windows.Controls.DockPanel> 的 <xref:System.Windows.Controls.DockPanel.GetDock%2A> 和 <xref:System.Windows.Controls.DockPanel.SetDock%2A> 方法。  
  
## 示例  
 此示例创建 <xref:System.Windows.Controls.TextBlock> 元素的实例 `txt1`，并使用 <xref:System.Windows.Controls.DockPanel> 的 <xref:System.Windows.Controls.DockPanel.SetDock%2A> 方法赋给 <xref:System.Windows.Controls.Dock> 值 `Top`。  然后，该示例使用 <xref:System.Windows.Controls.DockPanel.GetDock%2A> 方法将 <xref:System.Windows.Controls.Dock> 属性的值附加到 <xref:System.Windows.Controls.TextBlock> 元素的 <xref:System.Windows.Controls.TextBlock.Text%2A>。  最后，该示例将 <xref:System.Windows.Controls.TextBlock> 元素添加到父 <xref:System.Windows.Controls.DockPanel> `dp1`。  
  
 [!code-csharp[DockPanelSetDock#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DockPanelSetDock/CSharp/DockPanel_SetDock.cs#1)]
 [!code-vb[DockPanelSetDock#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DockPanelSetDock/VisualBasic/DockPanel_SetDock.vb#1)]  
  
## 请参阅  
 <xref:System.Windows.Controls.DockPanel>   
 <xref:System.Windows.Controls.DockPanel.GetDock%2A>   
 <xref:System.Windows.Controls.DockPanel.SetDock%2A>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)