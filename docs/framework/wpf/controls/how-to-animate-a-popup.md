---
title: "如何：对 Popup 进行动画处理 | Microsoft Docs"
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
  - "动画, Popup 控件"
  - "Popup 控件, 动画处理"
ms.assetid: acaa2a0a-6137-4efd-9cd1-75ece222e390
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：对 Popup 进行动画处理
本示例演示对 <xref:System.Windows.Controls.Primitives.Popup> 控件进行动画处理的两种方法。  
  
## 示例  
 下面的示例将 <xref:System.Windows.Controls.Primitives.PopupAnimation> 属性设置为 <xref:System.Windows.Controls.Primitives.PopupAnimation> 值，这会导致 <xref:System.Windows.Controls.Primitives.Popup> 以“滑入”的方式出现。  
  
 为了旋转 <xref:System.Windows.Controls.Primitives.Popup>，本示例将 <xref:System.Windows.Media.RotateTransform> 指定给 <xref:System.Windows.Controls.Primitives.Popup> 的子元素 <xref:System.Windows.Controls.Canvas> 的 <xref:System.Windows.UIElement.RenderTransform%2A> 属性。  
  
 为了使变换正确工作，本示例必须将 <xref:System.Windows.Controls.Primitives.Popup.AllowsTransparency%2A> 属性设置为 `true`。  此外，<xref:System.Windows.Controls.Canvas> 内容的 <xref:System.Windows.FrameworkElement.Margin%2A> 还必须指定足够的空间来供 <xref:System.Windows.Controls.Primitives.Popup> 旋转。  
  
 [!code-xml[AnimatedPopup#RotateTransform2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimatedPopup/CS/Window1.xaml#rotatetransform2)]  
  
 下面的示例演示单击某个 <xref:System.Windows.Controls.Button> 时发生的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件如何触发 <xref:System.Windows.Media.Animation.Storyboard> 以启动动画。  
  
 [!code-xml[AnimatedPopup#RotateTransform1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/AnimatedPopup/CS/Window1.xaml#rotatetransform1)]  
  
## 请参阅  
 <xref:System.Windows.UIElement.RenderTransform%2A>   
 <xref:System.Windows.Controls.Primitives.BulletDecorator>   
 <xref:System.Windows.Media.RotateTransform>   
 <xref:System.Windows.Media.Animation.Storyboard>   
 <xref:System.Windows.Controls.Primitives.Popup>   
 [帮助主题](../../../../docs/framework/wpf/controls/popup-how-to-topics.md)   
 [Popup 概述](../../../../docs/framework/wpf/controls/popup-overview.md)