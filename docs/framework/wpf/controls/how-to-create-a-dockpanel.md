---
title: "如何：创建 DockPanel | Microsoft Docs"
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
  - "控件, DockPanel"
  - "DockPanel 控件, 创建"
ms.assetid: 9194f663-e279-4f1a-86d7-125a57d05c6f
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：创建 DockPanel
## 示例  
 下面的示例通过使用代码创建和使用 <xref:System.Windows.Controls.DockPanel> 的实例。  该示例演示如何通过创建五个 <xref:System.Windows.Shapes.Rectangle> 元素并将它们放在（停靠在）父 <xref:System.Windows.Controls.DockPanel> 的内部来对空间进行分区。  如果保留默认设置，最后一个矩形将填满所有剩余的未分配空间。  
  
 [!code-csharp[DockPanelCode#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DockPanelCode/CSharp/DockPanel_Code.cs#1)]
 [!code-vb[DockPanelCode#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DockPanelCode/VisualBasic/dockpanel_vb.vb#1)]  
  
## 请参阅  
 <xref:System.Windows.Controls.DockPanel>   
 <xref:System.Windows.Controls.Dock>   
 [面板概述](../../../../docs/framework/wpf/controls/panels-overview.md)