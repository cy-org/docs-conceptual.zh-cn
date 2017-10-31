---
title: "如何：在 Windows 窗体中更改 ToolStrip 文本和图像的外观 | Microsoft Docs"
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
  - "工具栏 [Windows 窗体], 外观"
  - "工具栏 [Windows 窗体], 图像"
  - "工具栏 [Windows 窗体], 文本"
  - "ToolStrip 控件 [Windows 窗体], 外观"
  - "ToolStrip 控件 [Windows 窗体], 图像"
  - "ToolStrip 控件 [Windows 窗体], 文本"
ms.assetid: d62dc9d1-2edd-4dfa-aed7-1335d6e13d86
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：在 Windows 窗体中更改 ToolStrip 文本和图像的外观
可以控制是否在 <xref:System.Windows.Forms.ToolStripItem> 上显示文本和图像，以及它们如何互相对齐和与 <xref:System.Windows.Forms.ToolStrip> 对齐。  
  
### 定义在 ToolStripItem 上显示的内容  
  
-   将 <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> 属性设置为所需的值。  可能的值有：`Image`、`ImageAndText`、`None` 和 `Text`。  默认值为 `ImageAndText`。  
  
    ```vb  
    ToolStripButton2.DisplayStyle = _  
        System.Windows.Forms.ToolStripItemDisplayStyle.Image  
  
    ```  
  
    ```csharp  
    toolStripButton2.DisplayStyle = System.Windows.Forms.ToolStripItemDisplayStyle.Image;  
  
    ```  
  
### 对齐 ToolStripItem 上的文本  
  
-   将 <xref:System.Windows.Forms.ToolStripItem.TextAlign%2A> 属性设置为所需的值。  可能是上、中、下和左、中、右的组合。  默认值为 `MiddleCenter`。  
  
    ```vb  
    ToolStripSplitButton1.TextAlign = _  
        System.Drawing.ContentAlignment.MiddleRight  
  
    ```  
  
    ```csharp  
    toolStripSplitButton1.TextAlign = System.Drawing.ContentAlignment.MiddleRight;  
  
    ```  
  
### 对齐 ToolStripItem 上的图像  
  
-   将 <xref:System.Windows.Forms.ToolStripItem.ImageAlign%2A> 属性设置为所需的值。  可能是上、中、下和左、中、右的组合。  默认值为 `MiddleLeft`。  
  
    ```vb  
    ToolStripSplitButton1.ImageAlign = _  
        System.Drawing.ContentAlignment.MiddleRight  
  
    ```  
  
    ```csharp  
    toolStripSplitButton1.ImageAlign = System.Drawing.ContentAlignment.MiddleRight;  
  
    ```  
  
### 定义 ToolStripItem 文本和图像相对于各自如何显示  
  
-   将 <xref:System.Windows.Forms.ToolStripItem.TextImageRelation%2A> 属性设置为所需的值。  可能的值为 `ImageAboveText`、`ImageBeforeText`、`Overlay`、`TextAboveImage` 和 `TextBeforeImage`。  默认值为 `ImageBeforeText`。  
  
    ```vb  
    ToolStripButton1.TextImageRelation = _  
        System.Windows.Forms.TextImageRelation.ImageAboveText  
  
    ```  
  
    ```csharp  
    toolStripButton1.TextImageRelation = System.Windows.Forms.TextImageRelation.ImageAboveText;  
  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStrip>   
 [ToolStrip 控件概述](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)   
 [ToolStrip 控件体系结构](../../../../docs/framework/winforms/controls/toolstrip-control-architecture.md)   
 [ToolStrip 技术摘要](../../../../docs/framework/winforms/controls/toolstrip-technology-summary.md)