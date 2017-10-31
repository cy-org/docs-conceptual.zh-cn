---
title: "如何：更改 Windows 窗体 TabControl 的外观 | Microsoft Docs"
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
  - "按钮, 将选项卡显示为"
  - "图标, 在选项卡上显示"
  - "TabControl 控件 [Windows 窗体], 更改页外观"
  - "选项卡, 控制外观"
ms.assetid: 7c6cc443-ed62-4d26-b94d-b8913b44f773
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：更改 Windows 窗体 TabControl 的外观
通过使用 <xref:System.Windows.Forms.TabControl> 控件和组成控件上各选项卡的 <xref:System.Windows.Forms.TabPage> 对象的属性，可以更改 Windows 窗体中选项卡的外观。  通过设置这些属性，可使用编程方式在选项卡上显示图像，以垂直方式而非水平方式显示选项卡，显示多行选项卡，以及启用或禁用选项卡。  
  
### 在选项卡的标签部位显示图标  
  
1.  向窗体添加 <xref:System.Windows.Forms.ImageList> 控件。  
  
2.  将图像添加到图像列表中。  
  
     有关图像列表的更多信息，请参见 [ImageList 组件](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md) 和 [如何：使用 Windows 窗体 ImageList 组件添加或移除图像](../../../../docs/framework/winforms/controls/how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md)。  
  
3.  将 <xref:System.Windows.Forms.TabControl> 控件的 <xref:System.Windows.Forms.TabControl.ImageList%2A> 属性设置为 <xref:System.Windows.Forms.ImageList> 控件。  
  
4.  将 <xref:System.Windows.Forms.TabPage> 的 <xref:System.Windows.Forms.TabPage.ImageIndex%2A> 属性设置为列表中的相应图像的索引。  
  
### 创建多行选项卡  
  
1.  添加所需的选项卡页的数量。  
  
2.  将 <xref:System.Windows.Forms.TabControl> 的 <xref:System.Windows.Forms.TabControl.Multiline%2A> 属性设置为 `true`。  
  
3.  如果选项卡尚未以多行方式显示，则设置 <xref:System.Windows.Forms.TabControl> 的 <xref:System.Windows.Forms.Control.Width%2A> 属性，使其比所有的选项卡都窄。  
  
### 在控件一侧排列选项卡  
  
-   将 <xref:System.Windows.Forms.TabControl> 的 <xref:System.Windows.Forms.TabControl.Alignment%2A> 属性设置为 <xref:System.Windows.Forms.TabAlignment> 或 <xref:System.Windows.Forms.TabAlignment>。  
  
### 以编程方式启用或禁用选项卡上的所有控件  
  
1.  将 <xref:System.Windows.Forms.TabPage> 的 <xref:System.Windows.Forms.TabPage.Enabled%2A> 属性设置为 `true` 或 `false`。  
  
    ```vb  
    TabPage1.Enabled = False  
  
    ```  
  
    ```csharp  
    tabPage1.Enabled = false;  
  
    ```  
  
    ```cpp  
    tabPage1->Enabled = false;  
    ```  
  
### 将选项卡显示为按钮  
  
-   将 <xref:System.Windows.Forms.TabControl> 的 <xref:System.Windows.Forms.TabControl.Appearance%2A> 属性设置为 <xref:System.Windows.Forms.TabAppearance> 或 <xref:System.Windows.Forms.TabAppearance>。  
  
## 请参阅  
 [TabControl 控件](../../../../docs/framework/winforms/controls/tabcontrol-control-windows-forms.md)   
 [TabControl 控件概述](../../../../docs/framework/winforms/controls/tabcontrol-control-overview-windows-forms.md)   
 [如何：将控件添加到选项卡页](../../../../docs/framework/winforms/controls/how-to-add-a-control-to-a-tab-page.md)   
 [如何：禁用选项卡页](../../../../docs/framework/winforms/controls/how-to-disable-tab-pages.md)   
 [如何：使用 Windows 窗体 TabControl 添加和移除选项卡](../../../../docs/framework/winforms/controls/how-to-add-and-remove-tabs-with-the-windows-forms-tabcontrol.md)