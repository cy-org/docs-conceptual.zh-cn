---
title: "如何：指定自定义 Popup 位置 | Microsoft Docs"
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
  - "Popup 控件, 指定自定义位置"
ms.assetid: 28c24f39-d3aa-4ee2-b950-384b4a5dab92
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：指定自定义 Popup 位置
下面的示例演示当 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 属性设置为 <xref:System.Windows.Controls.Primitives.PlacementMode> 时，如何为 <xref:System.Windows.Controls.Primitives.Popup> 控件指定自定义位置。  
  
## 示例  
 当 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 属性设置为 <xref:System.Windows.Controls.Primitives.PlacementMode> 时，<xref:System.Windows.Controls.Primitives.Popup> 会调用为 <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> 委托定义的实例。  此委托返回一组可能的点，这些点相对于目标区域的左上角和 <xref:System.Windows.Controls.Primitives.Popup> 的左上角。  <xref:System.Windows.Controls.Primitives.Popup> 位置出现在可提供最佳可见性的点。  
  
 下面的示例演示如何通过将 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> 属性设置为 <xref:System.Windows.Controls.Primitives.PlacementMode> 来定义 <xref:System.Windows.Controls.Primitives.Popup> 的位置。  此示例还演示如何创建和分配 <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> 委托以定位 <xref:System.Windows.Controls.Primitives.Popup>。  该回调委托返回两个 <xref:System.Windows.Controls.Primitives.CustomPopupPlacement> 对象。  如果 <xref:System.Windows.Controls.Primitives.Popup> 在第一个位置被屏幕边缘隐藏，则 <xref:System.Windows.Controls.Primitives.Popup> 将放在第二个位置。  
  
 [!code-xml[PopupCustomPlacement#CustomPlacement](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PopupCustomPlacement/CSharp/Window1.xaml#customplacement)]  
  
 [!code-csharp[PopupCustomPlacement#DelegateInstance](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PopupCustomPlacement/CSharp/Window1.xaml.cs#delegateinstance)]
 [!code-vb[PopupCustomPlacement#DelegateInstance](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PopupCustomPlacement/visualbasic/window1.xaml.vb#delegateinstance)]  
  
 [!code-csharp[PopupCustomPlacement#DelegateDefinition](../../../../samples/snippets/csharp/VS_Snippets_Wpf/PopupCustomPlacement/CSharp/Window1.xaml.cs#delegatedefinition)]
 [!code-vb[PopupCustomPlacement#DelegateDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/PopupCustomPlacement/visualbasic/window1.xaml.vb#delegatedefinition)]  
  
 有关完整示例，请参见 [Popup Placement Sample](http://go.microsoft.com/fwlink/?LinkID=160032)（弹出项放置示例）。  
  
## 请参阅  
 <xref:System.Windows.Controls.Primitives.Popup>   
 [Popup 概述](../../../../docs/framework/wpf/controls/popup-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/controls/popup-how-to-topics.md)