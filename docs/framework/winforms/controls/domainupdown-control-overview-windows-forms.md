---
title: "DomainUpDown 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "DomainUpDown"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "DomainUpDown 控件 [Windows 窗体], 关于 DomainUpDown 控件"
  - "数值调节钮控件, 关于数值调节钮"
ms.assetid: 3f40f9c1-20ad-4331-b9b5-b0127eb36eb3
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# DomainUpDown 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.DomainUpDown> 控件实质上是一个文本框和一对用于在列表中上下移动的按钮的组合。  该控件显示并设置选择列表中的文本字符串。  用户可以通过多种方式来选择字符串，这些方式包括单击向上和向下按钮在列表中移动，按向上和向下键，或者键入与列表项匹配的字符串等。  该控件一个可能的用途是从按字母顺序排序的名称列表中选择项。  
  
> [!NOTE]
>  若要对该列表进行排序，请将 <xref:System.Windows.Forms.DomainUpDown.Sorted%2A> 属性设置为 `true`。  
  
 该控件的作用与列表框或组合框非常类似，但它占用的空间非常小。  
  
## 主要属性  
 该控件的主要属性包括 <xref:System.Windows.Forms.DomainUpDown.Items%2A>、<xref:System.Windows.Forms.UpDownBase.ReadOnly%2A> 和 <xref:System.Windows.Forms.DomainUpDown.Wrap%2A>。  <xref:System.Windows.Forms.DomainUpDown.Items%2A> 属性包含文本值显示在该控件中的对象列表。  如果 <xref:System.Windows.Forms.UpDownBase.ReadOnly%2A> 设置为 `false`，则该控件自动完成用户键入的文本并使该文本与列表中的值相匹配。  如果 <xref:System.Windows.Forms.DomainUpDown.Wrap%2A> 设置为 `true`，则滚过最后一项后将到达列表的第一项，反之亦然。  该控件的主要方法包括 <xref:System.Windows.Forms.DomainUpDown.UpButton%2A> 和 <xref:System.Windows.Forms.DomainUpDown.DownButton%2A>。  
  
 该控件只显示文本字符串。  如果需要显示数值的控件，则使用 <xref:System.Windows.Forms.NumericUpDown> 控件。  有关更多信息，请参见 [NumericUpDown 控件概述](../../../../docs/framework/winforms/controls/numericupdown-control-overview-windows-forms.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.DomainUpDown>   
 [DomainUpDown 控件](../../../../docs/framework/winforms/controls/domainupdown-control-windows-forms.md)