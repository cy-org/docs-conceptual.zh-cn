---
title: "如何：使控件拥有透明背景 | Microsoft Docs"
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
  - "自定义控件 [Windows 窗体], 透明背景"
  - "透明度, Windows 窗体自定义控件"
  - "透明背景, 自定义控件"
ms.assetid: 32433e63-f4e9-4305-9857-6de3edeb944a
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# 如何：使控件拥有透明背景
在早期版本的.NET Framework 中，如果事先未在窗体的构造函数中设置 <xref:System.Windows.Forms.Control.SetStyle%2A> 方法，控件将不支持设置透明背景色。 在当前的框架版本中，可以在设计时在“属性”窗口中或在窗体构造函数的代码中将背景色设置为 <xref:System.Drawing.Color.Transparent%2A>。  
  
> [!NOTE]
>  Windows 窗体控件不支持真正的透明。 透明 Windows 窗体控件的背景由其父级绘制。  
  
> [!NOTE]
>  即使将 <xref:System.Windows.Forms.ButtonBase.BackColor%2A> 属性设置为 <xref:System.Drawing.Color.Transparent%2A>，<xref:System.Windows.Controls.Button> 控件也不支持透明背景色。  
  
### 使控件拥有透明背景色  
  
-   在“属性”窗口中，选择 <xref:System.Windows.Forms.ButtonBase.BackColor%2A> 属性并将其设置为 <xref:System.Drawing.Color.Transparent%2A>  
  
## 请参阅  
 <xref:System.Drawing.Color.FromArgb%2A>   
 [使用 .NET Framework 开发自定义 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)   
 [使用托管图形类](../../../../docs/framework/winforms/advanced/using-managed-graphics-classes.md)   
 [如何：绘制不透明和半透明的线条](../../../../docs/framework/winforms/advanced/how-to-draw-opaque-and-semitransparent-lines.md)