---
title: "何时使用 Windows 窗体 ComboBox 而非 ListBox | Microsoft Docs"
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
  - "绑定控件, 组合框"
  - "组合框, 与列表框比较"
  - "ComboBox 控件 [Windows 窗体], 与 ListBox 比较"
  - "ListBox 控件 [Windows 窗体], 访问项"
  - "ListBox 控件 [Windows 窗体], 添加和移除项"
  - "ListBox 控件 [Windows 窗体], 与 ComboBox"
  - "ListCount 属性"
  - "ListIndex 属性"
  - "Windows 窗体控件, 数据绑定"
ms.assetid: 7bcaea58-1cfa-46db-9baf-b75a69d8f9ec
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 何时使用 Windows 窗体 ComboBox 而非 ListBox
<xref:System.Windows.Forms.ComboBox> 控件和 <xref:System.Windows.Forms.ListBox> 控件具有相似行为，在某些情况下可以互换。  但是也存在其中一种控件更适合于某任务的情况。  
  
 通常，组合框适合于存在一组“建议”选项的情况，而列表框适合于想要将输入限制为列表中内容的情况。  组合框包含一个文本框字段，因此可以键入列表中没有的选项。  但 <xref:System.Windows.Forms.ComboBox.DropDownStyle%2A> 属性设置为 <xref:System.Windows.Forms.ComboBoxStyle> 时除外。  在此情况下，如果您键入第一个字母，此控件将自动选择一项。  
  
 此外，组合框可节约窗体上的空间。  由于在用户单击下箭头键以前不显示完整列表，所以组合框可以方便地放入列表框放不下的窄小空间。  当 <xref:System.Windows.Forms.ComboBox.DropDownStyle%2A> 属性设置为 <xref:System.Windows.Forms.ComboBoxStyle> 时情况例外：此时显示完整列表，并且组合框占用的空间比列表框多。  
  
## 请参阅  
 <xref:System.Windows.Forms.ComboBox>   
 <xref:System.Windows.Forms.ListBox>   
 [如何：在 Windows 窗体 ComboBox 控件、ListBox 控件或 CheckedListBox 控件中添加或移除项](../../../../docs/framework/winforms/controls/add-and-remove-items-from-a-wf-combobox.md)   
 [如何：对 Windows 窗体 ComboBox 控件、ListBox 控件或 CheckedListBox 控件的内容排序](../../../../docs/framework/winforms/controls/sort-the-contents-of-a-wf-combobox-listbox-or-checkedlistbox-control.md)   
 [用于列出选项的 Windows 窗体控件](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)