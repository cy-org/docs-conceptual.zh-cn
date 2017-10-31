---
title: "NumericUpDown 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "NumericUpDown"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "数值调节钮控件, Windows 窗体"
  - "NumericUpDown 控件 [Windows 窗体], 关于 NumericUpDown 控件"
  - "数值调节钮控件, Windows 窗体"
ms.assetid: cff3cf30-4d46-4381-87df-37bfe83c71c5
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# NumericUpDown 控件概述（Windows 窗体）
<xref:System.Windows.Forms.NumericUpDown> 控件看起来像是一个文本框与一对用户可单击以调整值的箭头的组合。  该控件显示并设置固定的数值选择列表中的单个数值。  用户可以通过单击向上和向下、按向上和向下键或在控件的文本框部件中键入一个数字来增大和减小数字。  单击向上键时，值向最大值方向移动；单击向下键时，值向最小值方向移动。  
  
 此控件由于具有通用的功能，所以不失为一种明智的选择，例如在为音乐播放器应用程序创建音量控件时。  <xref:System.Windows.Forms.NumericUpDown> 控件用于许多 Windows 控制面板应用程序。  
  
## 主要属性和方法  
 该控件的文本框中显示的数字可为多种格式，包括十六进制。  有关更多信息，请参见 [如何：设置 Windows 窗体 NumericUpDown 控件的格式](../../../../docs/framework/winforms/controls/how-to-set-the-format-for-the-windows-forms-numericupdown-control.md)。  该控件的主要属性包括 <xref:System.Windows.Forms.NumericUpDown.Value%2A>、<xref:System.Windows.Forms.NumericUpDown.Maximum%2A>（默认值为 100）、<xref:System.Windows.Forms.NumericUpDown.Minimum%2A>（默认值为 0）和 <xref:System.Windows.Forms.NumericUpDown.Increment%2A>（默认值为 1）。  <xref:System.Windows.Forms.NumericUpDown.Value%2A> 属性设置该控件中当前选择的数字。  <xref:System.Windows.Forms.NumericUpDown.Increment%2A> 属性设置用户单击向上或向下箭头时数字的调整量。  当焦点移出该控件时，将根据最小值和最大值验证键入的输入。  当用户连续按向上或向下箭头时，您可以使用 <xref:System.Windows.Forms.NumericUpDown.Accelerations%2A> 属性增加该控件在数字上移动的速度。  该控件的主要方法包括 <xref:System.Windows.Forms.NumericUpDown.UpButton%2A> 和 <xref:System.Windows.Forms.NumericUpDown.DownButton%2A>。  
  
## 请参阅  
 <xref:System.Windows.Forms.NumericUpDown>   
 [NumericUpDown 控件](../../../../docs/framework/winforms/controls/numericupdown-control-windows-forms.md)   
 [如何：设置 Windows 窗体 NumericUpDown 控件的格式](../../../../docs/framework/winforms/controls/how-to-set-the-format-for-the-windows-forms-numericupdown-control.md)   
 [TextBox 控件](../../../../docs/framework/winforms/controls/textbox-control-windows-forms.md)