---
title: "如何：使用 Thumb 调整画布的大小 | Microsoft Docs"
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
  - "Canvas 控件"
  - "控件, Canvas"
  - "控件, Thumb"
  - "调整 Canvas 控件大小"
  - "Thumb 控件"
ms.assetid: 7dc9f435-726c-4d4d-be41-eb24cfe17bef
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：使用 Thumb 调整画布的大小
本示例演示如何使用 <xref:System.Windows.Controls.Primitives.Thumb> 控件来调整 <xref:System.Windows.Controls.Canvas> 控件的大小。  
  
## 示例  
 <xref:System.Windows.Controls.Primitives.Thumb> 控件提供了拖动功能，可以使用该功能，通过监控 <xref:System.Windows.Controls.Primitives.Thumb> 的 <xref:System.Windows.Controls.Primitives.Thumb.DragStarted>、<xref:System.Windows.Controls.Primitives.Thumb.DragDelta> 和 <xref:System.Windows.Controls.Primitives.Thumb.DragCompleted> 事件来移动控件或调整控件大小。  
  
 将鼠标指针停放在 <xref:System.Windows.Controls.Primitives.Thumb> 控件上后，用户可通过按住鼠标左键开始拖动操作。  只要一直按住鼠标左键，拖动操作就连续进行。  在拖动操作过程中，<xref:System.Windows.Controls.Primitives.Thumb.DragDelta> 可能会发生多次。  每次发生时，<xref:System.Windows.Controls.Primitives.DragDeltaEventArgs> 类都会根据鼠标位置的变化相应地更改位置。  用户松开鼠标左键后，拖动操作即完成。  拖动操作只提供新坐标；它不会自动重新改变 <xref:System.Windows.Controls.Primitives.Thumb> 的位置。  
  
 下面的示例说明 <xref:System.Windows.Controls.Primitives.Thumb> 控件是 <xref:System.Windows.Controls.Canvas> 控件的子元素。  其 <xref:System.Windows.Controls.Primitives.Thumb.DragDelta> 事件的事件处理程序提供了用于移动 <xref:System.Windows.Controls.Primitives.Thumb> 和调整 <xref:System.Windows.Controls.Canvas> 大小的逻辑。  <xref:System.Windows.Controls.Primitives.Thumb.DragStarted> 和 <xref:System.Windows.Controls.Primitives.Thumb.DragCompleted> 事件的事件处理程序在拖动操作过程中更改 <xref:System.Windows.Controls.Primitives.Thumb> 的颜色。  下面的示例定义 <xref:System.Windows.Controls.Primitives.Thumb>。  
  
 [!code-xml[Thumb#thumb](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Thumb/CSharp/Pane1.xaml#thumb)]  
  
 下面的示例演示 <xref:System.Windows.Controls.Primitives.Thumb.DragDelta> 事件处理程序，该事件处理程序将移动 <xref:System.Windows.Controls.Primitives.Thumb> 和调整 <xref:System.Windows.Controls.Canvas> 大小以响应鼠标移动。  
  
 [!code-csharp[Thumb#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Thumb/CSharp/Pane1.xaml.cs#2)]  
  
 下面的示例演示 <xref:System.Windows.Controls.Primitives.Thumb.DragStarted> 事件处理程序。  
  
 [!code-csharp[Thumb#DragStartedHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Thumb/CSharp/Pane1.xaml.cs#dragstartedhandler)]
 [!code-vb[Thumb#DragStartedHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Thumb/VisualBasic/Pane1.xaml.vb#dragstartedhandler)]  
  
 下面的示例演示 <xref:System.Windows.Controls.Primitives.Thumb.DragCompleted> 事件处理程序。  
  
 [!code-csharp[Thumb#DragCompletedHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Thumb/CSharp/Pane1.xaml.cs#dragcompletedhandler)]
 [!code-vb[Thumb#DragCompletedHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Thumb/VisualBasic/Pane1.xaml.vb#dragcompletedhandler)]  
  
 有关完整示例，请参见 [Thumb Drag Functionality Sample](http://go.microsoft.com/fwlink/?LinkID=160042)（滚动块拖动功能示例）。  
  
## 请参阅  
 <xref:System.Windows.Controls.Primitives.Thumb>   
 <xref:System.Windows.Controls.Primitives.Thumb.DragStarted>   
 <xref:System.Windows.Controls.Primitives.Thumb.DragDelta>   
 <xref:System.Windows.Controls.Primitives.Thumb.DragCompleted>