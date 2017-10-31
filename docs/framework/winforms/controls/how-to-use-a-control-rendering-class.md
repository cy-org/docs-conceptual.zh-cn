---
title: "如何：使用控件呈现类 | Microsoft Docs"
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
  - "专业外观, 呈现“Windows 窗体”控件"
  - "视觉样式, 呈现“Windows 窗体”控件"
  - "直观主题, 应用于 Windows 窗体控件"
ms.assetid: c0125e34-cd74-4c35-818c-3e40f462b0a3
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：使用控件呈现类
此示例演示如何使用 <xref:System.Windows.Forms.ComboBoxRenderer> 类呈现组合框控件的下拉箭头。  该示例包含一个简单自定义控件的 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法。  <xref:System.Windows.Forms.ComboBoxRenderer.IsSupported%2A?displayProperty=fullName> 属性用于确定是否在应用程序窗口的工作区中启用了视觉样式。  如果已启用了视觉样式，则 <xref:System.Windows.Forms.ComboBoxRenderer.DrawDropDownButton%2A?displayProperty=fullName> 方法将使用视觉样式呈现下拉箭头；否则 <xref:System.Windows.Forms.ControlPaint.DrawComboButton%2A?displayProperty=fullName> 方法将以 Windows 经典样式呈现下拉箭头。  
  
## 示例  
 [!code-cpp[System.Windows.Forms_ControlRenderer#10](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms_ControlRenderer/cpp/form1.cpp#10)]
 [!code-csharp[System.Windows.Forms_ControlRenderer#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms_ControlRenderer/CS/form1.cs#10)]
 [!code-vb[System.Windows.Forms_ControlRenderer#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms_ControlRenderer/VB/form1.vb#10)]  
  
## 编译代码  
 此示例需要：  
  
-   派生自 <xref:System.Windows.Forms.Control> 类的自定义控件。  
  
-   承载该自定义控件的 <xref:System.Windows.Forms.Form>。  
  
-   对 <xref:System?displayProperty=fullName>、<xref:System.Drawing?displayProperty=fullName>、<xref:System.Windows.Forms?displayProperty=fullName> 和 <xref:System.Windows.Forms.VisualStyles?displayProperty=fullName> 命名空间的引用。  
  
## 请参阅  
 [使用视觉样式呈现控件](../../../../docs/framework/winforms/controls/rendering-controls-with-visual-styles.md)