---
title: "如何：设计时将控件与窗体边缘对齐 | Microsoft Docs"
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
  - "自定义控件 [Windows 窗体], 使用设计器停靠"
  - "Dock 属性, 对齐控件（使用设计器）"
ms.assetid: 51f08998-5e3b-4330-be58-a4edd0eb60f4
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：设计时将控件与窗体边缘对齐
通过设置 <xref:System.Windows.Forms.Control.Dock%2A>，可以使控件与窗体的边缘对齐。  此属性指定控件在窗体中的驻留位置。  可以将 <xref:System.Windows.Forms.Control.Dock%2A> 属性设置为下列值：  
  
|设置|控件上的效果|  
|--------|------------|  
|<xref:System.Windows.Forms.DockStyle>|停靠到窗体底部。|  
|<xref:System.Windows.Forms.DockStyle>|占据窗体中的所有剩余空间。|  
|<xref:System.Windows.Forms.DockStyle>|停靠到窗体的左侧。|  
|<xref:System.Windows.Forms.DockStyle>|不在任何位置停靠，它显示在由 <xref:System.Windows.Forms.Control.Location%2A> 属性指定的位置。|  
|<xref:System.Windows.Forms.DockStyle>|停靠到窗体的右侧。|  
|<xref:System.Windows.Forms.DockStyle>|停靠到窗体的顶部。|  
  
 也可以在代码中设置这些值。  有关更多信息，请参见 [如何：使控件与窗体边缘对齐](../../../../docs/framework/winforms/controls/how-to-align-a-control-to-the-edges-of-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在设计时设置控件的 Dock 属性  
  
1.  在 Windows 窗体设计器中选择控件。  
  
2.  在**“属性”**窗口中，单击 <xref:System.Windows.Forms.Control.Dock%2A> 属性旁边的下拉框。  
  
     将显示表示六种可能的 <xref:System.Windows.Forms.Control.Dock%2A> 设置的图形界面。  
  
3.  选择相应的设置。  
  
4.  控件将按该设置指定的方式停靠。  
  
## 请参阅  
 <xref:System.Windows.Forms.Control.Dock%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Control.Anchor%2A?displayProperty=fullName>   
 [如何：使控件与窗体边缘对齐](../../../../docs/framework/winforms/controls/how-to-align-a-control-to-the-edges-of-forms.md)   
 [演练：使用对齐线在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)   
 [如何：在 Windows 窗体上锚定控件](../../../../docs/framework/winforms/controls/how-to-anchor-controls-on-windows-forms.md)   
 [如何：在 TableLayoutPanel 控件中锚定和停靠子控件](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)   
 [如何：在 FlowLayoutPanel 控件中锚定和停靠子控件](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-flowlayoutpanel-control.md)   
 [演练：使用 TableLayoutPanel 在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)   
 [演练：使用 FlowLayoutPanel 在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)   
 [设计时开发 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)