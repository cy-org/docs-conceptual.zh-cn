---
title: "如何：使用填充在 Windows 窗体控件周围创建边框 | Microsoft Docs"
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
  - "控件 [Windows 窗体], Margin 属性"
  - "控件 [Windows 窗体], 大纲显示"
  - "控件 [Windows 窗体], Padding 属性"
  - "Margin 属性 [Windows 窗体]"
  - "边距"
  - "边距, Windows 窗体"
  - "Padding 属性 [Windows 窗体]"
  - "填充, Windows 窗体"
ms.assetid: bac7ed4d-a163-4259-98bd-155a36345890
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：使用填充在 Windows 窗体控件周围创建边框
下面的代码示例演示如何在 <xref:System.Windows.Forms.RichTextBox> 控件周围创建边框或轮廓。  该示例将 <xref:System.Windows.Forms.Panel> 控件的 <xref:System.Windows.Forms.Padding> 属性的值设置为 5，并将 <xref:System.Windows.Forms.RichTextBox> 子控件的 <xref:System.Windows.Forms.Control.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle>。  <xref:System.Windows.Forms.Panel> 控件的 <xref:System.Windows.Forms.Control.BackColor%2A> 被设置为 <xref:System.Drawing.Color.Blue%2A>，这样会在 <xref:System.Windows.Forms.RichTextBox> 控件周围创建一个蓝色边框。  
  
## 示例  
 [!code-csharp[System.Windows.Forms.Padding#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Padding/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.Padding#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Padding/VB/Form1.vb#1)]  
  
## 请参阅  
 <xref:System.Windows.Forms.Padding>   
 [Windows 窗体控件中的边距和填充](../../../../docs/framework/winforms/controls/margin-and-padding-in-windows-forms-controls.md)