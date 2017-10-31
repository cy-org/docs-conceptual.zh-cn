---
title: "Windows 窗体中的拖放功能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "拖放, Windows 窗体"
  - "Windows 窗体, 拖放"
ms.assetid: 65cd2c03-8782-474e-b958-cbe43eeb902c
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Windows 窗体中的拖放功能
Windows 窗体包含一组实现拖放行为的方法、事件和类。  本主题概述了 Windows 窗体对拖放功能的支持。  另请参阅[拖放操作和剪贴板支持](http://msdn.microsoft.com/library/fe5ebfwe\(v=vs.110\))。  
  
## 执行拖放操作  
 若要执行拖放操作，请使用 <xref:System.Windows.Forms.Control> 类的 <xref:System.Windows.Forms.Control.DoDragDrop%2A> 方法。  有关如何执行拖放操作的详细信息，请参阅 <xref:System.Windows.Forms.Control.DoDragDrop%2A>。  若要获取拖放操作开始前鼠标指针必须拖动到的矩形，请使用 <xref:System.Windows.Forms.SystemInformation> 类的 <xref:System.Windows.Forms.SystemInformation.DragSize%2A> 属性。  
  
## 与拖放操作相关的事件  
 拖放操作中有两类事件：一类是拖放操作的当前目标上发生的事件，一类是拖放操作的源上发生的事件。  
  
### 当前目标上的事件  
 下表显示在拖放操作的当前目标上发生的事件。  
  
|鼠标事件|描述|  
|----------|--------|  
|<xref:System.Windows.Forms.Control.DragEnter>|将对象拖入控件的边界时此事件发生。  此事件的处理程序接收类型为 <xref:System.Windows.Forms.DragEventArgs> 的参数。|  
|<xref:System.Windows.Forms.Control.DragOver>|在鼠标指针位于控件的边界内时如果拖动对象则此事件发生。  此事件的处理程序接收类型为 <xref:System.Windows.Forms.DragEventArgs> 的参数。|  
|<xref:System.Windows.Forms.Control.DragDrop>|拖放操作完成时此事件发生。  此事件的处理程序接收类型为 <xref:System.Windows.Forms.DragEventArgs> 的参数。|  
|<xref:System.Windows.Forms.Control.DragLeave>|将对象拖出控件的边界时此事件发生。  此事件的处理程序接收类型为 <xref:System.EventArgs> 的参数。|  
  
 <xref:System.Windows.Forms.DragEventArgs> 类提供鼠标指针的位置、鼠标按钮和键盘修改键的当前状态、正在拖动的数据以及 <xref:System.Windows.Forms.DragDropEffects> 值（指定拖动事件的源所允许的操作以及操作的目标放置效果）。  
  
### 源上的事件  
 下表显示在拖放操作的源上发生的事件。  
  
|鼠标事件|描述|  
|----------|--------|  
|<xref:System.Windows.Forms.Control.GiveFeedback>|此事件在执行拖动操作期间发生。  借助此事件，可向用户提供可视提示（例如更改鼠标指针），通知拖放操作正在发生。  此事件的处理程序接收类型为 <xref:System.Windows.Forms.GiveFeedbackEventArgs> 的参数。|  
|<xref:System.Windows.Forms.Control.QueryContinueDrag>|此事件在拖放操作期间引发，并使拖动源可以确定是否应取消拖放操作。  此事件的处理程序接收类型为 <xref:System.Windows.Forms.QueryContinueDragEventArgs> 的参数。|  
  
 <xref:System.Windows.Forms.QueryContinueDragEventArgs> 类提供鼠标按钮和键盘修改键的当前状态、指定是否按 ESC 键的值以及 <xref:System.Windows.Forms.DragAction> 值（可设置为指定是否应继续拖放操作）。  
  
## 请参阅  
 [Windows 窗体应用程序中的鼠标输入](../../../docs/framework/winforms/mouse-input-in-a-windows-forms-application.md)