---
title: "Windows 窗体控件中的属性 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 属性"
  - "自定义控件 [Windows 窗体], 属性概述（使用代码）"
  - "属性 [Windows 窗体]"
ms.assetid: 2785279b-fb57-4937-8f6b-2050e475db6f
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Windows 窗体控件中的属性
Windows 窗体控件继承了基类 <xref:System.Windows.Forms.Control?displayProperty=fullName> 的许多属性。  包括 <xref:System.Windows.Forms.Control.Font%2A>、<xref:System.Windows.Forms.Control.ForeColor%2A>、<xref:System.Windows.Forms.Control.BackColor%2A>、<xref:System.Windows.Forms.Control.Bounds%2A>、<xref:System.Windows.Forms.Control.ClientRectangle%2A>、<xref:System.Windows.Forms.Control.DisplayRectangle%2A>、<xref:System.Windows.Forms.Control.Enabled%2A>、<xref:System.Windows.Forms.Control.Focused%2A>、<xref:System.Windows.Forms.Control.Height%2A>、<xref:System.Windows.Forms.Control.Width%2A>、<xref:System.Windows.Forms.Control.Visible%2A>、<xref:System.Windows.Forms.Control.AutoSize%2A> 等属性以及许多其他属性。  有关继承的属性的详细信息，请参见 <xref:System.Windows.Forms.Control?displayProperty=fullName>。  
  
 可以在控件中重写继承属性和定义新属性。  
  
## 本节内容  
 [定义属性](../../../../docs/framework/winforms/controls/defining-a-property-in-windows-forms-controls.md)  
 演示如何为自定义控件或组件实现属性，并介绍如何将该属性集成到设计环境中。  
  
 [使用 ShouldSerialize 和 Reset 方法定义默认值](../../../../docs/framework/winforms/controls/defining-default-values-with-the-shouldserialize-and-reset-methods.md)  
 演示如何为自定义控件或组件定义默认属性值。  
  
 [属性更改事件](../../../../docs/framework/winforms/controls/property-changed-events.md)  
 描述如何在属性值发生更改时启用属性更改通知。  
  
 [如何：公开构成控件的属性](../../../../docs/framework/winforms/controls/how-to-expose-properties-of-constituent-controls.md)  
 演示如何在自定义复合控件中公开构成控件的属性。  
  
 [自定义控件中的方法实现](../../../../docs/framework/winforms/controls/method-implementation-in-custom-controls.md)  
 描述如何在自定义控件和组件中实现方法。  
  
## 参考  
 <xref:System.Windows.Forms.UserControl>  
 介绍用于实现复合控件的基类。  
  
 <xref:System.ComponentModel.TypeConverterAttribute>  
 介绍指定要用于自定义属性类型的 <xref:System.ComponentModel.TypeConverter> 的特性。  
  
 <xref:System.ComponentModel.EditorAttribute>  
 介绍指定要用于自定义属性的 <xref:System.Drawing.Design.UITypeEditor> 的特性。  
  
## 相关章节  
 [Windows 窗体控件中的特性](../../../../docs/framework/winforms/controls/attributes-in-windows-forms-controls.md)  
 描述可以对自定义控件和组件的属性或其他成员应用的特性。  
  
 [组件的设计时特性\)](../Topic/Design-Time%20Attributes%20for%20Components.md)  
 列出要应用于组件和控件的元数据特性，以便使它们在设计时正确地显示在可视化设计器中。  
  
 [Extending Design\-Time Support](../Topic/Extending%20Design-Time%20Support.md)  
 描述如何实现如编辑器和设计器等提供设计时支持的类。