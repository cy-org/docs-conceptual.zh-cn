---
title: "如何：在 Windows 窗体中更改 ToolStrip 项的间距和对齐方式 | Microsoft Docs"
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
  - "示例 [Windows 窗体], 工具栏"
  - "工具栏 [Windows 窗体], 对齐项"
  - "ToolStrip 控件 [Windows 窗体], 对齐项"
ms.assetid: cd483466-0f49-43df-addf-e2b5fcd64027
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：在 Windows 窗体中更改 ToolStrip 项的间距和对齐方式
<xref:System.Windows.Forms.ToolStrip> 控件完全支持调整大小、<xref:System.Windows.Forms.ToolStripItem> 控件间相对间距调整、在 <xref:System.Windows.Forms.ToolStrip> 上排列控件，以及相对于 <xref:System.Windows.Forms.ToolStrip> 调整控件间距等布局功能。  
  
 因为 <xref:System.Windows.Forms.ToolStripItem.AutoSize%2A> 属性的默认值为 `true`，所以将自动调整控件大小，除非您将 <xref:System.Windows.Forms.ToolStripItem.AutoSize%2A> 属性设置为 `false`。  
  
### 手动调整 ToolStripItem 的大小  
  
1.  将关联控件的 <xref:System.Windows.Forms.ToolStripItem.AutoSize%2A> 属性设置为 `false`。  
  
    ```vb  
    ToolStripButton1.AutoSize = False  
  
    ```  
  
    ```csharp  
    toolStripButton1.AutoSize = false;  
  
    ```  
  
2.  根据需要为关联的 <xref:System.Windows.Forms.ToolStripItem> 设置 <xref:System.Windows.Forms.ToolStripItem.Size%2A> 属性。  
  
### 设置 ToolStripItem 的间距  
  
1.  将所需值（以像素为单位）插入到关联控件的 <xref:System.Windows.Forms.ToolStripItem.Margin%2A> 属性。  
  
     <xref:System.Windows.Forms.ToolStripItem.Margin%2A> 属性的值按照左、上、右和下的顺序指定此项和相邻项的间距。  
  
    ```vb  
    ToolStripTextBox1.Margin = New System.Windows.Forms.Padding _  
        (3, 0, 3, 0)  
  
    ```  
  
    ```csharp  
    toolStripTextBox1.Margin = new System.Windows.Forms.Padding   
        (3, 0, 3, 0);  
  
    ```  
  
### 将 ToolStripItem 与 ToolStrip 的右侧对齐  
  
1.  将关联控件的 <xref:System.Windows.Forms.ToolStripItem.Alignment%2A> 属性设置为 <xref:System.Windows.Forms.ToolStripItemAlignment>。  默认情况下，<xref:System.Windows.Forms.ToolStripItem.Alignment%2A> 被设置为 <xref:System.Windows.Forms.ToolStripItemAlignment>，将控件与 <xref:System.Windows.Forms.ToolStrip> 的左侧对齐。  
  
    ```vb  
    ToolStripSplitButton1.Alignment = _  
        System.Windows.Forms.ToolStripItemAlignment.Right  
  
    ```  
  
    ```csharp  
    toolStripSplitButton1.Alignment =   
        System.Windows.Forms.ToolStripItemAlignment.Right;  
  
    ```  
  
### 在 ToolStrip 上排列 ToolStrip 项  
  
-   将 <xref:System.Windows.Forms.ToolStrip.LayoutStyle%2A> 属性设置为需要的 <xref:System.Windows.Forms.ToolStripLayoutStyle> 值。  
  
    ```vb  
    ToolStripDropDown1.LayoutStyle = _  
        System.Windows.Forms.ToolStripLayoutStyle.Flow  
  
    ```  
  
    ```csharp  
    toolStripDropDown1.LayoutStyle =   
        System.Windows.Forms.ToolStripLayoutStyle.Flow;  
  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStrip>   
 <xref:System.Windows.Forms.Control.Layout>   
 <xref:System.Windows.Forms.ToolStrip.LayoutCompleted>   
 <xref:System.Windows.Forms.ToolStrip.LayoutSettings%2A>   
 <xref:System.Windows.Forms.ToolStripItem.TextImageRelation%2A>   
 <xref:System.Windows.Forms.ToolStripItem.Placement%2A>   
 <xref:System.Windows.Forms.ToolStrip.CanOverflow%2A>   
 [ToolStrip 控件概述](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)   
 [ToolStrip 控件体系结构](../../../../docs/framework/winforms/controls/toolstrip-control-architecture.md)   
 [ToolStrip 技术摘要](../../../../docs/framework/winforms/controls/toolstrip-technology-summary.md)