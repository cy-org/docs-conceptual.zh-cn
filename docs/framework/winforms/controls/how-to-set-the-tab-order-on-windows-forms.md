---
title: "如何：设置 Windows 窗体上的 Tab 键顺序 | Microsoft Docs"
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
  - "TabStop"
  - "TabIndex"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "控件 [Windows 窗体], 设置 Tab 键顺序"
  - "Tab 键次序, Windows 窗体上的控件"
  - "Windows 窗体控件, 设置 Tab 键顺序"
  - "Windows 窗体, 设置 Tab 键顺序"
ms.assetid: 71fa8e76-0472-414b-ad3c-0f90166e0ad7
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：设置 Windows 窗体上的 Tab 键顺序
Tab 键顺序就是用户按 TAB 键将焦点从一个控件移动到另一个控件的顺序。  每个窗体都有其自己的 Tab 键顺序。  默认情况下，Tab 键顺序与创建控件的顺序相同。  Tab 键顺序的编号从 0 开始。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 设置控件的 Tab 键顺序  
  
1.  在**“视图”**菜单上，单击**“Tab 键顺序”**。  
  
     它激活窗体上的 Tab 键顺序选择模式。  在每个控件的左上角出现一个数字（表示 <xref:System.Windows.Forms.Control.TabIndex%2A> 属性）。  
  
2.  依次单击控件以建立所需的 Tab 键顺序。  
  
    > [!NOTE]
    >  控件在 Tab 键顺序内的位置可设为任何大于或等于 0 的值。  当出现重复时，将对两个控件的 Z\-顺序进行计算，位于上面的控件将拥有优先的 Tab 键顺序。  （Z\-顺序是窗体上的控件沿窗体的 Z 轴 \[深度\] 的可视化分层。  Z 顺序确定哪些控件位于其他控件的前面。）有关 Z\-顺序的更多信息，请参见[将 Windows 窗体上的对象分层](../../../../docs/framework/winforms/controls/how-to-layer-objects-on-windows-forms.md)。  
  
3.  完成后，再次单击**“视图”**菜单中的**“Tab 键顺序”**，离开 Tab 键顺序模式。  
  
    > [!NOTE]
    >  无法获得焦点的控件以及禁用的和不可见的控件，都没有 <xref:System.Windows.Forms.Control.TabIndex%2A> 属性，也不包括在 Tab 键顺序中。  当用户按 Tab 键时，将跳过这些控件。  
  
 另外，可以在“属性”窗口中使用 <xref:System.Windows.Forms.Control.TabIndex%2A> 属性设置 Tab 键顺序。  控件的 <xref:System.Windows.Forms.Control.TabIndex%2A> 属性确定控件在 Tab 键顺序中的位置。  默认情况下，描述的第一个控件的 <xref:System.Windows.Forms.Control.TabIndex%2A> 值为 0，第二个控件的 <xref:System.Windows.Forms.Control.TabIndex%2A> 为 1，依此类推。  
  
 另外，默认情况下，<xref:System.Windows.Forms.GroupBox> 控件有自己的 <xref:System.Windows.Forms.Control.TabIndex%2A> 值，该值是一个整数。  <xref:System.Windows.Forms.GroupBox> 控件本身无法在运行时具有焦点。  因此，<xref:System.Windows.Forms.GroupBox> 内的每个控件都有其自己的十进制 <xref:System.Windows.Forms.Control.TabIndex%2A> 值（从 .0 开始）。  当 <xref:System.Windows.Forms.GroupBox> 控件的 <xref:System.Windows.Forms.Control.TabIndex%2A> 递增时，其中的控件自然也相应递增。  如果将 <xref:System.Windows.Forms.Control.TabIndex%2A> 值从 5 更改为 6，则该组中第一个控件的 <xref:System.Windows.Forms.Control.TabIndex%2A> 值自动更改为 6.0，依此类推。  
  
 最后，可在 Tab 键顺序中跳过窗体上众多控件中的任何控件。  通常，运行时连续按 TAB 键可选择 Tab 键顺序中的每个控件。  通过关闭 <xref:System.Windows.Forms.Control.TabStop%2A> 属性，可在窗体的 Tab 键顺序中忽略某控件。  
  
#### 从 Tab 键顺序中移除控件  
  
1.  在“属性”窗口中将控件的 <xref:System.Windows.Forms.Control.TabStop%2A> 属性设置为 `false`。  
  
     在用 TAB 键循环控件时，<xref:System.Windows.Forms.Control.TabStop%2A> 属性被设置为 `false` 的控件即使被跳过，它仍将保持其在 Tab 键顺序中的位置。  
  
    > [!NOTE]
    >  单选按钮组在运行时只有一个制表位。  选定按钮（即，其 <xref:System.Windows.Forms.RadioButton.Checked%2A> 属性设置为 `true` 的按钮）的 <xref:System.Windows.Forms.Control.TabStop%2A> 属性自动设置为 `true`，而其他按钮的 <xref:System.Windows.Forms.Control.TabStop%2A> 属性则设置为 `false`。  有关对 <xref:System.Windows.Forms.RadioButton> 控件进行分组的更多信息，请参见[将 Windows 窗体 RadioButton 控件分组独立工作](../../../../docs/framework/winforms/controls/how-to-group-windows-forms-radiobutton-controls-to-function-as-a-set.md)。  
  
## 请参阅  
 [Windows 窗体控件](../../../../docs/framework/winforms/controls/index.md)   
 [排列 Windows 窗体上的控件](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [根据功能列出的 Windows 窗体控件](../../../../docs/framework/winforms/controls/windows-forms-controls-by-function.md)