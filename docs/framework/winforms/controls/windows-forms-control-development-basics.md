---
title: "Windows 窗体控件开发基础知识 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "控件 [Windows 窗体], 创建"
  - "自定义控件 [Windows 窗体], 派生类型"
  - "编程概念, Windows 窗体控件"
ms.assetid: 6277bb81-90f7-4c5b-9f4b-b02bb42dd316
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# Windows 窗体控件开发基础知识
Windows 窗体控件是从 <xref:System.Windows.Forms.Control?displayProperty=fullName> 直接或间接派生的类。  以下列表描述了开发 Windows 窗体控件的常见方案：  
  
-   组合现有控件来创作一个复合控件。  
  
     复合控件封装有一个可以作为控件重复使用的用户界面。  其中的一个示例就是由文本框和重置按钮组成的控件。  可视化设计器为创建复合控件提供了有力的支持。  若要创作复合控件，请从 <xref:System.Windows.Forms.UserControl?displayProperty=fullName> 派生。  基类 <xref:System.Windows.Forms.UserControl> 为子控件提供了键盘路由并使子控件可以作为一个组进行工作。  有关更多信息，请参见 [开发复合 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-a-composite-windows-forms-control.md)。  
  
-   扩展现有控件，对其进行自定义或为其添加功能。  
  
     一个不能更改颜色的按钮和一个具有跟踪点击次数属性的按钮就是扩展控件的具体示例。  可以通过从任何 Windows 窗体控件派生控件并重写或添加属性、方法和事件的方式来自定义 Windows 窗体控件。  
  
-   创作一个不是通过组合或扩展现有控件而形成的控件。  
  
     在这种方案中，需从基类 <xref:System.Windows.Forms.Control> 派生控件。  可以添加和重写基类的属性、方法和事件。  若要开始创作，请参见 [如何：开发简单的 Windows 窗体控件](../../../../docs/framework/winforms/controls/how-to-develop-a-simple-windows-forms-control.md)。  
  
 Windows 窗体控件的基类 \(<xref:System.Windows.Forms.Control>\) 提供了客户端基于 Windows 的应用程序中的视觉显示所需的管道。  <xref:System.Windows.Forms.Control> 提供窗口句柄，处理消息路由，并提供鼠标和键盘事件以及许多其他用户界面事件。  还提供了高级布局，并具有特定于可视显示的属性，如 <xref:System.Windows.Forms.Control.ForeColor%2A>、<xref:System.Windows.Forms.Control.BackColor%2A>、<xref:System.Windows.Forms.Control.Height%2A>、<xref:System.Windows.Forms.Control.Width%2A> 和许多其他属性。  此外，它还提供了安全性、线程支持以及与 ActiveX 控件的交互性。  由于基类提供了很多基础结构，使得开发自己的 Windows 窗体控件变得相对简单。  
  
## 请参阅  
 [如何：开发简单的 Windows 窗体控件](../../../../docs/framework/winforms/controls/how-to-develop-a-simple-windows-forms-control.md)   
 [开发复合 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-a-composite-windows-forms-control.md)   
 [如何：创建显示进度的 Windows 窗体控件](../../../../docs/framework/winforms/controls/how-to-create-a-windows-forms-control-that-shows-progress.md)   
 [各种自定义控件](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)