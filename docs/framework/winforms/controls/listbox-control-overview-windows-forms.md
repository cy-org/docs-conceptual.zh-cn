---
title: "ListBox 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "ListBox"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "列表框, 关于列表框"
  - "ListBox 控件 [Windows 窗体], 关于 ListBox 控件"
ms.assetid: 37ea226b-6fc8-4c70-936a-c6af4e0cad4c
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# ListBox 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.ListBox> 控件显示一个项列表，用户可从中选择一项或多项。  如果项总数超出可以显示的项数，则自动向 <xref:System.Windows.Forms.ListBox> 控件添加滚动条。  当 <xref:System.Windows.Forms.ListBox.MultiColumn%2A> 属性设置为 `true` 时，列表框以多列形式显示项，并且会出现一个水平滚动条。  当 <xref:System.Windows.Forms.ListBox.MultiColumn%2A> 属性设置为 `false` 时，列表框以单列形式显示项，并且会出现一个垂直滚动条。  当 <xref:System.Windows.Forms.ListBox.ScrollAlwaysVisible%2A> 设置为 `true` 时，无论项数多少都将显示滚动条。  <xref:System.Windows.Forms.ListBox.SelectionMode%2A> 属性确定一次可以选择多少列表项。  
  
## 更改 ListBox 控件的方法  
 <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> 属性返回对应于列表框中第一个选定项的整数值。  通过在代码中更改 <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> 值，可以编程方式更改选定项；列表中的相应项将在 Windows 窗体上突出显示。  如果未选定任何项，则 <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> 值为 \-1。  如果选定列表中的第一个项，则 <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> 值为 0。  当选定多个项时，<xref:System.Windows.Forms.ListBox.SelectedIndex%2A> 值反映在列表中第一个出现的选定项。  <xref:System.Windows.Forms.ListBox.SelectedItem%2A> 属性类似于 <xref:System.Windows.Forms.ListBox.SelectedIndex%2A>，但它返回项本身，通常是字符串值。  <xref:System.Windows.Forms.ListBox.ObjectCollection.Count%2A> 属性反映列表的项数，由于 <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> 是从零开始的，所以 <xref:System.Windows.Forms.ListBox.ObjectCollection.Count%2A> 属性的值通常比 <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> 的最大可能值大一。  
  
 若要在 <xref:System.Windows.Forms.ListBox> 控件中添加或删除项，请使用 <xref:System.Windows.Forms.ListBox.ObjectCollection.Add%2A>、<xref:System.Windows.Forms.ListBox.ObjectCollection.Insert%2A>、<xref:System.Windows.Forms.ListBox.ObjectCollection.Clear%2A> 或 <xref:System.Windows.Forms.ListBox.ObjectCollection.Remove%2A> 方法。  或者，可以在设计时使用 <xref:System.Windows.Forms.ListBox.Items%2A> 属性向列表添加项。  
  
## 请参阅  
 <xref:System.Windows.Forms.ListBox>   
 [如何：在 Windows 窗体 ComboBox 控件、ListBox 控件或 CheckedListBox 控件中添加或移除项](../../../../docs/framework/winforms/controls/add-and-remove-items-from-a-wf-combobox.md)   
 [如何：对 Windows 窗体 ComboBox 控件、ListBox 控件或 CheckedListBox 控件的内容排序](../../../../docs/framework/winforms/controls/sort-the-contents-of-a-wf-combobox-listbox-or-checkedlistbox-control.md)   
 [如何：将 Windows 窗体 ComboBox 控件或 ListBox 控件绑定到数据](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-combobox-or-listbox-control-to-data.md)   
 [ComboBox 控件概述](../../../../docs/framework/winforms/controls/combobox-control-overview-windows-forms.md)   
 [CheckedListBox 控件概述](../../../../docs/framework/winforms/controls/checkedlistbox-control-overview-windows-forms.md)   
 [用于列出选项的 Windows 窗体控件](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)   
 [如何：为 Windows 窗体 ComboBox 控件、ListBox 控件或 CheckedListBox 控件创建查找表](../../../../docs/framework/winforms/controls/create-a-lookup-table-for-a-wf-combobox-listbox.md)