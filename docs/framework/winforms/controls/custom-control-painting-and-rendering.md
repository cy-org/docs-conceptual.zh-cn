---
title: "自定义控件的绘制和呈现 | Microsoft Docs"
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
  - "自定义控件 [Windows 窗体], 绘制"
  - "自定义控件 [Windows 窗体], 呈现"
  - "OnPaint 方法"
  - "用户控件 [Windows 窗体], 绘制"
ms.assetid: a09dbf76-0966-4cbf-a66a-2083ba98e068
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 自定义控件的绘制和呈现
控件的自定义绘制是由 .NET Framework 简化的众多复杂任务之一。  在创作自定义控件时，有很多涉及控件的图形化外观的选项。  如果要创作从 `Control` 继承的控件，则必须提供代码，使控件得以呈现它的图形化表示形式。  如果通过从 `UserControl` 继承来创建用户控件，或者从某个 Windows 窗体控件继承，则可以重写标准的图形化表示形式，并提供您自己的图形代码。  如果要为正在创作的 `UserControl` 的构成控件提供自定义呈现，则您的选择变得更为有限，但仍然允许您的控件和应用程序拥有很大的图形化可能性。  
  
## 本节内容  
 [呈现 Windows 窗体控件](../../../../docs/framework/winforms/controls/rendering-a-windows-forms-control.md)  
 说明如何编制显示控件的逻辑。  
  
 [用户描述的控件](../../../../docs/framework/winforms/controls/user-drawn-controls.md)  
 概述有关编写和重写控件的呈现代码的步骤。  
  
 [构成控件](../../../../docs/framework/winforms/controls/constituent-controls.md)  
 描述如何实现用户控件和窗体中构成控件的自定义呈现代码。  
  
 [如何：使控件在运行时不可见](../../../../docs/framework/winforms/controls/how-to-make-your-control-invisible-at-run-time.md)  
 显示如何使用 <xref:System.Windows.Forms.Control.Visible%2A> 属性来隐藏和显示控件。  
  
 [如何：使控件拥有透明背景](../../../../docs/framework/winforms/controls/how-to-give-your-control-a-transparent-background.md)  
 显示如何使用 <xref:System.Windows.Forms.Control.SetStyle%2A> 方法来创建不透明、透明或部分透明的背景颜色。  
  
 [使用视觉样式呈现控件](../../../../docs/framework/winforms/controls/rendering-controls-with-visual-styles.md)  
 显示如何在支持可见样式的操作系统中使用可见样式来呈现控件。  
  
## 参考  
 <xref:System.Windows.Forms.Control>  
 描述此类并提供指向其所有成员的链接。  
  
 <xref:System.Windows.Forms.UserControl>  
 描述此类并提供指向其所有成员的链接。  
  
 <xref:System.Windows.Forms.Control.OnPaint%2A>  
 描述此方法。  
  
## 相关章节  
 [如何：创建用于绘制的 Graphics 对象](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)  
 从 Visual Studio 的角度介绍 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 图形功能，并提供指向更多信息的链接。  
  
 [各种自定义控件](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)  
 描述可以创作的自定义控件的种类。