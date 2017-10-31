---
title: "如何：使用设计器用 Windows 窗体创建多窗格用户界面 | Microsoft Docs"
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
  - "多窗格用户界面"
  - "SplitContainer 控件 [Windows 窗体], 使用设计器"
  - "用户界面, 多窗格"
ms.assetid: c3f9294d-a26c-4198-9242-f237f55f7573
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：使用设计器用 Windows 窗体创建多窗格用户界面
在下面的过程中，将创建一个类似于在 Microsoft Outlook 中使用的多窗格用户界面，该界面中包含**“文件夹列表”**、**“邮件”**窗格和**“预览”**窗格。  这种排列主要是通过在窗体上停靠控件实现的。  
  
 在停靠控件时，可以确定控件要紧靠父容器的哪个边缘。  这样，如果将 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle>，控件的右边缘将停靠在它的父控件的右边缘。  此外，控件停靠边缘的大小将调整为与它的容器控件的大小匹配。  有关 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 属性工作方式的更多信息，请参见 [如何：在 Windows 窗体上停靠控件](../../../../docs/framework/winforms/controls/how-to-dock-controls-on-windows-forms.md)。  
  
 该过程的重点是在窗体上排列 <xref:System.Windows.Forms.SplitContainer> 和其他控件，而不是添加功能以使得应用程序类似于 Microsoft Outlook。  
  
 若要创建该用户界面，请将所有控件放到 <xref:System.Windows.Forms.SplitContainer> 控件（其左侧面板中包含 <xref:System.Windows.Forms.TreeView> 控件）中。  <xref:System.Windows.Forms.SplitContainer> 控件的右侧面板中包含另一个 <xref:System.Windows.Forms.SplitContainer> 控件，其中 <xref:System.Windows.Forms.ListView> 控件在 <xref:System.Windows.Forms.RichTextBox> 控件上方。  这些 <xref:System.Windows.Forms.SplitContainer> 控件支持在窗体上分别调整其他控件的大小。  可以改编此过程中的方法，制作出您自己的自定义用户界面。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在设计时创建 Outlook 样式的用户界面  
  
1.  创建新的“Windows 应用程序”项目。  有关详细信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)。  
  
2.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.SplitContainer> 控件拖到窗体上。  在**“属性”**窗口中，将 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle>。  
  
3.  将 <xref:System.Windows.Forms.TreeView> 控件从**“工具箱”**拖到 <xref:System.Windows.Forms.SplitContainer> 控件的左侧面板中。  在**“属性”**窗口中，通过单击值编辑器（在单击向下键时显示）中的左侧面板将 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle>。  
  
4.  从**“工具箱”**拖动另一个 <xref:System.Windows.Forms.SplitContainer> 控件；然后将它放到窗体中添加的 <xref:System.Windows.Forms.SplitContainer> 控件的右侧面板中。  在**“属性”**窗口中，将 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle>，并将 <xref:System.Windows.Forms.SplitContainer.Orientation%2A> 属性设置为 <xref:System.Windows.Forms.Orientation>。  
  
5.  将 <xref:System.Windows.Forms.ListView> 控件从**“工具箱”**拖到窗体中添加的第二个 <xref:System.Windows.Forms.SplitContainer> 控件的上方面板中。  将 <xref:System.Windows.Forms.ListView> 控件的 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle>。  
  
6.  将 <xref:System.Windows.Forms.RichTextBox> 控件从**“工具箱”**拖到第二个 <xref:System.Windows.Forms.SplitContainer> 控件的下方面板中。  将 <xref:System.Windows.Forms.RichTextBox> 控件的 <xref:System.Windows.Forms.SplitContainer.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle>。  
  
     此时，如果按 F5 运行应用程序，窗体将显示由三部分组成的用户界面，这类似于 Microsoft Outlook 的用户界面。  
  
    > [!NOTE]
    >  将鼠标指针放在 <xref:System.Windows.Forms.SplitContainer> 控件中的任一拆分器上时，可以调整内部尺寸的大小。  
  
     在应用程序开发中，此时已经设计了一个复杂的用户界面。  下一步要做的就是应用程序本身的编程了（可能需要将 <xref:System.Windows.Forms.TreeView> 控件和 <xref:System.Windows.Forms.ListView> 控件连接到某种数据源）。  有关将控件连接到数据的更多信息，请参见 [数据绑定和 Windows 窗体](../../../../docs/framework/winforms/data-binding-and-windows-forms.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.SplitContainer>   
 [SplitContainer 控件](../../../../docs/framework/winforms/controls/splitcontainer-control-windows-forms.md)