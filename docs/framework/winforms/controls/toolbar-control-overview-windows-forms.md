---
title: "ToolBar 控件概述（Windows 窗体） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ToolBar"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "ToolBar 控件 [Windows 窗体], 关于工具栏控件"
  - "工具栏 [Windows 窗体], 关于工具栏"
ms.assetid: d426b203-0216-4dbe-b834-1641e50a9c29
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# ToolBar 控件概述（Windows 窗体）
> [!NOTE]
>  <xref:System.Windows.Forms.ToolStrip> 控件取代了 <xref:System.Windows.Forms.ToolBar> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.ToolBar> 控件以实现向后兼容并供将来使用。  
  
 Windows 窗体 <xref:System.Windows.Forms.ToolBar> 控件用作窗体上的控制条，用于显示一行下拉菜单和一些可激活命令的位图按钮。  这样，单击一个工具栏按钮可与选择一个菜单命令等效。  可将按钮配置为以普通按钮、下拉菜单或分隔符等形式显示和表现。  通常情况下，工具栏包含的按钮和菜单与应用程序菜单结构中的项相对应，以提供对应用程序的常用功能和命令的快速访问。  
  
## 使用 ToolBar 控件  
 <xref:System.Windows.Forms.ToolBar> 控件通常沿其父窗口顶部“停靠”，但是也可以将它停靠到窗口的任一边上。  当用户将鼠标指针指向工具栏按钮时，工具栏可以显示工具提示。  工具提示是一个小的弹出式窗口，用以简述按钮或菜单的用途。  若要显示工具提示，必须将 <xref:System.Windows.Forms.ToolBar.ShowToolTips%2A> 属性设置为 `true`。  
  
> [!NOTE]
>  某些应用程序的特点是具有与工具栏非常类似的控件，这些控件可以“浮动”在应用程序窗口之上并可以重新定位。  Windows 窗体 ToolBar 控件不能执行这些操作。  
  
 当 <xref:System.Windows.Forms.ToolBar.Appearance%2A> 属性设置为 [Normal](frlrfSystemWindowsFormsToolBarAppearanceClassTopic) 时，工具栏按钮以凸起和三维方式显示。  可以将工具栏的 <xref:System.Windows.Forms.ToolBar.Appearance%2A> 属性设置为 <xref:System.Windows.Forms.ToolBarAppearance>，以使工具栏及其按钮按平面方式显示。  当鼠标指针移动到平面按钮时，该按钮的外观变为三维形状。  可以使用分隔符将工具栏按钮划分成多个逻辑组。  分隔符是 <xref:System.Windows.Forms.ToolBarButton.Style%2A> 属性设置为 [Separator](frlrfSystemWindowsFormsToolBarButtonStyleClassTopic) 的工具栏按钮。  它在工具栏上显示为空白。  当工具栏具有平面外观时，按钮分隔符显示为直线而不是按钮之间的空白。  
  
 <xref:System.Windows.Forms.ToolBar> 允许您通过将 <xref:System.Windows.Forms.Button> 对象添加到 <xref:System.Windows.Forms.ToolBar.Buttons%2A> 集合中来创建工具栏。  可以使用“集合编辑器”将按钮添加到 <xref:System.Windows.Forms.ToolBar> 控件中；每个 <xref:System.Windows.Forms.Button> 对象都应分配有文本或图像，不过也可同时分配文本和图像。  图像由一个关联的 [ImageList](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md) 组件提供。  在运行时，可使用 <xref:System.Windows.Forms.ToolBar.ToolBarButtonCollection.Add%2A> 和 <xref:System.Windows.Forms.ToolBar.ToolBarButtonCollection.Remove%2A> 方法在 <xref:System.Windows.Forms.ToolBar.ToolBarButtonCollection> 中添加或移除按钮。  若要对 <xref:System.Windows.Forms.ToolBar> 的按钮进行编程，请向 <xref:System.Windows.Forms.ToolBar> 的 <xref:System.Windows.Forms.ToolBar.ButtonClick> 事件添加代码，使用 <xref:System.Windows.Forms.ToolBarButtonClickEventArgs> 类的 <xref:System.Windows.Forms.ToolBarButtonClickEventArgs.Button%2A> 属性来确定单击了哪个按钮。  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolBar>   
 [ToolBar 控件](../../../../docs/framework/winforms/controls/toolbar-control-windows-forms.md)   
 [如何：向 ToolBar 控件添加按钮](../../../../docs/framework/winforms/controls/how-to-add-buttons-to-a-toolbar-control.md)   
 [如何：定义工具栏按钮的图标](../../../../docs/framework/winforms/controls/how-to-define-an-icon-for-a-toolbar-button.md)   
 [如何：触发工具栏按钮的菜单事件](../../../../docs/framework/winforms/controls/how-to-trigger-menu-events-for-toolbar-buttons.md)