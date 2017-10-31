---
title: "DomainUpDown 控件（Windows 窗体） | Microsoft Docs"
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
  - "DomainUpDown 控件 [Windows 窗体]"
  - "数值调节钮控件"
  - "数值调节钮控件, up-down 控件"
  - "up-down 控件"
  - "up-down 控件, 数值调节钮控件"
ms.assetid: fb7cf017-e931-4a95-9d21-8caee4ee122a
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# DomainUpDown 控件（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.DomainUpDown> 控件看起来像是一个文本框和一对用于在列表中上下移动的箭头的组合。  该控件显示并设置选择列表中的文本字符串。  用户可以通过多种方式来选择字符串，这些方式包括单击向上和向下按钮在列表中移动，按向上和向下键，或者键入与列表项匹配的字符串等。  该控件一个可能的用途是从按字母顺序排序的名称列表中选择项。  （若要对该列表排序，请将 <xref:System.Windows.Forms.DomainUpDown.Sorted%2A> 属性设置为 `true`。）该控件的作用与列表框或组合框非常类似，但它占用的空间非常小。  
  
 该控件的主要属性包括 <xref:System.Windows.Forms.DomainUpDown.Items%2A>、<xref:System.Windows.Forms.UpDownBase.ReadOnly%2A> 和 <xref:System.Windows.Forms.DomainUpDown.Wrap%2A>。  <xref:System.Windows.Forms.DomainUpDown.Items%2A> 属性包含文本值显示在该控件中的对象列表。  如果 <xref:System.Windows.Forms.UpDownBase.ReadOnly%2A> 设置为 `false`，则该控件自动完成用户键入的文本并使该文本与列表中的值相匹配。  如果 <xref:System.Windows.Forms.DomainUpDown.Wrap%2A> 设置为 `true`，则滚过最后一项后将到达列表的第一项，反之亦然。  该控件的主要方法包括 <xref:System.Windows.Forms.DomainUpDown.UpButton%2A> 和 <xref:System.Windows.Forms.DomainUpDown.DownButton%2A>。  
  
 该控件只显示文本字符串。  如果需要显示数值的控件，则使用 <xref:System.Windows.Forms.NumericUpDown> 控件。  有关更多信息，请参见[NumericUpDown 控件](../../../../docs/framework/winforms/controls/numericupdown-control-windows-forms.md)。  
  
## 本节内容  
 [DomainUpDown 控件概述](../../../../docs/framework/winforms/controls/domainupdown-control-overview-windows-forms.md)  
 介绍有关 <xref:System.Windows.Forms.DomainUpDown> 控件的一般概念，该控件允许用户在文本字符串列表中浏览并从中进行选择。  
  
 [如何：以编程方式向 Windows 窗体 DomainUpDown 控件添加项](../../../../docs/framework/winforms/controls/how-to-add-items-to-windows-forms-domainupdown-controls-programmatically.md)  
 介绍如何指定 <xref:System.Windows.Forms.DomainUpDown> 控件应显示的文本字符串。  
  
 [如何：从 Windows 窗体 DomainUpDown 控件移除项](../../../../docs/framework/winforms/controls/how-to-remove-items-from-windows-forms-domainupdown-controls.md)  
 介绍如何使用代码从 <xref:System.Windows.Forms.DomainUpDown> 控件中删除项。  
  
## 参考  
 <xref:System.Windows.Forms.DomainUpDown>  
 描述该类并提供指向其所有成员的链接。  
  
 <xref:System.Windows.Forms.NumericUpDown>  
 介绍该类并提供指向其所有成员的链接。  
  
## 相关章节  
 [可在 Windows 窗体中使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)  
 提供 Windows 窗体控件的完整列表，其中包含指向这些控件用法信息的链接。