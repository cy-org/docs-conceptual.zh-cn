---
title: "Windows 窗体中的鼠标指针 | Microsoft Docs"
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
  - "光标, 设置 [Windows 窗体]"
  - "鼠标光标"
  - "鼠标指针"
  - "鼠标指针, 设置 [Windows 窗体]"
  - "鼠标, 光标"
  - "指针, 设置 [Windows 窗体]"
ms.assetid: c3400d85-de5b-42e8-abc3-d6088d69ee53
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Windows 窗体中的鼠标指针
鼠标“指针”（有时称为光标）是一幅位图，它用于在屏幕上为通过鼠标进行的用户输入指定焦点。  本主题概述 Windows 窗体中的鼠标指针，并描述修改和控制鼠标指针的一些方法。  
  
## 访问鼠标指针  
 鼠标指针由 <xref:System.Windows.Forms.Cursor> 类表示，并且每个 <xref:System.Windows.Forms.Control> 都有一个为该控件指定指针的 <xref:System.Windows.Forms.Control.Cursor%2A?displayProperty=fullName> 属性。  <xref:System.Windows.Forms.Cursor> 类包含用于描述鼠标指针的属性（如 <xref:System.Windows.Forms.Cursor.Position%2A> 和 <xref:System.Windows.Forms.Cursor.HotSpot%2A> 属性）和可以修改鼠标指针外观的方法（如 <xref:System.Windows.Forms.Cursor.Show%2A>、<xref:System.Windows.Forms.Cursor.Hide%2A> 和 <xref:System.Windows.Forms.Cursor.DrawStretched%2A> 方法）。  
  
## 控制鼠标指针  
 有时，您可能希望限制鼠标指针的使用区域或希望更改鼠标位置。  您可以使用 <xref:System.Windows.Forms.Cursor> 的 <xref:System.Windows.Forms.Cursor.Position%2A> 属性来获取或设置鼠标的当前位置。  另外，通过设置 <xref:System.Windows.Forms.Cursor.Clip%2A> 属性，可以限制鼠标指针的使用区域。  默认情况下，剪辑区域是整个屏幕。  
  
## 更改鼠标指针  
 更改鼠标指针外观是一种向用户提供反馈的重要方式。  例如，在 <xref:System.Windows.Forms.Control.MouseEnter> 和 <xref:System.Windows.Forms.Control.MouseLeave> 事件的处理程序中可以修改鼠标指针，以便通知用户正在进行运算并限制控件中的用户交互操作。  有时，鼠标指针会因某些系统事件而发生更改，例如，在拖放操作中涉及到您的应用程序时。  
  
 更改鼠标指针的主要方式是将控件的 <xref:System.Windows.Forms.Control.Cursor%2A?displayProperty=fullName> 或 <xref:System.Windows.Forms.Control.DefaultCursor%2A> 属性设为新的 <xref:System.Windows.Forms.Cursor>。  有关更改鼠标指针的示例，请参见 <xref:System.Windows.Forms.Cursor> 类中的代码示例。  另外，<xref:System.Windows.Forms.Cursors> 类为多种不同类型的指针公开一组 <xref:System.Windows.Forms.Cursor> 对象，如类似手形的指针。  若要每当鼠标指针在控件上时都显示类似沙漏的等待指针，请使用 <xref:System.Windows.Forms.Control> 类的 <xref:System.Windows.Forms.Control.UseWaitCursor%2A> 属性。  
  
## 请参阅  
 <xref:System.Windows.Forms.Cursor>   
 [Windows 窗体应用程序中的鼠标输入](../../../docs/framework/winforms/mouse-input-in-a-windows-forms-application.md)   
 [Windows 窗体中的拖放功能](../../../docs/framework/winforms/drag-and-drop-functionality-in-windows-forms.md)