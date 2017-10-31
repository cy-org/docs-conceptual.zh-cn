---
title: "如何：在 Windows 窗体上停靠控件 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 停靠"
  - "Dock 属性"
  - "资源管理器样式的应用程序, 创建"
  - "Windows 窗体控件, 填充工作区"
ms.assetid: bc11f2e4-e90a-4830-b0e2-f43b6e2b8bec
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：在 Windows 窗体上停靠控件
可将控件停靠到窗体的边缘或使它们填充控件的容器（窗体或容器控件）。  例如，“Windows 资源管理器”将其 <xref:System.Windows.Forms.TreeView> 控件停靠到窗口的左侧，将其 <xref:System.Windows.Forms.ListView> 控件停靠到窗口的右侧。  对于所有可见的 Windows 窗体控件，使用 <xref:System.Windows.Forms.Control.Dock%2A> 属性来定义停靠模式。  
  
> [!NOTE]
>  控件以与 Z 顺序相反的顺序停靠。  
  
 <xref:System.Windows.Forms.Control.Dock%2A> 属性与 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性进行交互。  有关更多信息，请参见 [AutoSize 属性概述](../../../../docs/framework/winforms/controls/autosize-property-overview.md)。  
  
### 停靠控件  
  
1.  选择要停靠的控件。  
  
2.  在“属性”窗口中，单击 <xref:System.Windows.Forms.Control.Dock%2A> 属性右侧的箭头。  
  
     显示一个编辑器，其中显示一系列表示窗体边缘和中心的框。  
  
3.  单击表示控件停靠位置的窗体边缘的按钮。  若要填充控件的窗体或容器控件的内容，请单击中心框。  单击**“\(none\)”**禁用停靠。  
  
     控件的大小将自动调整以适合停靠边缘的边界。  
  
    > [!NOTE]
    >  继承的控件必须是 `Protected`，才能停靠。  若要更改控件的访问级别，请在“属性”窗口中设置其**“Modifier”**属性。  
  
## 请参阅  
 [Windows 窗体控件](../../../../docs/framework/winforms/controls/index.md)   
 [排列 Windows 窗体上的控件](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [标记单个 Windows 窗体控件并提供它们的快捷方式](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [根据功能列出的 Windows 窗体控件](../../../../docs/framework/winforms/controls/windows-forms-controls-by-function.md)   
 [如何：在 FlowLayoutPanel 控件中锚定和停靠子控件](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-flowlayoutpanel-control.md)   
 [如何：在 TableLayoutPanel 控件中锚定和停靠子控件](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)   
 [AutoSize 属性概述](../../../../docs/framework/winforms/controls/autosize-property-overview.md)   
 [如何：在 Windows 窗体上锚定控件](../../../../docs/framework/winforms/controls/how-to-anchor-controls-on-windows-forms.md)