---
title: "ComboBox 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "ComboBox"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "组合框, 关于组合框"
  - "ComboBox 控件 [Windows 窗体], 关于 ComboBox 控件"
  - "下拉列表, ComboBox 控件"
  - "下拉列表, Windows 窗体"
ms.assetid: a58b393f-a614-45d1-8961-857a024b5acd
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# ComboBox 控件概述（Windows 窗体）
Windows 窗体 <xref:System.Windows.Forms.ComboBox> 控件用于在下拉组合框中显示数据。  默认情况下，<xref:System.Windows.Forms.ComboBox> 控件分两个部分显示：顶部是一个允许用户键入列表项的文本框。  第二部分是一个列表框，它显示一个项列表，用户可从中选择一项。  有关组合框的其他样式的更多信息，请参见 [何时使用 Windows 窗体 ComboBox 而非 ListBox](../../../../docs/framework/winforms/controls/when-to-use-a-windows-forms-combobox-instead-of-a-listbox.md)。  
  
 <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> 属性返回一个整数值，该值与选择的列表项相对应。  通过在代码中更改 <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> 值，可以编程方式更改选择项；列表中的相应项将出现在组合框的文本框部分。  如果未选定任何项，则 <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> 值为 \-1。  如果选择列表中的第一项，则 <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> 值为 0。  <xref:System.Windows.Forms.ComboBox.SelectedItem%2A> 属性类似于 <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A>，但它返回项本身，通常是字符串值。  <xref:System.Windows.Forms.ComboBox.ObjectCollection.Count%2A> 属性反映列表的项数，由于 <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> 是从零开始的，所以 <xref:System.Windows.Forms.ComboBox.ObjectCollection.Count%2A> 属性的值通常比 <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> 的最大可能值大一。  
  
 若要在 <xref:System.Windows.Forms.ComboBox> 控件中添加或删除项，请使用 <xref:System.Windows.Forms.ComboBox.ObjectCollection.Add%2A>、<xref:System.Windows.Forms.ComboBox.ObjectCollection.Insert%2A>、<xref:System.Windows.Forms.ComboBox.ObjectCollection.Clear%2A> 或 <xref:System.Windows.Forms.ComboBox.ObjectCollection.Remove%2A> 方法。  或者，可以在设计器中使用 <xref:System.Windows.Forms.ComboBox.Items%2A> 属性向列表添加项。  
  
## 请参阅  
 <xref:System.Windows.Forms.ComboBox>   
 [ListBox 控件概述](../../../../docs/framework/winforms/controls/listbox-control-overview-windows-forms.md)   
 [何时使用 Windows 窗体 ComboBox 而非 ListBox](../../../../docs/framework/winforms/controls/when-to-use-a-windows-forms-combobox-instead-of-a-listbox.md)   
 [如何：在 Windows 窗体 ComboBox 控件、ListBox 控件或 CheckedListBox 控件中添加或移除项](../../../../docs/framework/winforms/controls/add-and-remove-items-from-a-wf-combobox.md)   
 [如何：对 Windows 窗体 ComboBox 控件、ListBox 控件或 CheckedListBox 控件的内容排序](../../../../docs/framework/winforms/controls/sort-the-contents-of-a-wf-combobox-listbox-or-checkedlistbox-control.md)   
 [如何：访问 Windows 窗体 ComboBox 控件、ListBox 控件或 CheckedListBox 控件中的特定项](../../../../docs/framework/winforms/controls/access-specific-items-in-a-wf-combobox-listbox-or-checkedlistbox.md)   
 [如何：将 Windows 窗体 ComboBox 控件或 ListBox 控件绑定到数据](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-combobox-or-listbox-control-to-data.md)   
 [用于列出选项的 Windows 窗体控件](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)   
 [如何：为 Windows 窗体 ComboBox 控件、ListBox 控件或 CheckedListBox 控件创建查找表](../../../../docs/framework/winforms/controls/create-a-lookup-table-for-a-wf-combobox-listbox.md)