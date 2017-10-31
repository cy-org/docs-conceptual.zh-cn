---
title: "如何：对 Windows 窗体 ComboBox 控件、ListBox 控件或 CheckedListBox 控件的内容排序 | Microsoft Docs"
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
  - "CheckedListBox 控件 [Windows 窗体], 排序"
  - "组合框, 对目录进行排序"
  - "ComboBox 控件 [Windows 窗体], 对目录进行排序"
  - "列表框, 对目录进行排序"
  - "ListBox 控件 [Windows 窗体], 对目录进行排序"
ms.assetid: c268e387-3d1d-4d86-a940-19f6673c8d06
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：对 Windows 窗体 ComboBox 控件、ListBox 控件或 CheckedListBox 控件的内容排序
Windows 窗体控件为数据绑定时不排序。  若要显示已排序数据，请使用支持排序的数据源，然后使数据源对数据进行排序。  支持排序的数据源有数据视图、数据视图管理器和已排序数组。  
  
 如果控件不是数据绑定控件，就可以对它进行排序。  
  
### 排序列表  
  
1.  将  `Sorted`  属性设置为 `true`。  
  
     本设置以排序顺序重新放置现有的所有列表项。  
  
## 请参阅  
 <xref:System.Windows.Forms.ComboBox>   
 <xref:System.Windows.Forms.ListBox>   
 <xref:System.Windows.Forms.CheckedListBox>   
 [Windows 窗体数据绑定](../../../../docs/framework/winforms/windows-forms-data-binding.md)   
 [如何：在 Windows 窗体 ComboBox 控件、ListBox 控件或 CheckedListBox 控件中添加或移除项](../../../../docs/framework/winforms/controls/add-and-remove-items-from-a-wf-combobox.md)   
 [何时使用 Windows 窗体 ComboBox 而非 ListBox](../../../../docs/framework/winforms/controls/when-to-use-a-windows-forms-combobox-instead-of-a-listbox.md)   
 [用于列出选项的 Windows 窗体控件](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)