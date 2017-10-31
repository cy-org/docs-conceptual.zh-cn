---
title: "如何：在 Windows 窗体的 ToolStrip 控件中启用自动完成 | Microsoft Docs"
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
  - "AutoComplete, 在工具栏中启用"
  - "AutoComplete, 示例"
  - "示例 [Windows 窗体], 工具栏"
  - "工具栏 [Windows 窗体], AutoComplete"
  - "ToolStrip 控件 [Windows 窗体], AutoComplete"
  - "ToolStripComboBox 类, 示例"
ms.assetid: fd66d085-1af1-45d4-930a-cde944da2e16
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：在 Windows 窗体的 ToolStrip 控件中启用自动完成
下面的过程将一个 <xref:System.Windows.Forms.ToolStripLabel> 和一个 <xref:System.Windows.Forms.ToolStripComboBox> 组合在一起，以下拉方式可显示一个项列表（例如最近访问的网站）。  如果用户键入一个与列表中某项的第一个字符匹配的字符，该项将会立即显示。  
  
> [!NOTE]
>  自动完成功能处理 `ToolStrip` 控件的方式与处理传统控件（如 <xref:System.Windows.Forms.ComboBox> 和 <xref:System.Windows.Forms.TextBox>）相同。  
  
### 在 ToolStrip 控件中启用自动完成  
  
1.  创建一个 <xref:System.Windows.Forms.ToolStrip> 控件，并向其中添加项。  
  
    ```vb  
    ToolStrip1 = New System.Windows.Forms.ToolStrip  
    ToolStrip1.Items.AddRange(New System.Windows.Forms.ToolStripItem()_  
        {ToolStripLabel1, ToolStripComboBox1})  
    ```  
  
    ```csharp  
    toolStrip1 = new System.Windows.Forms.ToolStrip();  
    toolStrip1.Items.AddRange(new System.Windows.Forms.ToolStripItem[]   
        {toolStripLabel1, toolStripComboBox1});  
  
    ```  
  
2.  将标签和组合框的 <xref:System.Windows.Forms.ToolStripItem.Overflow%2A> 属性设置为 <xref:System.Windows.Forms.ToolStripItemOverflow>，以便该列表总是可用，而不管窗体的大小如何。  
  
    ```vb  
    ToolStripLabel1.Overflow = _  
        System.Windows.Forms.ToolStripItemOverflow.Never  
    ToolStripComboBox1.Overflow = _  
        System.Windows.Forms.ToolStripItemOverflow.Never  
    ```  
  
    ```csharp  
    toolStripLabel1.Overflow = _  
        System.Windows.Forms.ToolStripItemOverflow.Never  
    toolStripComboBox1.Overflow = System.Windows.Forms.ToolStripItemOverflow.Never  
  
    ```  
  
3.  向 <xref:System.Windows.Forms.ToolStripComboBox> 控件的项集合中添加字词。  
  
    ```vb  
    ToolStripComboBox1.Items.AddRange(New Object() {"First Item", _  
        "Second Item", "Third Item"})  
  
    ```  
  
    ```csharp  
    toolStripComboBox1.Items.AddRange(new object[] {"First item", "Second item", "Third item"});  
  
    ```  
  
4.  将组合框的 <xref:System.Windows.Forms.ComboBox.AutoCompleteMode%2A> 属性设置为 <xref:System.Windows.Forms.AutoCompleteMode>。  
  
    ```vb  
    ToolStripComboBox1.AutoCompleteMode = _  
        System.Windows.Forms.AutoCompleteMode.Append  
    ```  
  
    ```csharp  
    toolStripComboBox1.AutoCompleteMode = System.Windows.Forms.AutoCompleteMode.Append;  
  
    ```  
  
5.  将组合框的 <xref:System.Windows.Forms.ComboBox.AutoCompleteSource%2A> 属性设置为 <xref:System.Windows.Forms.AutoCompleteSource>。  
  
    ```vb  
    ToolStripComboBox1.AutoCompleteSource = _  
        System.Windows.Forms.AutoCompleteSource.ListItems  
    ```  
  
    ```csharp  
    toolStripComboBox1.AutoCompleteSource = System.Windows.Forms.AutoCompleteSource.ListItems;  
  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.ToolStripLabel>   
 <xref:System.Windows.Forms.ToolStripComboBox>   
 <xref:System.Windows.Forms.ToolStripComboBox.AutoCompleteMode%2A>   
 <xref:System.Windows.Forms.ToolStripComboBox.AutoCompleteSource%2A>   
 [ToolStrip 控件概述](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)   
 [ToolStrip 控件体系结构](../../../../docs/framework/winforms/controls/toolstrip-control-architecture.md)   
 [ToolStrip 技术摘要](../../../../docs/framework/winforms/controls/toolstrip-technology-summary.md)