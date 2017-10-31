---
title: "如何：在 Windows 窗体上锚定控件 | Microsoft Docs"
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
  - "Anchor 属性, 启用可调整大小的窗体"
  - "控件 [Windows 窗体], 锚定"
  - "控件 [Windows 窗体], 定位"
  - "窗体, 调整大小"
  - "调整窗体的大小"
  - "屏幕分辨率和控件显示"
  - "Windows 窗体控件, 屏幕分辨率"
  - "Windows 窗体控件, 大小"
  - "Windows 窗体, 调整大小"
ms.assetid: 59ea914f-fbd3-427a-80fe-decd02f7ae6d
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：在 Windows 窗体上锚定控件
如果要设计用户可在运行时调整其大小的窗体，则该窗体上的控件应能正确地调整大小及重新定位。  若要与窗体一起动态调整控件的大小，可使用 Windows 窗体控件的 <xref:System.Windows.Forms.Control.Anchor%2A> 属性。  <xref:System.Windows.Forms.Control.Anchor%2A> 属性定义控件的定位点位置。  当控件锚定到某个窗体时，如果该窗体的大小被调整，该控件维持它与定位点位置之间的距离不变。  例如，如果一个 <xref:System.Windows.Forms.TextBox> 控件锚定于窗体的左、右和底边缘，那么当调整该窗体的大小时，该 <xref:System.Windows.Forms.TextBox> 控件将在水平方向上调整大小，以便维持与该窗体右边和左边的距离不变。  另外，控件垂直定位其自身，以便其到窗体底边的距离始终不变。  如果控件未锚定而窗体的大小被调整，则该控件相对于窗体边缘的位置将发生变化。  
  
 <xref:System.Windows.Forms.Control.Anchor%2A> 属性与 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性进行交互。  有关更多信息，请参见 [AutoSize 属性概述](../../../../docs/framework/winforms/controls/autosize-property-overview.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在窗体上锚定控件  
  
1.  选择要锚定的控件。  
  
    > [!NOTE]
    >  可以按照如下方法同时锚定多个控件：按下 Ctrl 键，单击各个控件以进行选择，然后按照上面过程中的其余步骤操作。  
  
2.  在**“属性”**窗口中，单击 <xref:System.Windows.Forms.Control.Anchor%2A> 属性右边的箭头。  
  
     显示一个编辑器，该编辑器显示一个十字线。  
  
3.  若要设置定位点，单击该十字线的上、左、右或下部分。  
  
     默认情况下，控件锚定到左边和上边。  
  
4.  若要清除已锚定的控件的边，请单击该十字线的相应臂。  
  
5.  要关闭 <xref:System.Windows.Forms.Control.Anchor%2A> 属性编辑器，可以再次单击 <xref:System.Windows.Forms.Control.Anchor%2A> 属性名。  
  
 当窗体在运行时显示时，该控件调整大小以保持与该窗体边缘的距离不变。  到锚定边缘的距离始终保持在 Windows 窗体设计器中定位该控件时所定义的距离。  
  
> [!NOTE]
>  某些控件（如 <xref:System.Windows.Forms.ComboBox> 控件）有高度限制。  将控件锚定到其窗体或容器的底部无法强制该控件超过其高度限制。  
  
 继承的控件只有处于 `Protected` 状态才能够被锚定。  若要更改控件的访问级别，请在**“属性”**窗口中设置其 `Modifiers` 属性。  
  
## 请参阅  
 [Windows 窗体控件](../../../../docs/framework/winforms/controls/index.md)   
 [排列 Windows 窗体上的控件](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [AutoSize 属性概述](../../../../docs/framework/winforms/controls/autosize-property-overview.md)   
 [如何：在 Windows 窗体上停靠控件](../../../../docs/framework/winforms/controls/how-to-dock-controls-on-windows-forms.md)   
 [演练：使用 FlowLayoutPanel 在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)   
 [演练：使用 TableLayoutPanel 在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)   
 [演练：使用 Padding、Margins 和 AutoSize 属性对 Windows 窗体控件进行布局](../../../../docs/framework/winforms/controls/windows-forms-controls-padding-autosize.md)