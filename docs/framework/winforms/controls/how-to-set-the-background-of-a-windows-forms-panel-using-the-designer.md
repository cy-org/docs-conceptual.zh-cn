---
title: "如何：使用设计器设置 Windows 窗体面板的背景 | Microsoft Docs"
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
  - "背景色, Windows 窗体 Panel 控件"
  - "背景图像, Windows 窗体 Panel 控件"
  - "颜色, Windows 窗体 Panel 控件"
  - "Panel 控件 [Windows 窗体], 背景"
ms.assetid: db83cf54-3c69-4b08-ac6c-25b9b5abb1b0
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：使用设计器设置 Windows 窗体面板的背景
Windows 窗体 <xref:System.Windows.Forms.Panel> 控件既可以显示背景颜色又可以显示背景图像。  <xref:System.Windows.Forms.Control.BackColor%2A> 属性为面板中包含的控件（如标签和单选按钮）设置背景颜色。  如果未设置 <xref:System.Windows.Forms.Control.BackgroundImage%2A> 属性，则所选 <xref:System.Windows.Forms.Control.BackColor%2A> 将填充整个面板。  如果设置 <xref:System.Windows.Forms.Control.BackgroundImage%2A> 属性，则会在面板包含的控件后面显示图像。  
  
 下面的过程需要一个**“Windows 应用程序”**项目，该项目拥有一个包含 <xref:System.Windows.Forms.Panel> 控件的窗体。  有关如何设置此类项目的信息，请参见 [How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa) 和 [如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在 Windows 窗体设计器中设置背景  
  
1.  选择 <xref:System.Windows.Forms.Panel> 控件。  
  
2.  在**“属性”**窗口中，单击 <xref:System.Windows.Forms.Control.BackColor%2A> 属性旁边的箭头按钮以显示一个带有三个选项卡的窗口。  
  
3.  选择**“自定义”**选项卡以显示颜色调色板。  
  
4.  选择**“Web”**或**“系统”**选项卡以显示预定义的颜色名称的列表，然后选择一种颜色。  
  
5.  在**“属性”**窗口中，单击 <xref:System.Windows.Forms.Control.BackgroundImage%2A> 属性旁的箭头按钮。  
  
6.  在**“打开”**对话框中，选择想要显示的文件。  
  
## 请参阅  
 <xref:System.Windows.Forms.Control.BackColor%2A>   
 <xref:System.Windows.Forms.Control.BackgroundImage%2A>   
 [Panel 控件](../../../../docs/framework/winforms/controls/panel-control-windows-forms.md)   
 [Panel 控件概述](../../../../docs/framework/winforms/controls/panel-control-overview-windows-forms.md)   
 [如何：使用设计器用 Windows 窗体面板控件对控件进行分组](../../../../docs/framework/winforms/controls/group-controls-with-wf-panel-control-using-the-designer.md)